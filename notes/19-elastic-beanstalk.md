# Elastic Beanstalk
A service for deploying and scaling web applications. You upload the code and Elastic Beanstalk will handle deployment, capacity provisioning, load balancing, auto-scaling and application health. 

## Updating code
Elastic Beanstalk supports multiple options for processing deployments:
* All at once - deploys new versions to all instances simultaneously, which means you will experience downtime. If the update fails, you need to rollback the changes by re-deploying the old version. Not ideal for production environments.
* Rolling - Deploys new versions in batches. Your environment capacity will be reduced by the number of instances in a batch while the deployment takes place. If the update fails, you'll need to perform an additional rolling update to rollback the changes. Not ideal for performance sensitive systems.
* Rolling with additional batch - Launches an additional batch of instances for the deploy and then deploys the new code in batches. Mantains full capacity during deployment process. If the update fails, you need to perform an additional rolling update to rollback. Good for performance sensitive systems.
* Immutable - Deploys the new code to a fresh group of instances in their own new auto-scaling group. When the instance pass the health-check, they are moved to your auto-scaling group, and instance with the old code are terminated. The rollback process requires only terminating the new auto-scaling group. Preferred option for **Mission Critical** production systems.

## Advanced Elastic Beanstalk
You can customize your Elastic Beanstalk environment using configuration files. The configuration is defined in a YAML or JSON format. The file can have a filename of your choice but must have a `.config` extension and be save inside inside a folder called `.ebextensions`. The `.ebextensions` directory must be included in the top-level directory of the application.

## RDS & Elastic Beanstalk 
You can launch RDS instances within the Elastic Beanstalk environment, but it means the database lifecycle will be tied to the application environment. If you terminate the environment, it terminates the database (good for development and testing only). For production environments, the preferred option is to decouple the RDS instance from the Elastic Beanstalk environment. 

To allow the EC2 in the Elastic Beanstalk environment to connect to an outside database, there are 2 additional configuration steps:
* An additional security group must be added to your environment's auto-scaling group
* Provide the connection string configuration to your application servers.

## Exam tips
* What it is and what it does: 
  * Deploys and scales web applications including the web application server platform where required
  * Supports a lot of programming technologies (NodeJS, Docker, Java, PHP)
  * Provisions underlying resources for you
  * You can choose to administer the EC2 instances or leave it to Beanstalk
  * Updates, monitoring, metrics and health checks are included
* Know the differentt update strategies
* You can customize the environment with a configuration file
* Docker containers can also be deployed using Elastic Beanstalk
* You can deploy your docker container to a single EC2 instance
* You can deploy multiple docker containers to an ECS cluster
* You can upload your code from your local machine, a public S3 bucket or CodeCommit
* You can use Packer to build a custom Elastic Beanstalk platform (custom platforms = customized OS, additional software for applications that use languages or softwares not supported by a managed platform)