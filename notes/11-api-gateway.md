# API Gateway
"Front door" for applications. Expose HTTPS endpoints to define RESTful APIs.

## What it does
* Expose HTTPS endpoints 
* Serverless-ly connect to services like lambdas and dynamoDB
* Send each API endpoint to a different target
* Efficient with very low cost 
* Scales easily
* Track and control using API keys
* Throttle requests to prevent attacks 
* Mantain multiple versions of an API

## Configuration 
* Define an API (container)
* Define resources and nested resources (URL paths)
* For each resource
  * Select supported HTTP methods
  * Set security
  * Choose targets (EC2, Lambda, DynamoDB, S3, etc)
  * Set request and response transformations 
* Deploy to a stage
  * Use API Gateway domain (default) or custom

## API Caching
Can be enabled to cache API Gateway endpoint's response. With caching you reduce the number of calls to the resource and also improve latency.

### Same-origin Policy
Enforced by browsers, ignored by tools like Postman and Insomnia. Important concept in the web application security model, where a web page can access resources from a second page, as long as both pages live in the same domain (have the same origin).

### CORS (Cross-domain resource sharing)
One way to allow controlled access of resources to different origins. "Relax" the same-origin policy. 

## Import 
You can use the API Gateway import feature to import an API from an external definition file into API Gateway (Swagger 2.0 definition files).

You can create a new API by submitting a `POST` request that includes a Swagger definition in the payload and endpoint configuration. Or you can update an existing API with a `PUT` request. You can update an API by overwriting it with a new definition, or merge a definition with an external API. You specify the options using a mode query parameter in the request URL.

## API Throttling 
By default API Gateway limits steady-state request rate to 10K requests per second (rps). The maximum concurrent requests is 5K requests across all APIs within an AWS account. If you go over 10K rps or 5K concurrent requests, you will receive a `429 Too Many Requests` response. 

## Exam tips
* Remember what it is
* You can throttle API Gateway to prevent attacks
* You can log to CloudWatch
* "Origin policy cannot be read at the remote resource" error = you need to enable CORS on API Gateway
* CORS is enforced by the client
* You can import APIs using Swagger 2.0 definition files
* You get a 429 status code if you go over the 10K rps or 5K concurrent requests 
* API Gateway can be configured as a SOAP passthrough