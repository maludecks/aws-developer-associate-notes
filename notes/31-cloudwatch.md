# CloudWatch
Monitoring service to monitor resources and applications that run on AWS

By default, CloudWatch monitors:
* CPU
* Network
* Disk
* Status check

You can retrieve data using `GetMetricStatistics` API or by using third-party tools. You can store log data in CloudWatch for as long as you want. By default, CloudWatch logs will store data indefinitely, but you can change the retention period.

## Alarms
You can create an alarm to monitor any CloudWatch metric. 

## CloudWatch x CloudTrail x Config
* CloudWatch monitors performance
* CloudTrail monitors your API calls (auditing)
* AWS Config records the state of your AWS environment and can notify you of changes

## Exam tips
* What it is
* If it's not CPU, Network, Disk and Status check (Host Level Metrics), it's a custom metric
* RAM utilization is a custom metric (not by default)
* By default, EC2 monitoring is 5 minutes interval, you can enable detailed monitoring which makes it 1 minute intervals (for smaller intervals, like 10 seconds, you need to configure a high-resolution custom metric)
* Logs are stored indefinitely by default
* You can retrieve logs from terminated instances after their termination
* For custom metrics, the minimun granularity is 1 minute
* Not restricted to only AWS resources