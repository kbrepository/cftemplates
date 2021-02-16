## The main objective is to be able to launch HIPAA compliant architecture with dynamic OS and DB.
## As of now, the CloudFormation template are created considering Amazon Linux 2 OS and Maria DB Database engine.

## This folder comprises of CloudFormation templates which are derived from AWS.
## The templates are modified with the purpose of making the infrastructure deployment dynamic.
## The classic load balancer has been replaced by application load balancer.
## ACM certificate has been added to the application template for end-to-end secure encryption.

## Reference:
## Reference Architecture for HIPAA on AWS - https://aws.amazon.com/quickstart/architecture/compliance-hipaa/


ARCHITECTURE FLOW

1.	Master template will trigger nested template to create different components.
2.	IAM template will be triggered to create IAM resources.
3.	Logging template will be triggered to create CloudTrail, S3 buckets for CloudTrail and CloudWatch alarms, SNS.
4.	Production Vpc template will be triggered to create network environment that provides a standard public facing application, separates private-public subnets and enforce traffic with NACL rules.
5.	Management Vpc template will be triggered to create network environment for a standard management Vpc and a nested template will be triggered to create a bastion server.
NOTE: Management template will be triggered on successful execution of Step 4.

6.	Application template will be triggered to deploy a web application with reverse proxy, Application Load Balancers, Auto Scaling., etc.
NOTE: This template will be triggered on successful execution of step 2, 3, 4 and 5.

7.	Config Rule template will be triggered to set up AWS Config Rules.
NOTE: This template is optional.

