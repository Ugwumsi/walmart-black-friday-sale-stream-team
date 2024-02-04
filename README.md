# walmart-black-friday-sale-stream-team


## Architecture:

![Architecture_Black_Friday_Sale_Walmart](https://github.com/Ugwumsi/walmart-black-friday-sale-stream-team/assets/81196037/147c7aee-c4da-4b63-8e13-677185f4147e)


## Detailed explanation:

*1. Producer Code:*

Created Lambda function. 
We have used library fake and random_timestamp so we have created zip file including lambda_function.
Created random data for Inventory Update data.
We have used product_id, timestamp, quantity_change, store_id from Inventory Update data because these data are relatable for example quantity change from Inventory update is -2 so quantity in Sales Transaction will be 2.
Created Sales Transaction data.
Send message to AWS SQS Inventory-Updates-Stream & Sales-Transactions-Stream respectively.
To make it near real time, we have used AWS Event Bridge Scheduler to orchestrate every 15 minutes.

*2. Consumer Code:*

Created AWS S3 Bucket and 2 objects one for Sales Transactions and other for Inventory Updates.
Used AWS SQS feature Triggers Lambda automatically whenever there is message in message queue. 
So, 2 lambda functions for Consumer Code as there are 2 SQS service.
Created Lambda Function.
As data coming batch, used for loop.
Read message body in each loop and save it in list.
At the end of loop, created pandas dataframe.
Save pandas dataframe in csv file to AWS S3 object.

*3. Data warehousing*

Created AWS Redshift Cluster.
Created Schema and 4 tables schema.
Use COPY command to load data from S3 to Redshift with JOB CREATE <job-name> AUTO ON at the end of this command.
Loaded dim table data directly using python or through lambda function for one time.
Created Materialized View for various metrics.

*4. Dashboard*

Used AWS Quick Insight from Materialized View tables which we created from 2 fact and 2 dim tables.

This is just crux of what we have mentioned. 
Created user group and added user group with 3 users and added policies in user group.
Created role for different service and added policies.

Team Name: Stream Team

Team Members: 

Rahul Gangwani (rahulgangwani729@gmail.com)
Ugwumsi (eugwumsi@gmail.com)
Satwik (satwikkmr188@gmail.com)
