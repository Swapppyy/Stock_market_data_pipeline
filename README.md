# Stock Market Data pipeline using Airflow, Spark, Postgres and Metabase

What is this pipeline exactly doing?

1. Extracting data from Yahoo finance API.
2. Storing the raw data into an Minio bucket using Airflow.
3. Transforming the data for Analytics using PySpark (which runs seperately on the docker container).
4. Load the transformed data into Postgres for analytics.
5. Using Metabase as a service through Docker for analytics.

## Architecture
![stock-market-data-pipeline.jpg](stock-market-data-pipeline.jpg)
1. **Reddit API**: Source of the data.
2. **Apache Airflow & Celery**: Orchestrates the ETL process and manages task distribution.
3. **PostgreSQL**: Temporary storage and metadata management.
4. **Amazon S3**: Raw data storage.
5. **AWS Glue**: Data cataloging and ETL jobs.
6. **Amazon Athena**: SQL-based data transformation.
7. **Amazon Redshift**: Data warehousing and analytics.

## Prerequisites
- AWS Account with appropriate permissions for S3, Glue, Athena, and Redshift.
- Reddit API credentials.
- Docker Installation
- Python 3.9 or higher

## System Setup
1. Clone the repository.
   ```bash
    git clone https://github.com/Swapppyy/Reddit_ETL_Pipleline.git
   ```
2. Create a virtual environment.
   ```bash
    python3 OR python -m venv venv
   ```
3. Activate the virtual environment. (Below is for Windows OS)
   ```bash
    source venv/bin/activate
   ```
4. Install the dependencies.
   ```bash
    pip install -r requirements.txt
   ```
5. Rename the configuration file to config.conf in the config folder and update the credentials for your system.
   ```bash
    git mv config.conf.example config.conf
   ```
6. Starting the containers
   ```bash
    docker-compose build --no-cache
    docker-compose up airflow-init
    docker-compose up -d
   ```
7. Launch the Airflow web UI and run the etl_DAG to extract data from Reddit API and push it to the S3 Bucket.
   ```bash
    open http://localhost:8080
   ```
