+++
authors = []
date = 2020-04-07T22:00:00Z
draft = true
excerpt = "DynamoDB migration"
hero = ""
timeToRead = 5
title = "Cross Account Dynnamodb Migration      "

+++
This article describes a solution used for migrating an application using DynamoDB from one account to another aws account. Application migrated is an API. Application was running on aws ec2 with auto scaling, and used Dynamodb as the database. According to a organization wide initiative to migrate all services in to kubernetes cluster was created in a new aws account.The end goal is to have the application, including all of its components, running in a Kubernetes cluster with the DynamoDB instance in a different AWS account.

Migration effort was complicated by the requirement to have the migration done without any downtime, there were lot of articles about doing a dynamodb migration with a downtime. Also there are multiple tools available to take a backup of dynamodb table and restore it to another table. But there wasn't much information on doing a migration without  application downtime.