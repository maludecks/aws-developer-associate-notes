## CLI Pagination
Control the number of items included in the output when using the CLI. By default it's 1K items. You can use `--page-size` to request a smaller number of items. The CLI still retrieves the full list of items, but performs a larger number of smaller API calls in the background. Setting a page size is not the same as setting a maximum/limit of items. If you see errors related to `timeout` or `too many results` in the CLI, you might want to adjust the `--page-size` to reduce the size of each API call

## Additional resources
* Checkout the [FAQs](https://aws.amazon.com/faqs/)
  * Serverless: Lambda, API Gateway, DynamoDB, Elasticache and S3
  * Dev Tools: CodeCommit, CodePipeline, CodeDeploy and CodeBuild
  * Security: IAM, Cognito and KMS
  * Automation & Monitoring: ElasticBeanstalk, CloudFormation, CloudWatch and X-Ray
  * Containers: ECS and ECR
  * Messaging & Streaming: SQS and Kinesis
* Checkout the [whitepapers](https://aws.amazon.com/whitepapers/) 
  * [Architecting for the Cloud: Best practices](https://d1.awsstatic.com/whitepapers/AWS_Cloud_Best_Practices.pdf)
  * [Practicing CI/CD on AWS](https://d1.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf)
  * [Blue/Green deployments on AWS](https://d1.awsstatic.com/whitepapers/AWS_Blue_Green_Deployments.pdf)
  * [Introduction to DevOps on AWS](https://d1.awsstatic.com/whitepapers/AWS_DevOps.pdf)
  * [Running containerized microservices on AWS](https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf)
  * [Docker on AWS: Running Containers in the Cloud](https://d1.awsstatic.com/whitepapers/docker-on-aws.pdf)
  * [AWS Security Best Practices](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
  * [Serverless Architecture with Lambda](https://d1.awsstatic.com/whitepapers/serverless-architectures-with-aws-lambda.pdf)
  * [Optimizing Enterprise economics with Serverless Architecture](https://d1.awsstatic.com/whitepapers/optimizing-enterprise-economics-serverless-architectures.pdf)
  * 
* re:Invent videos
  * [Become an IAM Policy Master in 60 Minutes or Less](https://www.youtube.com/watch?v=YQsK4MtsELU&t=2s)
  * [Continuous Integration Best Practice](https://www.youtube.com/watch?v=77HvSGyBVdU&t=2638s)
  * [Getting started with Docker on AWS](https://www.youtube.com/watch?v=mUzsYt3Bj08)
  * [Serverless Architectural Patterns and Best Practices](https://www.youtube.com/watch?v=Xi_WrinvTnM)
  * [Your Virtual Data Center: VPC Fundamentals and Connectivity Options](https://www.youtube.com/watch?v=jZAvKgqlrjY)
  * [Moving to DevOps the Amazon Way](https://www.youtube.com/watch?v=Pvb74TlV8SA&t=3075s)