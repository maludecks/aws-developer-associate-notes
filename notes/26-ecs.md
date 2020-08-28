# Elastic Container Service
Elastic Container Service (ECS) is a container orchestration service which allows you to run containerized workloads in AWS. Supports both Docker and Windows Containers. Similar to Kubernetes. 

Checkout the whitepaper: [Running Containerized Microservices on AWS](https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf)

You have 2 options when it comes to running Clusters of Virtual Machines on ECS:
* Fargate (for Serverless, you don't need to worry about underlying infrastructure)
* EC2 (for more control)

If you already have a Docker Image that you want to start deploying to ECS, you'll have to first add it to Elastic Container Registry (ECR).

## Lab summary
Add a Dockerfile to a CodeCommit repository, use CodeBuild to generate a docker image and push it to ECR, then use ECS to launch a docker container in an EC2, using the docker image from ECR.

## Exam tips
* Remember what a container is: virtual operating environment with everything the software needs to run (library, system tools, code and runtime)
* Remember what ECS is: clustered platform which allows you to run your docker images in the cloud 
* Know the docker commands to push docker images to ECR: 
  * Authenticate your docker client to your registry: `$(aws ecr get-login --no-include-email --region {REGION})`
  * Build docker image: `docker build -t {DOCKER_IMAGE_NAME} .`
  * Tag the image to easily identify it: `docker tag {REPOSITORY_NAME}:latest {REPOSITORY_PATH}:latest`
  * Push the image to the ECR repository: `docker push {REPOSITORY_PATH}:latest`