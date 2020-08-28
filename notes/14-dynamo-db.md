# DynamoDB
Fast, flexible, scalable and fully managed NoSQL database. Document and key-value store.

* Stored on SSD storage
* Spread accross 3 geo-distinct data centers
* Choice of 2 consistency models:
  * Eventually consisted reads (default) - usually reached within 1 second
  * Strongly consisted reads - result reflects all sucessful writes that happened prior to the read

## Consists of 
* Table
* Items (row)
* Attributes (columns)
* Supports key-value and document structures (JSON, HTML or XML)

DynamoDB stores and retrieves data based on a **primary key**. Primary keys can be of 2 types:
* Partition key - unique
* Composite key - partition key + sort key 

## Auth
Authentication and access control is done via IAM. You can create IAM roles to give permanent or temporary access to DynamoDB. You can also create a special **IAM condition** to restrict user access to their own records (match the partition key with the user ID).

## Indices
There are 2 types of indices in DynamoDB:

### Local secondary index
* Can only be created when creating the table
* You can't add, remove or modify later
* It has the same partition key as the original table but a different **sort key**
* Gives a different view of the data but using a different sort option
* Any queries that run using this sort key are faster using the index than using the main table

### Global secondary index
* Can be created when creating the table, or added later
* Different partition key as well as sort key than the main table (completely different view of the data)
* Speeds up any queries relating to this alternative partition and sort key

## Scan x Query

### Query
Query operation finds items in a table based on the primary key. You can also use a sort key to refine the results. By default a query returns all attributes, but you can select only specific attributes using the `ProjectionExpression`. Results are always sorted (asc) with the sort key. You can reverse the order (desc) setting the `ScanIndexForward` to false (queries only). Queries are **eventually consistent** by default.

### Scan
Examines every item on a table. By default it also returns all attributes. A scan will read all the data from the table first, and then on top of that, add filters, to remove the unwanted data.

Query is more efficient than scan. As the table grows, the scan operation takes longer. A scan on a large table can use the provisioned throughput in just a single operation.

You can reduce the impact on performance of a query or scan by setting a smaller page size which uses fewer read operations.

Avoid using scans, design the application in a way that you can use `Query`, `Get` or `BatchItemGet` APIs.

## Pricing - capacity

### Provisioned throughput
Used to define the capacity and performance requirements in DynamoDB.
* Measured in capacity units 
* When you create the table you define read and write capacity units
* 1 write capacity unit = 1 x 1KB write per second
* 1 read capacity unit = 1 x strongly consistent read of 4KB read per second **OR** 2 x eventually consistent reads of 4KB per second (default)

### On-demand capacity 
Charges apply for reading and writing, with on-demand you don't need to specify your requirements. DynamoDB instantly scales up and down based on the activity of the application (great for unpredictable workloads).

## DAX
DynamoDB Accelerator (DAX) is an in memory cache for DynamoDB. DAX is a write-through caching service = every time DynamoDB writes to a table, the cache is updated. If on read, it's a cache miss, then DAX performs an **eventually consistent** `GetItem` operation against the table.
* Only for read performance
* Delivers up to 10x read performance improvements 
* Ideal for read heavy/bursty workloads (black friday promotions, gaming, etc)
* Not suitable for: **strongly consistent** reads, write intensive applications, low read traffic, applications that don't require microsecond response times

## Transactions
All or nothing operations, ACID (as most relational databases).

You can use a transaction when you need an ACID operation, or when you need to check for a certain pre-requisite condition before writing to a table (like checking if there's money on an account before a transfer).

## TTL
Defines an expiry time for data. Items marked for deletion = deleted in the next 48 hours. Good for removing stale data. You can filter out expired items from queries and scans. You define the attribute used as TTL.

## Streams
History of item modifications (inserts, updates and deletions). Everytime an item changes it will be recorded in DynamoDB Streams. 
* These logs are stored for 24h. Accessed using a dedicated endpoint
* You can use a DynamoDB Stream to trigger a lambda if a certain operation happened
* By default the primary key is recorded
* You can configure to get snapshots from before and after the changes
* Events are recorded in near real-time
* Applications can take action based on which operation/what happened to the data
* Event source for Lambda

## ProvisionedThroughputExceededException
Happens if your request rate is too high for the read/write capacity provisioned. The SDK will automatically retry the requests until successful. If you're not using the SDK you can:
* Reduce request frequency
* Use exponential backoff

### Exponential backoff
Exponential backoff means progressively longer waits between consecutives retries (50ms, 100ms, 200ms...) for improved flow control. If after 1 minute the retries keep failing, you might exceed the request size throughput for read/write capacity. In this case, you want to evaluate the throughput. 

## Exam tips
* Know what it is (low latency NoSQL database that supports key-value and document data models)
* Supported documents formats are JSON, HTML and XML 
* Consists of tables, items and attributes
* 2 types of primary keys: partition key (unique) and combination of partition key + sort key (composite)
* 2 consistency models: eventually consisted reads and strongly consistent reads
* Access is controlled via IAM
* Fine grained access using IAM condition (match user ID with the partition key)
* Indices enable faster queries on specific data columns
* Know the difference between the index types
* Know the difference between query and scan
* Prefer queries to scans
* You can configure parallel scans (divide a table or index into segments and scan each segment)
* Avoid parallel scans if the table/index is already incurring heavy reads/writes 
* 1 write capacity unit = 1 x 1KB write per second
* 1 read capacity unit = 1 x strongly consistent read of 4KB read per second **OR** 2 x eventually consistent reads of 4KB per second (default)
* Choose provisioned capacity when you can predict workloads and traffic, otherwise use on-demand (spiky, short lived peaks traffic)
* You can switch pricing models once per day
* DAX is an in-memory cache for eventually consistent read intensive applications
* DAX was built specifically for DynamoDB (as opposed to Elasticache)
* DAX only uses write-through strategy (no lazy loading)
* When the current time is greater than the TTL, items are marked to be deleted = deleted in 48 hours
* `ProvisionedThroughputExceededException` means number of requests are too high
* Use exponential backoff as a strategy (not only for DynamoDB)
* A Partition key is a single attribute and is used as a Primary Key attribute to **uniquely** identify a record in the DynamoDB table (IDs)