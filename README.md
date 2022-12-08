# Serverless_Framework_Athena_Glue_Deployment_on_existing_S3_Bucket

## Description
AWS Athena, Glue Database, Glue Crawler deployment on existing S3 bucket through Serverless (sls) Framework.

## Overview
Serverless is a cloud-native development model that allows developers to build and run applications without having to manage servers. There are still servers in serverless, but they are abstracted away from app development.
Or you can say Serverless is an application delivery model where cloud providers automatically intercept user requests and computing events to dynamically allocate and scale compute resources, allowing you to run applications without having to provision, configure, manage, or maintain server infrastructure.

## Serverless Framework
Develop, deploy, troubleshoot, and secure your serverless applications with radically less overhead and cost by using the Serverless Framework. The Serverless Framework consists of an open-source CLI and a hosted dashboard. Together, they provide you with full serverless application lifecycle management.

Setting Up the Serverless Framework with AWS

## Step - 1
Login to your AWS account, go to IAM (Identity and Access Management) console


Click “Users” from left navigation panel and click on “Add users” button


Add user name and check box “Access key - Programmatic access” and click “Next Permissions” button


Click on “Attach existing policies directly”, check box “AdministratorAccess” and click on “Next: Tags” button


Add Key, Value as required and click on “Next: Review” button


Click on “Create user” button to create user.


Finally download .csv credentials file and secure it so no one have access and click on “Close” button


Your ServerlessUser created.

## Step - 2
Login to your linux server to configure serverless. Before installing serverless you need to install nodejs package if it’s already installed then you can proceed with serverless installation otherwise you can install through given commands.


apt update


curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -


apt install -y nodejs


Check install version
node -v

npm -v


Following command install the serverless package
npm install -g serverless


To setup Serverless with AWS run the following command
serverless config credentials --provider aws --key your-account-key --secret your-account-secret --profile ServerlessUser


Use the credentials of the user you created in first step

## Step - 3
Now we have to create our first project to deploy our resources on AWS for that we can do it by two ways as
Create a project directory with command
mkdir athena-project


cd athena-project


sls create --template aws-nodejs


Command will create three files in your project directory in which serverless.yml is the main file you can edit and configure for your project resources.


Run the following command directly create your project with directory and all files as
sls create --template aws-nodejs --path athena-project


Go into the project directory and check
cd athena-project
ls


## Step - 4
Basic serverless.yml file look like this which you have to edit with your project code. To view it run command.


cat serverless.yml


Now open your file in your favorite editor Vim or Nano to edit it, and run the following command.

vim serverless.yml
OR
nano serverless.yml

As you can see serverless defines the service with our project name, selecting AWS provider, where we are defining our profile which we created at the time of credentials configuration, and defining the environment with the AWS region where we want to deploy resources.

We are also defining the custom resources of already existing S3 buckets with their paths which we are using in the glue crawler and Athena workgroup.

Finally, we are creating a simple SQL query with Athena workgroup where we are providing a glue database with a glue table created by a glue crawler with an S3 bucket data directory name.


## Step - 5
Now we need to deploy our project through command

sls deploy


Further you can check on AWS CloudFormation console to verify.


## Step - 6
Finally you can cleanup your resources to avoid any extra charges

sls remove
