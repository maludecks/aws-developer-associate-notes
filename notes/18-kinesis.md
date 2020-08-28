# Kinesis 
Kinesis is a platform in AWS to send streaming data to. Kinesis makes it easier to load and analyze streaming data.

## Services
* Kinesis Streams - data is sent to Kinesis, stored in shards and by default, stored for 24h (configurable to 7 days retention). Separate consumer services then mine and analyse this data and store the results in some other database (DynamoDB, RedShift, S3, etc. The total capacity of the stream is the sum of the capacities of all shards.
* Kinesis Firehose - you don't have to worry about shards, it's all automated. The data analysis can be done by Kinesis Firehose in a lambda, and you can store the result of the analysis in S3. The analytics of the data is optional. There's no retention time, the data is immediately processed or passed through S3. 
* Kinesis Analytics - you can run SQL queries on the data stored inside Kinesis (Streams and Firehose), and then store the result of these queries in S3, RedShift or ElasticSearch.

## Exam tips
* Know the difference between Kinesis Streams and Firehose
* Shards = Kinesis Streams
* Retention period = Kinesis Streams
* Analysing data automatically in lambda = Kinesis Firehose
* On the consumers (EC2 processing the data from the shards), it's the Kinesis Client Library (KCL) that will record a processor for each shard that is being consumed by an instance
* If you increase the number of shards (re-shard), the KCL will add more record processors on your consumers, and it will spread the shards equally between the number of consumers
* Always use the CPU utilization to decide if you need to increase the number of consumers (re-sharding doesn't necessarily mean increasing the number of consumer instances)
* Use an auto-scaling group, and base scaling decisions on CPU load