# Cloudfront
Cloudfront is a CDN (content delivery network) that delivers content to a user based on the geographic location of the user. In other words, it's a service that speeds-up the distribution of content (assets). Optimized to work with a lot of other AWS services (like S3, lambdas, etc).

Cloudfront = content delivery (download)
Transfer acceleration = faster uploads to S3.

## Terminology 
* Edge location - a collection servers distributed geographically that keeps a cache of your content (copies of files). After the TTL, the cache is gone. You can clear the cache yourself, but you'll be charged for that
* Origin - The origin of all the files that the CDN will distribute
* Distribution - Name of the given CDN, which consists of a collection of edge locations
* Web distribution - Typically used for websites
* RTMP - Media streaming

## Distribution types
* Website distribution - used for websites, HTTP/HTTPS
* RTMP distribution - Adobe Real Time Messaging Protocol, used for media streaming/flash multi-media content

## Cloudfront and S3 Transfer acceleration 
Enables fast, easy and secure transfers over long distances between users and an S3 bucket. Data is distributed to an edge location, and from the edge location it's routed to the S3 bucket, using an optimized network.

## Exam tips
* Remember edge locations
* There are more edge locations than AZs and regions
* Remember the terminology 
* Remember the different types of distribution
* Edge locations are not read only 
* Cloudfront is also used by S3 transfer acceleration
* You'll be charged for clearing/invalidating the cache yourself
* Maximum TTL is 1 year (365 days in seconds)
* Default TTL is 24h (in seconds)
* You can allowlist/blocklist countries
* Cloudfront configurations are not immediatelly created, it takes up to 15 minutes