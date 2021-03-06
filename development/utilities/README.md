# Utilites 

## **config.py Explained**

### What config.py Does

The config.py file allows the Lambda School Labs 26 Citrics Team A Data Scientist to choose whether to build the team Docker image and deploy to the team AWS application or build his personal Docker image and deploy to his own application.

### Using config.py

The simplest part of this README;
in command line or terminal, simply type:

```
python development/utilities/config.py
```

You should see a message in command line or terminal prompting you to enter your Docker ID:

```
Docker ID:
```

Simply input your Docker ID if building and pushing to your personal AWS app. If building and pushing to the team app, use *Aaron Watkins'* Docker ID **ekselan**.  In the former case, you'll be greeted with the following in command line or terminal:

```
Docker ID: YOUR_DOCKER_ID
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "YOUR_DOCKER_ID/labs26-citrics-ds-teama_web:latest",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "8000"
    }
  ],
  "Command": "uvicorn app.main:app --workers 1 --host 0.0.0.0 --port 8000"
}
writing to ./Dockerrun.aws.json
```

Double check that the Dockerrun.aws.json file is up to date, and you can proceed with pushing to docker and deploying to AWS.

### Resetting config.py

Two reset options are built into the config.py script, reset and reset team.

The former resets the DOCKER_ID parameter to the default, like so:

```
Docker ID: reset
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "DOCKER_ID/labs26-citrics-ds-teama_web:latest",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "8000"
    }
  ],
  "Command": "uvicorn app.main:app --workers 1 --host 0.0.0.0 --port 8000"
}
```

The latter resets the DOCKER_ID parameter to the team Docker ID, *ekselan*:

```
Docker ID: reset team
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "ekselan/labs26-citrics-ds-teama_web:latest",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "8000"
    }
  ],
  "Command": "uvicorn app.main:app --workers 1 --host 0.0.0.0 --port 8000"
}
```

### Exiting the program:

When prompted for the Docker ID, the following inputs will close the program without altering the .json file.

```
Docker ID: exit
```

or

```
Docker ID: quit
```

or 

```
Docker ID: q
```

---

## **Using the weather.py file**

### Please read before using the weather.py file:)

The *weather.py* file is setup to pull data from the [World Weather Online API](https://www.worldweatheronline.com/developer/). The data from the API itself are stored in the data\weather directory along with information on the zipcodes of which locations statistics have already been pulled from the API.

### Instructions

#### Open an Account for the API

Follow the instructions in the following [link](https://www.worldweatheronline.com/developer/) in order to create an account for use with the World Weather Online API.

#### Packages

Before attempting to use the *weather.py* file, make sure to check that you have the correct versions of **python-dotenv** and **wwo_hist** as listed in the global requirements.txt file.

If not using a virtual environment or if using conda:
```
pip list
```

If using Pipenv

```
pipenv run pip list

python -m pipenv run pip list (if the former does not work)
```

As of the time of this writing the correct versions of these are

```
python-dotenv                      0.14.0
wwo-hist                           0.0.5
```

#### Installing Packages from requirements.txt file

If you using a Conda environment, entering

```
conda install --yes --file requirements.txt
```

in command line will ensure that the appropriate version of both packages
are installed on your local machine.

#### Individual Package Installation

If you are not installed and you are not using a virtual environment or are using Conda:
```
pip install python-dotenv==0.14.0
pip install wwo-hist==0.0.5
```

If the dependencies are already installed, and you are using Pipenv, simply activating the environment should do the trick.

Otherwise enter:

```
pipenv install python-dotenv==0.14.0
pipenv install wwo-hist==0.0.5
```

#### Running the weather.py file

Before pulling any new data, PLEASE CONSULT THE LEXICON, lexicon.txt, in the data\weather directory to ensure that you do not duplicate a call which has been already made.

Assuming you have not opened your wallet and are just using the trial version of API, you will be limited to 500 API calls per day which adds up to data for three cities. The weather.py file is set up to ask if you choose to include more than three cities, but leaves the option open in case you did open your wallet.

The weather.py file is setup to take the zip codes of the given locale as system arguments.
For example, if I wanted to pull data for New York, Los Angeles, and Chicago I would run the file with the zip codes for each respective city as additional arguments like so:

```
python development/utilities/weather.py 10007 90012 60602
```

The script would then ask to input the names of each location IN ORDER. These inputs are then used to update the lexicon.

Let's see this in action:

```
10007 : location {user input}
```

Enter the name of the city

```
10007 : location New York
```

The script repeats this with each of the cities entered, appends them to the lexicon file, then proceeds to pull the data from the API.

**Important!** When the data are first pulled, they will be stored in the following format:

{zip code}.csv.
 
It is important for readability and consistency that these be changed to reflect the natural language name of the city in the following format:

{cityname}_{state id}.csv

For example: New York would initally read out as 10007.csv, but would need to be manually changed to new_york_ny.csv

**Also Important!** Even after following the steps above to retrieve data from the API, your job in still not done yet! These data you just pulled now exist in the data/weather directory as csv files, but in order for any files in the project directory to be able to recognize them when the DS API is deployed online, they need to be inserted into the database. To do this, follow the instructions for using the *insert.py* file below.

---

## **Using the insert.py file**

### Please read before using the insert.py file:)

The *insert.py* file is setup to insert data pulled from the [World Weather Online API](https://www.worldweatheronline.com/developer/) into the project's PostgreSQL database.

### Instructions

#### Packages

Before attempting to use the *insert.py* file, make sure to check you have downloaded the correct version of **psycopg2**.

If not using a virtual environment or if using conda:
```
pip list
```

If using Pipenv

```
pipenv run pip list

python -m pipenv run pip list (if the former does not work)
```

As of the time of this writing the correct version of the package is

```
psycopg2-binary==2.8.5
```

##### Installing Packages from requirements.txt file

If you using a Conda environment, entering

```
conda install --yes --file requirements.txt
```

in command line will ensure that the appropriate version of both packages
are installed on your local machine.

##### Individual Package Installation

If they are not installed and you are not using a virtual environment or are using Conda:
```
pip install psycopg2==2.8.5
```

If the dependencies are already installed, and you are using Pipenv, simply activating the environment should do the trick.

Otherwise enter:

```
pipenv install psycopg2==2.8.5
```

#### Using insert.py

Unlike, the *weather.py* script, *insert.py* takes command-line input after running

```
python developtment/utilities/insert.py
```

as opposed to command-line arguments.

The *insert.py* script also features instructions in the form of input prompts, like the one generated when running the program:

```
    Welcome to the Historical Weather Database Insertion Utility!

    If you would like to insert a city, simply type 'insert' in the prompt
    below, then type the city name and state abbreviation when prompted.

    If you would like to repopulate the database with all the historic data
    found in the data/weather directory, type 'populate'

    If you would like to reset the entire Historic Weather Database, simply
    type 'reset'.

    If you would like to reset only those data for a single city, type
    'reset city', then type the desired city name and state abbreviation
    when prompted.

    If you would like to retrieve data for a specific city, type 'retrieve'.
```

or the prompt shown when typing *'retrieve'*:

```
        Would you like to retrieve the records by city name, or by zipcode?
        For the former, type 'city';
        for the latter, type 'location'.
```

In order to leave the program, type, *'exit'*, *'quit'*, or  *'q'*, but be advised, your command line terminal window may close depending on which terminal you use.

**NOTE:** There is currently no way of directly exiting the program when prompted for a city name, state abbreviation, or location zip code, so if you desire to exit the program without querying the database or altering any of the data therein, simply type an invalid value in both boxes and the built in error messages will prevent the query from being executed.

**Important!**: Please be very, very cautious when using *'populate'*, *'reset'*, and  *'reset city'* commands as they may affect your fellow data scientists and the web development team who may be attempting to call information from the API, and by extension, the database. As an matter of ettiquite, please inform your DS colleagues and, if relevant, the web team, whenever using any of these three commands.

---

## **Using the [db_sentry.py](https://github.com/Lambda-School-Labs/Labs26-Citrics-DS-TeamA/blob/master/development/utilities/db_sentry.py) file**

### Please read before using the db_sentry.py file :)

The `db_sentry.py` file is setup to manage database connections and safely terminate connections in excess.

### Instructions

#### Packages

The `db_sentry.py` file uses the `PostgreSQL` class created in [database.py](https://github.com/Lambda-School-Labs/Labs26-Citrics-DS-TeamA/blob/master/development/utilities/database.py), so make sure to check you have downloaded the correct version of **psycopg2**, as above.

#### Using db_sentry.py

From the repository's root directory, the file will run continuously after entering:

```sh
python development/utilities/db_sentry.py
```

The program will scan the database (specified by the credentials found in the `.env` file) on 5-minute intervals and terminate connections if the number of connections is considered "high" at time of scanning (program considers 20 connections to be a "high" number - AWS RDS Postgres instances degrade over 70 connections). 

**NOTE:** In the `kill_switch` query found in `db_sentry.py`, the IP address passed into `client_addr` must be managed by determing the *"culprit address"*. Extensive use of certain endpoints in the API can lead to a spike in connections. Upon inspection, look for addresses prefixed with `172.31`. These addresses are generated by the Elastic Beanstalk (EB) environment, and can be safely terminated without disrupting user-generated, intentional connections. This culprit address will vary depending on the EB environment, so be sure to check for the appropriate culprit address by examing the database.

#### Examining the Database

Assuming use of a PostgreSQL database (db) instance hosted on AWS RDS, the following query will return a list of active connections to your db instance:

```py
"""
SELECT 
    *
FROM 
    pg_stat_activity
WHERE 
    datname='postgres'
"""
```

For visibility purposes, it is recommended to run this query from a DBMS, such as TablePlus. Upon inspection, look for multiple records sharing a single IP address, and if that shared IP address begins with `172.31`, it is likely your culprit. For further inspection, check the `query` column in the returned output of the query above, and if these same records have no values for `query`, you can indentify this address as your culprit. 

Once identified, replace the IP address in the `client_addr` field of the `kill_switch` query, and proceed to run the program. As long as the appropriate address is entered, the program will run in perpetuity until keyboard-interrupted. 

**NOTE:** For high-usage situations (such as working hours), multiple "sentries" can be deployed by running the `python development/utilities/db_sentry.py` command from multiple terminal tabs/windows. These duplicate instances will not interfere with each other, and if deployed at strategic time intervals, can keep database connections in check with great efficacy. 

---

## **A note on Python imports**

**Important!**

**Please read** before building any new pre-routes in the development directory which use any of the objects or functions in the utilities directory.

**Note:** at the begining of the **weather_pred.py* file in the preroutes directory before all of the other imports, the development directory route has been appended to the system path.

```
import sys
import os

sys.path.append(os.path.join(os.getcwd(), "development"))
```

Without doing so the following import statement would not work.

```
from utilities.database import PostgreSQL
```

Since the above path includes development, one need not add *development* ahead of utilities to the import statement like so:

```
DO NOT USE

from development.utilities.database import PostgreSQL
```

**Note:** When appending a new path to the system, be sure to use *os.path.join()* and *os.getcwd()*. These commands insure that the paths are system agnostic. This is important given that the hardcoded command on Windows would read out as

```
sys.path.append("\path\to\repo\dir\development")
```

whereas, the path on Mac and Linux would read out as

```
sys.path.append("/path/to/repo/dir/development")
```

**Also Note:** All files in either the preroutes or utilities directory are built to be run from the root directory of the repository. This is due to the fact that the *os* library in Python for the whatever directory the terminal is currently operating in when running a *.py* file as opposed to the directory the *.py* file is in.