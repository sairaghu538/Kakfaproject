Step 1 : Create RDS Database
      a. SQL Server Standard Edition
      b. In the security group allow TCP traffic from all sources on port 1433
Step 2 : Create Database, table , enable CDC on table and insert the data into table
      a. execute the scripts given under database/cdc_script.sql
Step 3 : Create S3 Bucket , and Setup S3 VPC endpoint
      a. When creating endpoint choose type "Gateway" and service name "com.amazonaws.us-east-1.s3" (change region according to your bucket)
Step 3: Create MSK Cluster
      a. Cluster type : Provisioned
      b. Security group : allow inbound and outbound traffic from everywhere (you can keep it more restricted to allow only from required sources)
      c. Authentication type : IAM 
Step 4: Create an IAM Role for MSK with the policy given in Repo
      a. IAM policy details given here : IAM/MSKConnectorRole.json
Step 5: Create connector plugins for SQL Server Source and S3 Sink
      a. Debezium Connector for SQL Server : https://www.confluent.io/hub/debezium/debezium-connector-sqlserver
      b. Kafka-S3-Sink Connector: https://www.confluent.io/hub/confluentinc/kafka-connect-s3
Step 6: Create the source connector
      follow the steps explained in the video to create the source connector 
Step 7: Create and EC2 instance (This step is optional , we are doing this to just to view the data in Kafka topic)
      a. Create EC2 instance
      b. Create EC2 service role with IAM permissions given here : IAM/ecRole.json
Step 8: Verify the data in topic (This step is optional , we are doing this to just to view the data in Kafka topic)
      a. Install Kafka by using the commands given here : kafka/kafka_commands.txt
      b. Use the console consumer command (#7 in above file) to view the data in topic
Step 9: Create S3 Sink Connector
      follow the steps explained in the video to create the Sink connector 
Step 10: Verify the data in target S3 Bucket