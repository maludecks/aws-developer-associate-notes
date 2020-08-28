# ELB 
Elastic Load Balancers (ELB) helps balance the load accross multiple servers. 

## Types of load balancers
* Classic load balancer - legacy, layer 4 and layer 7, but layer 7 is not nearly as intelligent as the application ELB. By default it returns a 504 when there's an application error.
* Application load balancer - best suited for `http` and `https` traffic. They are "intelligent" and application-aware. You can create advanced request routing, sending specified requests to **specific web servers**. It can determined from where the request is comming from and get a lot of data from it, then decide where does it need to go.
* Network load balancer (preferred for production) - best suited for TCP traffic where extreme performance is required. Capable of handling millions of requests per second maintaining **ultra-low latency**.

Mnemonic: ELB **CAN**!

## Exam tips 
* Remember the types
* 504 means the application did not respond within the timeout period. The problem is not in the ELB, troubleshoot the application.
* To get the public IPv4 address of the end user (not the ELB one), use the *X-Forwarded-For* header.
