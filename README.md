# Data-Modeling-with-PostgreSQL

This project consists of three following parts: 
* Data modeling with Postgres
* Database star schema created 
* ETL pipeline using Python

## Project Summary 

The objective of this project is to create a SQL analytics database for a fictional music streaming service compacy called Sparkify. Sparkify's analytics team would like to 
understand what, when and how their users are playing songs on their app. The analysts need to figure out a way to query and analyze the data easily, which
is currently locally stored in raw JSON logs on user activity on the app and a directory with JSON metadata on the songs in their app.

The data engineers's task is to create a database schema and upload the locally stored data into a PostgreSQL databse as well as to implement an ELT pipeline.  

### Data Description 

* Song databset: all json files in subdirectories under /data/song_data
* Log dataset: all json files in subdirectories under /data/log_data 

## Database Schema

The schema used for this task is the Star Schema.

One main fact table containing all the measures associated with each event - songplays, and 4-dimentional tables - songs, artists, users, and time. In each of the 4-dimentional 
tables, a primary key can be referenced from the fact table. 

![database schema diagram](/img/database-schema.PNG)

The reasons to use a relational databse for this task are: 
* the data types are structured 
* the amount of data to analyze is not too big 
* the structure enables the analysts to aggregate the data efficiently 

## 
