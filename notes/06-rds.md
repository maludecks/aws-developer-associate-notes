# RDS
Relational Database Service (RDS) is what the name already tells. Compatible with SQL Server, MySQL, PostgreSQL, Oracle, Amazon Aurora and MariaDB.

## Backups
* Automated backups - allow you to recover a database to any point in time within a retention period. The retention period can be between 1 and 35 days. Automated backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will choose the most recent snapshot and transaction logs. Enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of the database.
* Snapshots - Always done manually. They are stored even after you delete the original RDS instance, unlike the automated backups.

When you restore a backup (automated or from snapshots), the restored version will be a new RDS instance.

## Encryption 
Encryption is supported to all database types and it's done through KMS (AWS Key Management System).

## Multi-AZs
If you have a ELB writing to an instance in `eu-west-1`, in case this AZ fails, the ELB will then write to a different AZ. AWS will handle the replication automatically. Downtime is very limited. Multi-AZs is for disaster recovery. Multi-AZs != Read replicas. Read replicas are for performance.

## Read replicas 
Replicas from the production database meant for reading (🥳). Most of the access to a database is usually for reading, and this way you spread the load between instances so one doesn't get overloaded. Good for performance. You can have up to 5 read replicas. Each read replica has it's own DNS endpoint. You can have a read replica that has Multi-AZs. You can turn a read replica to be their own database (or to be the primary/main).

## Exam tips
* You can't connect an EC2 instance in a security group to an RDS instance in a different security group. You have to open port `3306` in the RDS security group, pointing to the EC2 security group so they can interact
* Latency might increase when an automated backup is running
* To encrypt a database you can:
    * Create a snapshot
    * Enable encryption in the snapshot
    * Deploy another instance with the snapshot
* Multi-AZs are for disaster recovery. Multi-AZs != Read replicas. Read replicas are for performance.
* AWS Secrets Manager is an AWS service that can be used to securely store, retrieve, and automatically rotate database credentials. AWS Secrets Manager has built-in integration for RDS databases. Applications use Secrets Manager API's to retrieve database credentials, enabling secure storage of sensitive information outside of the application code.