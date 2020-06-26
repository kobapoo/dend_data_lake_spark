# Project 4: Data Lake & Spark

<p align="center"><img src="images/logo.png" style="height: 100%; width: 100%; max-width: 200px" /></p>

## Introduction
As a data engineer, I was responsible for developing a data lake for the analytics team at Sparkify. After considerable growth in user base and song database it was time to move the data warehouse to a data lake and enhance data processing through Spark.

### Achievements
As their data engineer, I was responsible for building out an ETL pipeline, extracting data from S3 buckets, processing it through Spark and transforming into a star schema stored in S3 buckets with parquet formatting and efficient partitioning. The database and ETL pipeline were validated by running queries provided by the analytics team and compared expected results.
Skills include:
* Building out an ETL pipeline using Spark, Python, Hadoop Clusters (EMR).
* Fast-tracking the data lake buildout using (serverless) AWS Lambda and cataloging tables with an AWS Glue Crawler
* Setting up IAM Roles, Hadoop Clusters, EMR,  Config files and security groups.
* Scaling up the data analysis process through the use of a data lake and Spark, in order to further optimize queries on song play analysis

# Run The Scripts
The primary file in this repo is the `etl.py`, which will read in files from S3 buckets, process them using Spark and store them as parquet files in S3 buckets, partitioned appropriately.

# Available Data
### Song Dataset
The first dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```
And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```
### Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from a music streaming app based on specified configurations.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.

```
log_data/2018/11/2018-11-12-events.json

```

# Schema for Song Play Analysis
Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.



#### Fact Table
1. songplays - records in log data associated with song plays i.e. records with page `NextSong`
    * songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### Dimension Tables
2. <b>users</b> - users in the app
    * user_id, first_name, last_name, gender, level
3. <b>songs</b> - songs in music database
    * song_id, title, artist_id, year, duration
4. <b>artists</b> - artists in music database
    * artist_id, name, location, lattitude, longitude
5. <b>time</b> - timestamps of records in <b>songplays</b> broken  down into specific units
    * start_time, hour, day, week, month, year, weekday
