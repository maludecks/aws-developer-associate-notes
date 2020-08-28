# SAM
Serverless Application Model (SAM) is an extension to CloudFormation used to define serverless applications specifically. It provides a simplified syntax for defining serverless resources (APIs, Lambda functions, DynamoDB tables, etc). SAM also has it's own CLI that can be used to package deployment code, upload builds to S3 and deploy serverless applications.

## CLI commands
* `sam package`
    * Packages your application
    * Uploads deployment files to S3
    * Takes a YAML template as input
    * Outputs a SAM compatible template
    * Uploads a deployment package to a specified S3 bucket 
* `sam deploy`
    * Deploys your serverless application using CloudFormation
    * Takes as input a SAM template, the name of the CloudFormation stack and an IAM capability

## Exam tips
* Know what it is
* Remember the 2 commands