# Elasticache
Web service that makes it easy to deploy, operate and scale an in-memory database/cache in the cloud. 

## Supported types
* Memcached
  * Use cases: caching is the primary goal; simple caching model; ability to scale horizontally; large cache nodes.
* Redis 
  * Use cases: more advanced data types (hashes, lists and sets); sorting and ranking datasets in memory; persistence is important; multi AZs with failover.

## Caching strategies 

### Lazy loading 
Loads the data into the cache when necessary. If requested data is in the cache, Elasticache returns the data to the application. If it's not in the cache or has expired, Elascticache returns `null`, the application then fetches the data from the database and writes it into the cache so that it's available next time. Adding a TTL is a way of avoiding stale data. Expired data is treated a cache miss. 

Advantages:
* Only requested data in cache (avoids filling up with unused data)
* Node failures are not fatal (a new empty node results in a lot of cache misses initially)

Disavantages:
* Cache miss penalty (query the database, write to cache, more operations)
* Stale data (doesn't automatically update if the data has changed)

### Write-through
Adds or updates data to the cache whenever data is written to the database. 

Advantages:
* No stale data
* Users are generally more tolerant to additional latency when writing

Disavantages:
* Write penalty (every write results in a write to cache)
* In case of node failure, data is missing until it's updated in the database (mitigate using lazy loading in combination with write-through)
* Wasted resources if most of the data is never read

## Exam tips
* Redis supports primary/secondary replication and multi AZs
* Scenario question about stress/load/read-heavy of OLTP (transactions), you can alliviate the load using Elasticache. If it's about OLAP (analysis/heavy queries/data warehousing), you can alliviate that using Redshift
* When to use Memcached x Redis (super simple cache = Memcached, advanced data types and multi AZs = Redis)
* Remember the caching strategies (lazy loading x write-through)