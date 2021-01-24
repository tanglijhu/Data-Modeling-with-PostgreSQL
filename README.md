# Data-Modeling-with-PostgreSQL

# Table of Contents
<!--ts-->
- [Project Summary](#project-summary)
  * [Dataset Description](#dataset-description)
  * [Python Script Description](#python-script-description)
- [Database Schema](#database-schema)
- [ETL Pipeline Details](#etl-pipeline-details)
  * [song_data ETL](#song_data-etl)
  * [log_data ETL ](#log_data-etl)
 - [Usage Precedure](#usage-precedure) 
<!--te-->  

## Project Summary 

The objective of this project is to create a SQL analytics database for a fictional music streaming service compacy called Sparkify. Sparkify's analytics team is interested 
in understanding what, when and how their users are playing songs on their app. The analysts need to figure out a way to query and analyze the data easily, which
is currently locally stored in raw JSON logs on user activity on the app and a directory with JSON metadata on the songs in their app.

The data engineers's task is to 1) create a database schema, 2) to upload the locally stored data into a PostgreSQL database, and 3) to implement an ELT pipeline using Python.  

### Dataset Description 

* Song dataset: all json files in subdirectories under /data/song_data
* Log dataset: all json files in subdirectories under /data/log_data 

### Python Script Description

* create_tables.py: clean previous schema and create tables 
* sql_queries.py: all queries used in the ETL pipeline 
* etl.py: read JSON logs and JSON metadata and load the data into the tables created by implementing "create_tables.py"

## Database Schema

The schema used for this task is the Star Schema.

One main fact table containing all the measures associated with each event - songplays, and 4-dimentional tables - songs, artists, users, and time. In each of the 4-dimentional 
tables, a primary key can be referenced from the fact table. 

![database schema diagram](/img/database-schema.PNG)

The reasons to use a relational databse for this task are: 
* the data types are structured 
* the amount of data to analyze is not too big 
* the structure enables the analysts to aggregate the data efficiently 

## ETL Pipeline Details 

In general, data can be extracted from two locally stored JSON source files: song_data and log_data. The JSON files are read into pandas dataframes, processed and uploaded into the database using psycopg2.

### song_data ETL 

#### dataset source

Example of a file path for song_data: song_data/A/B/C/TRABCEI128F424C983.json 

Each file in JSON format contains metadata about a song and the artist information 

#### final PostgreSQL tables 

* songs: song_id, title, artist_id, year, duration 
* artist: artist_id, name, location, latitude, longitude 

### log_data ETL 

#### dataset source

Example of a file path for log_data: log_data/2018/11/2018-11-12-events.json 

Each file in JSON format contains metadata about log information partitioned by year and month 

#### final PostgreSQL tables 

* time: start_time, hour, day, week of year, month, year, and weekday (note: extracted from the 'ts' field)  
* users: user_id, first_name, last_name, gender, level (note: update level field is duplicated user information is delivered)
* songplays: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

## Usage Precedure 

1) From terminal, run "create_tables.py" to drop the previous tables and set up the database / tables;
2) Run "etl.py" to process and load data into the database / tables; 
3) Run "test.ipynb" to validate and example queries.


