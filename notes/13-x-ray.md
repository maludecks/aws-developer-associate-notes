# AWS X-Ray
Service that collects data about requests and provides tools you can use to view, filter and gain insights. You can see details about requests, responses and also calls that the application does downstream (other services, databases, etc).

## Exam tips 
* Supports all languages lambda does
* Understand what it is
* SDK: 
  * interceptors to add to code to trace HTTP requests
  * client handlers to instrument AWS SDK clients that your application uses to call other AWS services
  * An HTTP client to use to insturment calls to other internal and external HTTP web services
* Integrates with EBS, Lambda, API Gateway, EC2 and Beanstalk
* Application can be running on EC2, Elastic Beanstalk, ECS and on-premise systems
* To configure X-Ray you'll need: 
  * X-Ray SDK installed
  * X-Ray Daemon installed
  * Instrument the application using the SDK to start sending data to X-Ray
* You can also send metadata (annotations) along with the request data