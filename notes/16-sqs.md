# SQS
Simple Queue Service (SQS) is a web service that gives you access to a message queue. A queue is a temporary repository for messages that are awaiting processing. Using a queue is great for when the producer is producing work faster than the consumer can process it.

## Types of queue 
* Standard queue - default, nearly-unlimited requests per second, no order garanteed (generally delivered in the same order as they are sent)
* FIFO - order garanteed, duplicates are not introduced to the queue

## Visibility timeout
The period of time that a message is invisible after a consumer picks it up. If the consumer process the message **before** the visibility timeout expires, the message gets deleted from the queue. If the message is not processed within the timeout, the message will get visible in the queue again, and will get to be picked up again.

## Polling
* Short Polling - returns immediatelly even if no messages are in the queue
* Long Polling - is a way to retrieve messages from an SQS queue. Long polling doesn't return a response until a message arrives or until the long poll times out. Saves some money because in a different scenario you would be constantly polling every short interval of time. Maximum long poll timeout is 20 seconds

## Delay Queues
Postpone delivery of new messages to a queue for a number of seconds. Messages sent to the delay queue remain invisible to consumers for the duration of the delay. Default is 0 seconds delay, maximum is 900 seconds. 

## Managing large SQS messages
For large SQS messages (256KB uo to 2GB in size), the best practice is to store them in S3. You need an specific SDK to store and manage the messages in S3.

## Exam tips
* SQS is a pull-based system 
* Remember the types of queues
* Messages are 256KB in size
* Messages can be kept in the queue from 1 minute to 14 days
* Default retention period is 4 days
* SQS guarantees that your message will be processed at least once
* Default visibility timeout is 30 seconds
* Visibility timeout should be increased if the process takes more than 30 seconds
* Maximum visibility timeout is 12 hours
* DelaySeconds != VisibilityTimeout (hidden *before* it gets picked-up x hidden *after* it gets picked-up)
* Maximum long poll timeout is 20 seconds
* You can delay or post-pone the delivery of new messages to a queue using *delay queues* 
* Store large messages in S3
* You can use Amazon S3 and the Amazon SQS Extended Client Library for Java to manage Amazon SQS messages stored in S3. This includes specifying when messages should be stored in S3, referencing message objects stored in S3, getting them, and deleting them