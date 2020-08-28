# Amazon Cognito
Provides *Web Identity Federation* using social media accounts like Facebook, with the following features:
* Sign-up and sign-in to apps
* Access for guest users
* Acts as an Identity Broker between your application and Web ID providers
* Synchronizes user data for multiple devices (if you update data on your account, it should synced between devices)
* Recommended for all mobile applications AWS services

Cognito brokers between the app and Facebook/Google to provide temporary credentials which map to an IAM role allowing access to the required resources.

## Web Identity Federation
Lets you give your users access to AWS resources after they have successfully authenticated with a web-based identity provider like Amazon, Facebook or Google.  

## AssumeRoleWithWebIdentity
`assume-role-with-web-identity` is an API provided by STS (Security Token Service). Cognito under covers is using this API. You can choose to use the API directly instead of using Cognito as well. In the response of the API, `AssumedRoleUserARN` and `AssumedRoleID` are used to programatically reference the temporary credentials (not an IAM role).

## Exam tips
* Federation allows users to authenticate with a Web Identity Provider
* The users authenticates first with the Web ID provider and receives an authentication token, which is exchanged for temporary AWS credentials, allowing them to assume an IAM role
* Cognito is an *Identity Broker* which handles interaction between your application and the Web ID provider
* Remember the features
* Cognito uses User Pools to manager user sign-up and sign-in directly or via Web ID providers
* Cognito uses Push Syncronization (SNS) to send a silent push notification of user data updates to multiple device types associated with a user ID
* The `STS:AssumeRole` API call returns a set of temporary security credentials which can be used to access AWS resources, including those in a different account
* `AssumeRoleWithWebIdentity` returns a set of temporary credentials (access key ID, secret access key and security token) which give temporary access to AWS services
* Cognito User Pools are like a directory, allowing users sign-up and sign-in. Identity pools are used to grant temporary access to unauthenticated guests.