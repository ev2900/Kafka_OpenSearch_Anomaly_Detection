# Kafka OpenSearch Anomaly Detection Demo

## Architecture

## Instructions

1. Launch CloudFormation stack

    [![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=open-search-demo-vpc&templateURL=https://sharkech-public.s3.amazonaws.com/misc-public/OpenSearch_demo_VPC.yaml)

2. Update msk security group to allow inbound traffic from Cloud9 security group

    - Navigate to [Security Group](https://us-east-1.console.aws.amazon.com/vpc/home?region=us-east-1#securityGroups:) page in the AWS console
    - Select ```msk security group```
    - Add inbound bound rule allowing all traffic from the aws-cloud9 security group

3. Create Kafka topic

    - Navigate to [Cloud9](https://us-east-1.console.aws.amazon.com/cloud9/home?region=us-east-1#) page in the AWS console
    - Open IDE for the msk-workshop-cloud9 enviorment
    - Follow the instructions in [Kafka/1_create_topic.py](https://github.com/ev2900/Kafka_OpenSearch_Anomaly_Detection/blob/main/Kafka/1_create_topic.py)

4. Create OpenSearch index

    - via. Cloud9 update the required section(s) and run [OpenSearch/1_create_index.py](https://github.com/ev2900/Kafka_OpenSearch_Anomaly_Detection/blob/main/OpenSearch/1_create_index.py)

5. Configure Lambda

    - Navigate to [lambda](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions/msk-os-lambda?tab=code) function page in the AWS console

    - Add MSK trigger to the Lambda
        - MSK cluster = ```msk-cluster-workshop```
        - Batch size = ```100```
        - Batch window = ```15```
        - Topic name = ```ApplicationMetricTopic```
        - Starting position = ```Latest```   
    
    - Update the ```os_url``` variable in the lambda code with the domain endpoint of the OpenSearch cluster deployed by the CloudFormation stack  

6. Send data to OpenSearch 

    - Navigate to [Cloud9](https://us-east-1.console.aws.amazon.com/cloud9/home?region=us-east-1#) page in the AWS console

    - Send base data via. Cloud9. Update the required section(s) and run [Kafka/2_base_data.py](https://github.com/ev2900/Kafka_OpenSearch_Anomaly_Detection/blob/main/Kafka/2_base_data.py)

    - Send anomoly data via. Cloud9. Update the required section(s) and run [Kafka/3_anomoly_data.py](https://github.com/ev2900/https://github.com/ev2900/Kafka_OpenSearch_Anomaly_Detection/blob/main/Kafka/3_anomoly_data.py)

7. Create + run OpenSearch anomaly detector

    - via. Cloud9 update the required section(s) and run [OpenSearch/2_create_anomoly_detector.py](https://github.com/ev2900/Kafka_OpenSearch_Anomaly_Detection/blob/main/OpenSearch/2_create_anomoly_detector.py)
