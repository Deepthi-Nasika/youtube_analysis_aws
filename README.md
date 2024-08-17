## Youtube Video Popularity - Data Engineering and Analysis with AWS Services
### Overview
If a business wants to run an advertising campaign on YouTube, the business has to know certain metrics that make the YouTube video popular. To understand the categories of videos that are currently trending, the role of performance metrics, and user interactions in the video popularity we have to perform an analysis of the current trending YouTube video statistics.

### Goal
The main goal of this project is to streamline the structured, and semi-structured data from the Kaggle dataset into a proper standard format securely. To store large amounts of data, manage, and perform the analysis we need to use the cloud - to handle all the cases efficiently AWS services are used in this project. Dashboards are built to analyze the trending metrics for the video popularity on YouTube concerning regions.

### Dataset
1) The dataset is a daily record of the top 200 trending YouTube videos for certain months in multiple regions.
2) Every region's data is stored in separate files with different ```category_id```. It includes multiple metrics like video title, channel title, tags, views, comment count, likes, and dislikes.
3) All the attributes related to a specific video are stored in JSON files respective to each region. \
4) Link: https://www.kaggle.com/datasets/datasnaek/youtube-new

### Steps
#### Data Ingestion
Ingest the data from multiple sources into an S3 bucket
1) Load JSON data files using shell command:\
```aws s3 cp . s3://s3_bucket_name/youtube/raw_stats_json/ --recursive --exclude "*" --include "*.json"```\
2) Load CSV data files w.r.t. regions using shell command:\
For example, to load CAvideos.csv file ```aws s3 cp CAvideos.csv s3://s3_bucket_name/youtube/raw_stats/region=ca/```

#### Data Lake

### AWS Services
1) Data Storage - AWS S3 Bucket
2) Glue Jobs - Crawlers
3) AWS Lambda Function
4) SQL Query - AWS Athena
5) Analysis - AWS Quicksight

### Analysis Dashboards
#### Number of Likes grouped by Genre
[no_of_likes_by_genre.pdf](https://github.com/user-attachments/files/16631101/no_of_likes_by_genre.pdf)
#### Number of Views grouped by Genre
[no_of_views_by_genre.pdf](https://github.com/user-attachments/files/16631103/no_of_views_by_genre.pdf)
