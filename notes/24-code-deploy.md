# CodeDeploy
Automated deployment service, works with EC2s, on-premises and Lambdas. 

## Deployment approaches

### In-place
The application is stopped on each instance (one by one) and the new release is installed. Also known as a *Rolling update*. 

Steps:
  * CodeDeploy stops the application in the first instance
  * The instance is out of service during the deployment (capacity is reduced)
  * No traffic should be sent to the instance while the deployment is running (needs to be configured in the load balancer)
  * CodeDeploy installs the new version of the application, known as a **revision** 
  * The instance comes back into service and gets re-registered with the load balancer
  * CodeDeploy continues to the next instance

Rollback:
You are going to need to re-deploy the previous version. Which means going through the entire process again.

### Blue/Green
New instances are provisioned and the new release is installed on the new instances. Blue represents the active version, green is the new release. You pay for both environments until the deployment is completely finished and the old instances are terminated. 

Steps:
* CodeDeploy provisions new instances, completely independent of the production (blue) environment
* The revision is deployed to the green environment
* The green instances are registered with the load balancer
* Traffic is routed away from the blue environment
* The blue environment is eventually terminated 

Rollback: 
If something fails on deployment, you can set the loadbalancer to direct traffic to the blue environment. This can only be done if the blue environment hasn't been terminated yet.

## AppSpec file
Configuration file that defines the parameters to be used during a CodeDeploy deployment. The file structure depends on whether you are deploying on EC2 or Lambda. For EC2 and on-premise systems, the AppSpec file can be written on YAML format only. For Lambda, it can be written in YAML and JSON format. The AppSpec file must be placed in the root directory of the revision.

File structure: 
* Version - reserved for future use, only allowed value is 0.0
* OS - operating system version
* Files - location of any application files that need to be copied and where they should be copied to
* Hooks/Lifecycle event hooks - scripts which need to run at set points in the deployment lifecycle. Example of scripts: 
  * Unzip files
  * Run tests
  * Deal with load balancing

## Lifecycle event hooks
Lifecycle event hooks are run in a specific order known as the *run order*.
Examples: `BeforeInstall`, `AfterInstall`, `ApplicationStart`, `ValidateService`.

### Run order for an in-place deployment
Think of 3 different phases:
* Phase 1: de-register instances from a load balancer
  * `BeforeBlockTraffic`: all tasks that you want to run before the instances are de-registered from the load balancer
  * `BlockTraffic`: de-register instances from the load balancer
  * `AfterBlockTraffic`: all tasks that you want to run after the instances are de-registered from the load balancer

* Phase 2: activities that need to happen in order to deploy the application itself
  * `ApplicationStop`: scripts you need to run for gracefully stopping the application
  * `DownloadBundle`: CodeDeploy agent copies the application revision files to a temp location
  * `BeforeInstall`: pre-installation scripts (backing up current version, decrypting files, etc)
  * `Install`: copying the application files to the final location
  * `AfterInstall`: post-install scripts (configuration, file permissions, etc)
  * `ApplicationStart`: start any services that were stopped during `ApplicationStop`
  * `ValidateService`: run tests to validate the service, if it works as expected

* Phase 3: re-register instances with the load balancer
  * `BeforeAllowTraffic`: tasks that you want to run on the instances before they are registered with the load balancer
  * `AllowTraffic`: register instances with the load balancer
  * `AfterAllowTraffic`: tasks that you want to run on the instances after they are registered with the load balancer

## Exam tips
* CodeDeploy supports EC2, ECS (both EC2 and Fargate), Lambda, and on-premise servers
* Application version = Revision
* Know the difference between the deployment approaches
* Safest option for a production deployment = Blue/Green (doesn't affect performance, fast to rollback)
* AppSpec on EC2 = YAML
* AppSpec on Lambda = YAML and JSON
* AppSpec file must be placed in the root directory of the revision
* Understand the run order (lifecycle event hooks order)
* In-place deployment: 3 phases (de-registering load balancer, application deployment, re-registering load balancer) 