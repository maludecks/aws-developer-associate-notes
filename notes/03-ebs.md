# EBS 
If EC2 is a virtual server in the cloud, EBS is a virtual disk. EBS allows you to create storage volumes and attach them to EC2 instances. You can create a file system on top of these volumes, run a database, etc. An EBS is replicated through multiple AZs.

## Volume types
### SSD
* General purpose SSD (GP2) - balances price and performance. Less than 10K IOPS. Can be a boot volume (primary).
* Provisioned IOPS SSD (IO1) - designed for I/O intensive applications, like large scale databases. For more than 10K IOPS (up to 20K IOPS). Can be a boot volume (primary).

### Magnetic
* Throughput optimized HDD (ST1) - for big data, warehouses, log processing. It can't be a boot volume (always an additional volume). 
* Cold HDD (SC1) - lowest cost storage for infrequently accessed workloads. Typical use is a file server. It can't be a boot volume (always an additional volume). 
* Magnetic (Standard) - lowest cost per gigabyte of all bootable EBS. For workloads where data is accessed infrequently and where lowest cost is very important (test applications). Legacy but can still be used.

## Exam tips
* Remember the different EBS volume types
* EBS volumes created from encrypted snapshots are automatically encrypted. EBS volumes created from unencrypted snapshots are automatically unencrypted. You can't undo it. If you want to **choose** to encrypt or not, do not select a snapshot
* To encrypt a Root volume there are 2 ways:
  * OS: Do it through the operating system
  * Snapshot:
    * Create a snapshot
    * Create an encrypted copy
    * Generate an image with the encrypted copy
    * Launch an EC2 using this image
* To encrypt additional volumes you can use the console or the CLI
* Frequent snapshots are not recommended, as they can result in performance degradation
* It is not possible to directly share an EBS volume with another account. In order to do so, it is required to create an EBS volume snapshot and grant permissions on that snapshot to the second AWS account. Although EBS volume snapshots are stored in S3, they are not in a user-visible bucket