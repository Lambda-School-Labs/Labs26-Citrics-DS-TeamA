# Citrics A

## Description:
Finding a place to live is hard! Nomads struggle with finding the right city for them. Citrics is a city comparison tool that allows users to compare cities and find cities based on user preferences.

### **Mission:**
Using visualizations for a variety of metrics, such as how walkable a city is, predominant industries, unemployment rates, as well as predictions for rental prices, our users can make a more well-informed decision on what is best for them before making their move.

[AWS Deployed API](https://ds.citrics.dev/) / [Web-Deployed Implementation](https://a.citrics.dev/)

## Directory Structure
```
├── data <- Collection of datasets used in this project.
│    ├── BLS <- Files related to the Bureau of Labor Statistics data.
│    │    ├── BLS 2019 Data - All May 2019 Data.csv.zip <- All BLS data in .zip file.
│    │    └── BLS_sub_clean1.csv <- CSV of clean BLS data.
│    ├── census <- Files related to Census data.
│    │    ├── cleaned_census_data.csv <- CSV of clean census data.
│    │    └── sub-est2019_all.csv <- CSV of census data (unclean).
|    ├── climate <- files related to climate and time zone data.
|    |    ├── zip_to_latlon.csv <- raw timezone data containing city names, zipcodes, and latitutes and longitudes.
|    |    ├── climate.csv <- processed climate data containing all data from zip_to_latlon.csv with data pulled from the climate API.
│    ├── rental
│    │    ├── Apartment_List_Rent_Data_-_City_2020-8.csv <- CSV of Apartment List rental data.
│    │    ├── apt_rental_price_clean1.csv <- CSV of cleaned Apartment List rental data.
│    │    └── rental.csv <- CSV of rental price predictions.
│    ├── static <- Contains static data CSV.
│    │    └── static.csv <- CSV of all static data.
│    ├── weather <- Collection of CSV files related to historical weather data.
│    |    └── *.csv <- CSV file containing historical data for city in file name.
|    ├── whimsical <- Collection of whimsical boards for use in planning an ideation.
|    |    ├── APISchema.png <- API schema for predictive routes.
|    |    └── Pickling.png <- Single-route schema for pickling time-series models.
|    └── README.md <- README file for data directory.    
├── development <- Directory containing development materials outside of the API itself Jupyter.   
|    ├── __init__.py <- __init__.py file
|    ├── notebooks <- Directory containing Jupyter Notebooks.
│    │    ├── basic_rental_cleanup.ipynb <- Jupyter notebook for price data cleaning.
│    │    ├── bls_eda_1.ipynb <- Jupyter notebook for BLS data cleaning.
|    |    ├── climate.ipynb <- Jupyter notebook for fetching climate and timezone data from climate API.
│    │    ├── get_stats.ipynb <- Jupyter notebook, precursor to weather_pred route.
│    │    ├── Labs_26_Data_Science.ipynb <- Labs starter notebook.
│    │    ├── Labs_26_Data_Science.ipynb <- Labs starter notebook (Zone Identifier).
|    |    ├── population.ipynb <- Preroute for project/app/api/census_pred.py
│    │    ├── rental.ipynb <- Jupyter notebook for rental data preprocessing.
│    │    ├── rental_pred.ipynb <- Jupyter notebook for rental predictions.
│    │    ├── rental_viz1.ipynb <- Jupyter notebook for visualization. (DEPRECATED)
│    │    ├── rent_price_viz_dev.ipynb <- Jupyter notebook for rental visualization from database. (DEPRECATED)
│    │    ├── static_dev.ipynb <- Jupyter notebook for fetching 
static data.
|    |    └── tsa.ipynb <- Jupyter notebook with demostrations of basic Time Series Analysis and modeling techniques.  
|    ├── preroutes <- Preroutes, files built outside of API itself in preparation for building API routes.
│    │    ├── __init__.py <- __init__.py file
│    │    └── weather.py <- Preroute file for fetching historical weather data.
|    ├── utilities <- Utilities for use in managing deployment,retrieving data from third-party APIs, and using the database.
│    |    ├── config.py <- Utility file to change from team to personal Docker image.
│    |    ├── database.py <- Utility file for PostgreSQL database.
|    |    ├── db_sentry.py - Utility for managing run-away database connections.
│    |    ├── __init__.py <- __init__.py file
│    |    ├── insert.py <- Inserts World Weather Online API data into database.
│    |    ├── README.md <- Markdown file explaining usage of config.py, weather.py, and insert.py
│    |    └── walk.py <- Utility file for generalizing Walk Scores and populating database.
|    └── README.md <- README file for development directory.       
├── project <- Main project files.
│    ├── app <- Folder containing all files related to app deployment.
│    │    ├── api <- Files used in API deployment.
│    │    │    ├── __init__.py <- Init file for api folder.
│    │    │    ├── bls_jobs1.py <- Returns JSON string containing job data for top industry in BLS data.
│    │    │    ├── bls_viz.py <- Returns JSON output of BLS data visualizations.
│    │    │    ├── bls_viz_view.py <- Returns PNG of BLS data visualizations.
│    │    │    ├── census.py <- Returns Census data.
|    |    |    ├── census_pred.py <- Returns rental predictions for two years from the present (2020)
│    │    │    ├── current.py <- Returns current weather data calculated in both imperial and metric.
│    │    │    ├── predict.py <- Starter predict file. (DEPRECATED)
│    │    │    ├── rent_city_states.py <- Returns cities and states, dealing with duplicate values (requested by front-end).
│    │    │    ├── rental1.py <- Fetches rental prices from SQL database.
│    │    │    ├── rental_pred.py <- Makes rental price predictions.
│    │    │    ├── rentviz1.py <- Returns JSON output of rental price visualizations, unstyled. (DEPRECATED)
│    │    │    ├── rentviz2.py <- Returns JSON output of rental price visualizations, styled.
│    │    │    ├── rentviz2_view.py <- Returns PNG of rental price predictions, styled. (DEPRECATED)
│    │    │    ├── rentviz_view.py <- Returns PNG of rental price predictions, unstyled. (DEPRECATED)
│    │    │    ├── static.py <- Returns all static data.
│    │    │    ├── viz.py <- Returns JSON output of unemployment data, styled.
│    │    │    ├── viz_view.py <- Returns PNG of unemployment data, styled. (DEPRECATED)
│    │    │    ├── walkability.py <- Returns Walk Score calculations stored in database.
│    │    │    └── weather_pred.py <- Makes weather predictions.
│    │    ├── tests <- FastAPI TestClient test files.
│    │    │    ├── __init__.py <- Init file for tests filder.
│    │    │    ├── test_main.py <- Main TestClient file.
│    │    │    ├── test_predict.py <- Predict TestClient file.
│    │    │    └── test_viz.py <- Visualization TestClient file.
│    │    ├── __init__.py <- Init file.
│    │    ├── database.py <- Utility file for PostgreSQL database usage.
│    │    ├── main.py <- Main API file; handles routes.
│    │    ├── sql_query_function.py <- Utility file for SQL queries.
│    │    └── string_formatter.py <- Utility file for sanitization of input for formatting used in data/weather.
│    ├── Dockerfile <- Dockerfile for Docker deployment.
│    └── requirements.txt <- Requirements file.
├── .ebignore <- Files and directories to ignore in ElasticBeanstalk deployment.
├── .gitignore <- Files and directories to ignore in GitHub repo.
├── Dockerrun.aws.json <- Dockerrun file for AWS deployment.
├── LICENSE <- License for this software.
├── Pipfile <- Pipfile for pipenv.
├── Pipfile.lock <- Lock for Pipfile.
├── README.md  <- You are here! Data Science API README file.
├── docker-compose.yml <- Build file for Docker deployment.
└── requirements.txt  <- The requirements file for reproducing environment.
```

## **Resources**

**LABS**
- [Labs Calendar](https://calendar.google.com/calendar/u/0/r?cid=Y19hMG5ydDdsNWhpbm52OHM4bHVwMmJpN2tjc0Bncm91cC5jYWxlbmRhci5nb29nbGUuY29t)
- [Labs Curriculum](https://github.com/LambdaSchool/labs-curriculum/tree/master/Labs%20Curriculum) (Sprint and Module Prompts)
- [Labs Student Guide](https://www.notion.so/Labs-26-Student-Guide-95d845339f8041de85252f743f0d709d)
- [Module and Sprint Submission Instructions](https://www.notion.so/Module-and-Sprint-Entry-Submission-Logistics-a6003eb8288b4fd1af0fb40a1a42d278)

**LABS DS STARTER**
- [Labs DS Docs](https://docs.labs.lambdaschool.com/data-science/)
- [Labs DS Notebook](https://colab.research.google.com/drive/1MbF-L6mKy_JA9L6wxBCb5_Vch3PX3RRL?usp=sharing) - Ryan Herr
- [Labs DS Notebook - Local](development/notebooks/Labs_26_Data_Science.ipynb) - Ryan Herr
- [Schedule with Ryan Herr (Calendly)](https://calendly.com/ryan-herr)

**CITRICS**
- [Citrics Product Overview](https://www.notion.so/Labs-26-Product-Overview-a81834be6b7d4fefb3c1291bb17e2c23)
- [Citrics A Trello](https://trello.com/b/dEeOumaD/citrics-team-a)
- [Citrics A Whimsical Page](https://whimsical.com/LwTzXGSfiS3YegDRoEVgXY)

**DATA**
- [Apartment Rental Price Data](https://www.apartmentlist.com/research/category/data-rent-estimates) (NOTE: Does not include HI, WV or PR)
- [Bureau of Labor Staticstics](https://www.bls.gov/oes/tables.htm)
- [Climate Data](https://www.ncei.noaa.gov/metadata/geoportal/rest/metadata/item/gov.noaa.ncdc:C00821/html)
- [Climate Zone API](http://climateapi.scottpinkelman.com/)
- [Historical Weather API](https://www.worldweatheronline.com/developer/api/historical-weather-api.aspx) (NOTE: 60 day free trial √)
- [Jobs Data](https://datausa.io/cart)
- [Population](https://public.opendatasoft.com/explore/dataset/worldcitiespop/api/?disjunctive.country)
- [US Census Bureau](https://www.census.gov/data/tables/time-series/demo/popest/2010s-total-cities-and-towns.html)
- [WalkScore API](https://www.walkscore.com/professional/api.php) (NOTE: Developer-friendly documentation)
- [Weather Data](https://openweathermap.org/api) (NOTE: Potentially pricy ...)
- [Yelp API](https://www.yelp.com/developers) (NOTE: Requires sign-up.)
- [Zillow API](https://www.zillow.com/howto/api/APIOverview.htm) (NOTE: Requires sign-up / application.)

**Predictive Modeling**
- [Explanatory Notebook](development/notebooks/tsa.ipynb)
- [Python for Time Series Data Analysis  - Udemy Course](https://www.udemy.com/course/python-for-time-series-data-analysis/)
- [Pandas Time Series Docs](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)
- [Python Datetime Module Docs](https://docs.python.org/3/library/datetime.html#module-datetime)
- [Statsmodels](https://www.statsmodels.org/stable/index.html)

**FastAPI**
- [Route Referencing](project/app/api/README.md)

**AWS / DOCS**
- [AWS - Postgres Deployment Docs](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)
- [AWS Dashboard](https://console.aws.amazon.com/route53/v2/home#Dashboard)
- [AWS Instructions](https://docs.labs.lambdaschool.com/guides/aws/elastic-beanstalk/elastic-beanstalk-dns)
- [AWS RDS](https://console.aws.amazon.com/rds/home?region=us-east-1#)
- [Amazon Web Services in Plain English](https://expeditedsecurity.com/aws-in-plain-english/)
- [Deploying to AWS](https://docs.labs.lambdaschool.com/data-science/#deploy-to-aws)
- [Docker Images Docs](https://docs.docker.com/engine/reference/commandline/images/)
- [EB Docker Management](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.container.console.html)
- [EB Environment Management](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-softwaresettings.html)
- [Elastic Beanstalk Environments](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environments)


**OTHER REFERENCES AND DOCUMENTATION**
- [How to Access BLS API](http://danstrong.tech/blog/BLS-API/)
- [Plotly Docs](https://plotly.com/python/)