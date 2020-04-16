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

Migration effort was complicated by the requirement to have the migration done without any downtime, there were lot of articles about doing a dynamodb migration with a downtime. Also there are multiple tools available to take a backup of dynamodb table and restore it to another table. But there wasn't much information on doing a migration without  application downtime. But since the application only needed to retain 3 weeks of data backup and restore part was not required at all.

Existing dynamodb replication solutions like [dynamodb-replicator](https://github.com/mapbox/dynamodb-replicator), [dynamodb-cross-region-library](https://github.com/awslabs/dynamodb-cross-region-library) were evaluated. Since those could not be used for our requirement we came up with multiple options and these solutions were evaluated to find out the best option.

Options considered:

1. writing to dynamodb tables in both accounts
2. split read/writes across accounts while cross account replication is being done.
3. Only implement cross account replication from old account to new.
4. Use multiple application deployments with cross account replication.

We ended up using the 4th option because it provided a way to migrate without any downtime without having to meddle with application code a lot. 