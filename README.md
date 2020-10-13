# Climate Analysis of Honolulu, Hawaii
![Hawaii Surf](https://www.bosshunting.com.au/wp-content/uploads/2020/03/screen-shot-2017-03-01-at-83152-pm.png)

## Challenge Instructions
This project utilizes Python and SQLAlchemy to achieve basic climate analysis and data exploration of the climate database in Hawaii. Based on the initial analysis, a Flask API was designed by using these queries.

## Climate Analysis and Exploration
The basic climate analysis was completed by using SQLAlchemy ORM queries, Pandas, and Matplotlib.
- Precipitation Analysis
  - A query was designed to retrieve the last 12 months of precipitation data
  - The `date` and `prcp` values of the query results were selected and loaded into a Pandas DataFrame
  - The results were sorted by `date` and plotted using `plot` method
  - A summary statistics for the precipitation data was displayed using Pandas
<p align="center">
  <img src="https://github.com/Jiuhe2020/sqlalchemy-challenge/blob/master/images/Prcp.png" height="30%" width="30%">
</p>

- Station Analysis
  - A query was designed to calculate the total number of stations in Hawaii
  - The query finds the most active stations using functions as `func.min`, `func.max`, `func.avg`, and `func.count`
  - Another query was designed to retrieve the last 12 months of temperature observation data (TOBS), which were later filtered by the station with the highest number of observations and plotted as a histogram with `bins=12`
<p align="center">
  <img src="https://github.com/Jiuhe2020/sqlalchemy-challenge/blob/master/images/Temp.png" height="30%" width="30%">
</p>

## Climate App
A Flask API was designed based on the queries from above and Flask `jsonify` was used to convert API data into a valid JSON response object. Routes were created as follows:
- `/`
  - Home page
  - List all routes that are available
- `/api/v1.0/precipitation`
  - Convert the query results to a dictionary using `date` as the key and `prcp` as the value
  - Return the JSON representation of your dictionary
- `/api/v1.0/stations`
  - Return a JSON list of stations from the dataset
- `/api/v1.0/tobs`
  - Query the dates and temperature observations of the most active station for the last year of data
  - Return a JSON list of temperature observations (TOBS) for the previous year
- `/api/v1.0/<start> and /api/v1.0/<start>/<end>`
  - Return a JSON list of the minimum temperature, the average temperature, and the max temperature for a given start or start-end range
  - When given the start only, calculate `TMIN`, `TAVG`, and `TMAX` for all dates greater than and equal to the start date
  - When given the start and the end date, calculate the `TMIN`, `TAVG`, and `TMAX` for dates between the start and end date inclusive

## BONUS: Other Analyses
### Temperature Analysis I
Hawaii is reputed to enjoy mild weather all year. Is there a meaningful difference between the temperature in, for example, June and December? Here the SQLAlchemy was used to identify the average temperature in June at all stations across all available years in the dataset. Same method was applied to December temperature.
> The unpaired t-test was used because it's comparing the means of two independent samples (Jun vs. Dec). Based on the t-test result, the difference in the means of Jun vs Dec was statistically significant.

### Temperature Analysis II
The function `calc_temps` was used to calculate the min, avg, and max temperature for my trip (2017-03-01 to 2017-03-10) from the previous year (2016-03-01 to 2016-03-10). A bar chart was created using the average temperature as the height and the peak-to-peak (TMAX-TMIN) value as the y error bar (YERR).
<p align="center">
  <img src="https://github.com/Jiuhe2020/sqlalchemy-challenge/blob/master/images/Trip_Avg_Temp.png" height="30%" width="30%">
</p>

### Daily Rainfall Average
The rainfall per weather station was calculated using the previous year's matching dates. The daily normals of my trip (2017-03-01 to 2017-03-10), including the average of the min, avg, and max temperatures, were also calculated by the `daily_normals` function. In the end, an area plot (`stacked=False`) was created for the daily normal during my trip.
<p align="center">
  <img src="https://github.com/Jiuhe2020/sqlalchemy-challenge/blob/master/images/Trip_Daily_Temp.png" height="30%" width="30%">
</p>

## List of Files
1. climate_analysis.ipynb: a Jupyter Notebook of Climate Analysis and Exploration + Bonus Questions
2. app.py: a Python file of Climate App
3. Resources: a folder containing hawaii_measurements.csv, hawaii_stations.csv and hawaii.sqlite

---
### Copyright
Jiuhe Zhu © 2020. All Rights Reserved.
