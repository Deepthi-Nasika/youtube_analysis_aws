## Youtube Video Popularity - Data Engineering and Analysis with AWS Services
### Overview
If a business wants to run an advertising campaign on YouTube, the business has to know certain metrics that make the YouTube video popular. To understand the categories of videos that are currently trending, the role of performance metrics, and user interactions in the video popularity we have to perform an analysis of the current trending YouTube video statistics.

### Goal
The main goal of this project is to streamline the structured, and semi-structured data from the Kaggle dataset into a proper standard format securely. To store large amounts of data, manage, and perform the analysis we need to use the cloud - to handle all the cases efficiently AWS services are used in this project. Dashboards are built to analyze the trending metrics for the video popularity on YouTube concerning regions.

### Dataset
The dataset is a daily record of the top 200 trending YouTube videos for certain months in multiple regions. Every region's data is stored in separate files with different ```category_id```. It includes multiple metrics like video title, channel title, tags, views, comment count, likes, and dislikes. All the attributes related to a specific video are stored in JSON files respective to each region. \
Link: https://www.kaggle.com/datasets/datasnaek/youtube-new

### Steps
1) Data Ingestion - Ingest the data from multiple sources into an S3 bucket\
   - Load JSON data files using shell command:\
```aws s3 cp . s3://s3_bucket_name/youtube/raw_stats_json/ --recursive --exclude "*" --include "*.json"```\
   - Load CSV data files w.r.t. regions using shell command:\
           For example, to load CAvideos.csv file ```aws s3 cp CAvideos.csv s3://s3_bucket_name/youtube/raw_stats/region=ca/```
3) Data Catalog - Crawlers are created to crawl through the JSON and CSV file data from the S3 bucket and creates data catalog tables on top of it
4) ETL(Data Preprocessing) 
   - Lambda function to convert ```JSON -> Apache Parquet```
   - Glue job to convert ```CSV -> Apache Parquet```
5) A trigger is added to the lambda function for its execution whenever the new data is being loaded to the S3 bucket. The crawlers are executed on the cleaned versions of parquet formatted data.
6) A table ```youtube_analytics``` is created to join both json_parquet_data and csv_parquet_data into a single table and store it in a separate S3 location
7) Analytical Dashboard are built in Amazon QuickSight using the table ```youtube_analytics```

### AWS Services
1) Amazon S3(Simple Storage Service) - It is an object storage service that stores large amounts of data with scalability, availability, security, and efficient performance
2) AWS IAM(Identity Access and Management) - It is a service that helps you securely control access to AWS resources.
3) AWS Glue - It is a serverless data integration service to create, manage, and monitor high-quality data across data lakes and pipelines for analysis, machine learning, and application development.
4) AWS Lambda - It is a serverless computing service that runs code in response to events
5) AWS Athena - It is an interactive query service that makes it simple to analyze data directly in Amazon S3
6) Amazon QuickSight - It is a business intelligence service that helps in building visualizations and performing analysis

### Analysis Dashboards
- Number of Likes grouped by Genre: [no_of_likes_by_genre.pdf](https://github.com/user-attachments/files/16631101/no_of_likes_by_genre.pdf)
- Number of Views grouped by Genre: [no_of_views_by_genre.pdf](https://github.com/user-attachments/files/16631103/no_of_views_by_genre.pdf)
