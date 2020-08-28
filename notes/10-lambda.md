# Lambda
Function as a service, or event-driven compute service (runs your code in response to events). No worries about the infrastructure layer, provisioning, scaling etc.

## Languages
* Node.js
* Java
* Python
* C#
* Go

## Pricing
Per number of requests, 1st million is free, $ 0.20 per million requests. Also on duration, from the time it starts to when it returns.

## Advantages
* No servers
* Continuous scaling
* Cheap

## Versioning
When you create a function, there is only one version: `$LATEST`. If you upload a new version of the lambda, the newer version will become the `$LATEST`. You can create multiple versions of your function and use aliases to reference the version you want to use as part of the `ARN`.

By having multiple versions of a lambda, as a result, you can for instance have a development, beta and production version. You can do versioning through the use of aliases. For example, if you publish a version 1 of the lambda, and create an alias `PROD` that points to version 1, you can use `PROD` to invoke version 1. Now if you want to publish another version, you can re-map `PROD` to point to the new version. If something goes wrong you can rollback and point to version 1 again.

## Concurrent execution limit
There is a security feature which limits the number of functions that can run simultaneously within the same region per account. The error message you get when you reach this limit is `TooManyRequestsException`, and the status code you might get is `429` (`TooManyRequests`/Throttling). You can have `reserved concurrency` in order to set priority for specific critical functions and guarantee that they wil always run.

## Exam tips
* Default timeout is 3 seconds
* Maximum timeout is 900 seconds (15 minutes)
* Lambda scales out (not up) automatically 
* Lambda functions are independent, 1 event = 1 function
* Lambda is a compute service 
* Lambda is serverless
* Remember all services which are serverless
* Lambda functions can trigger other lambdas (1 event can = several functions being triggered)
* Use AWS X-Ray to debug lambda architectures 
* Lambda work globally (not region specific)
* Know all lambda triggers (API Gateway, AWS IoT, Alexa Skills Kit, Alexa Smart Home, Cloudfront, Cloudwatch Events, Cloudwatch Logs, CodeCommit, Cognito Sync Trigger, DynamoDB, Kinesis, S3 and SNS)
* Each lambda has its own unique ARN (immutable)
* Qualified ARN has the version, unqualified doesn't
* If you use an unqualified name (without a version or `$LATEST` in the ARN), the lambda will point to the `$LATEST` by default
* Use version alias for versioning 
* You can split traffic between 1 or 2 versions of a lambda (but not from `$LATEST`)
* Know the supported languages 
* By default, a lambda function will not be able to access any resources within a private subnet. You'll have to add VPC information to your lambda config using the `--vpc-config` parameter
* To configure access to private resources you need to
  * Configure the lambda function to connect to the private subnets
  * Configure lambda's security group
  * Configure lambda's execution role to have permissions for managing an ENI (Elastic Network Interface) within the VPC