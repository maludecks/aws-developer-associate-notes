# SNS 
Amazon Simple Notification Service (SNS) is a web service that has the capability to publish messages from an application and immediately deliver them to subscribers or other applications.

SNS allows you to group multiple recipients using topics. A topic is an access point. When you publish to a topic, all multiple subscribers will receive it formatted on the way they need. 

SNS follows the **publish-subscribe** *(pub-sub)* message paradigm.

## Usages
Besides pushing cloud notifications directly to mobile devices, SNS can also deliver notifications by SMS, email, to SQS queus, to any HTTP endpoints, or trigger lambda functions.

## SNS x SQS
* Both are messaging services
* SQS - poll-based
* SNS - push-based

## SES x SNS
* SES (Simple Email Service) is email only
* SES only needs an email addess to start sending notifications 
* SQS consumers need to subscribe to a topic to receive notifications

## Exam tips
* Push-based delivery
* No up-front cost, pay as you go 