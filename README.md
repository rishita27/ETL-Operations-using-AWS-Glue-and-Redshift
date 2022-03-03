# ETL-Operations-using-AWS-Glue-and-Redshift

Used AWS Glue to perform ETL operations and load resultant data to AWS Redshift service. In the second phase of the demo, used AWS CloudWatch rules and LAMBDA function to automatically run **GLUE Jobs** to load data to Data Warehouse **(AWS Redshift).**

## Architecture-1
![image](https://github.com/ManjinderSingh3/ETL-Operations-using-AWS-Glue-and-Redshift/blob/master/Architecture/Glue_1.png)

### Explanation:
* Load dataset to S3 bucket 
* Create a Connection between Glue and Redshift which will be used while configuring Crawler at redshift side.
* Create a Crawler at Source side which will fetch data from source i.e, S3 Bucket.
* Create a temporary database so that whenever crawler job is executed, crawler fetches data from S3 and store in this temporary DB. This step is executed while creating Crawler.
* Create a Crawler at Destination side using the connection built at second step. A temporary DB will also be created
* Execute Glue Job to push data to Redshift

## Architecture-2
![image](https://github.com/ManjinderSingh3/ETL-Operations-using-AWS-Glue-and-Redshift/blob/master/Architecture/Glue_2.png)

### Explanation :
* Load Data to S3 Bucket
* Cloud watch rule will keep an eye on Source side crawler. Whenever crawler fetches data from source than Event Bridge (rule) will trigger the Lambda function which will in result execute the Glue Job to Load data at Redshift.
* CloudWatch rule triggers the LAMBDA function which will than execute the Glue Job to automatically Load data to Redshift.
