# aws_covid_pipeline
# COVID ETL Pipeline using Amazon S3, Crawler, Dimension Models, Data Models, Amazon Athena, and AWS Glue
This project creates an ETL pipeline to process COVID-19 data and store it in Amazon Redshift for further analysis. The pipeline consists of six AWS services: Amazon S3, Crawler, Amazon Athena, and AWS Glue.
Dimension Models and Data Models are made using draw.io
 
<img width="1226" alt="Screenshot 2023-03-24 at 12 30 57" src="https://user-images.githubusercontent.com/103274172/227521857-daa1a5ff-8722-4b59-b74d-c9757ee7e443.png">

# Architecture
The ETL pipeline follows the following architecture:

- Data Ingestion: The COVID-19 data is collected from various sources and stored in Amazon S3.

- Data Crawling: AWS Crawler is used to automatically discover and infer the schema of the data stored in S3.

- Data Transformation: AWS Glue is used to transform the data using PySpark scripts that clean, filter, and aggregate the data as per the desired output format.

- Dimension Modeling: A Dimensional Model is used to create a star schema that organizes data into dimensions and facts. This model helps in efficient querying of the data.

- Data Modeling: A Data Model is created to map the data from the source to the Dimensional Model. This model helps in data mapping and transformation.

- Data Storage: The transformed data is stored in Amazon Redshift.

- Data Querying: Amazon Athena is used to query the transformed data stored in S3 and generate insights on COVID-19 data.

# COVID ETL Pipeline Architecture

## Data Ingestion
COVID-19 data is collected from our [data source -aws Data Lake](https://aws.amazon.com/covid-19-data-lake/) and stored in Amazon S3 in CSV format. The data includes information on cases, deaths, and vaccinations for each country and state. The data is updated daily, and new data is added to the S3 bucket.

## Data Crawling
AWS Crawler is used to automatically discover and infer the schema of the data stored in S3. The Crawler scans the S3 bucket for new data and creates tables in the AWS Glue Data Catalog. The Data Catalog is used to manage metadata for the data stored in S3.

## Data Transformation
AWS Glue is used to transform the data using Python scripts. The scripts clean, filter, and aggregate the data to generate insights on COVID-19 data.

## Data Modeling
A Data Model is created to map the data from the source to the Dimensional Model. This model helps in data mapping and transformation. The Data Model includes mapping rules that transform the source data into the desired output format for the Dimensional Model.

  <img width="320" alt="Screenshot 2023-03-24 at 12 27 23" src="https://user-images.githubusercontent.com/103274172/227521526-b186fea0-b540-4ef5-b649-383103022091.png"> 

## Dimension Modeling
A Dimensional Model is used to create a star schema that organizes data into dimensions and facts. This model helps in efficient querying of the data. The dimensions include date, location, and COVID-19 metrics such as cases, deaths, and vaccinations.
<img width="858" alt="Screenshot 2023-03-24 at 12 26 46" src="https://user-images.githubusercontent.com/103274172/227521643-3829d754-67e6-4c7b-b9f7-5a3d82c1d321.png">

Data Storage
The transformed data is stored in Amazon Redshift for efficient querying and analysis of the data.

Data Querying
Amazon Athena is used to query the transformed data stored in S3. Athena provides an SQL interface to query the data and generate insights on COVID-19 data. The insights can be used to track the spread of COVID-19, identify trends, and make data-driven decisions.
```response = athena_client.start_query_execution (
    QueryString="SELECT * FROM uscounty",
    QueryExecutionContext={"Database": SCHEMA_NAME},
    ResultConfiguration={
        "OutputLocation": S3_STAGING_DIR,
        "EncryptionConfiguration": {"EncryptionOption": "SSE_S3"},
    },
)
uscounty = download_and_load_query_results(athena_client, response)
```

Conclusion
This COVID ETL pipeline provides a scalable and efficient way to process and analyze COVID-19 data. It leverages the power of AWS services to handle large volume of data.
