# CloudFormation
CloudFormation is a service that allows you to manage, configure and provision AWS infrastructure as code.

* Resources are defined using a CloudFormation template (YAML and JSON)
* CloudFormation reads a template from S3, then interprets the template and makes the appropriate API calls to create the resources defined
* The resulting resources are called a stack

## Benefits
* Consistency, fewer mistakes
* Less time with manual configuration 
* You can version control templates
* Free to use (charged only by what you create)
* Can be used to manage updates and dependencies
* Can be used to rollback and delete entire stacks 

## Template structure
The main sections in a CloudFormation template are:
* Parameters - input custom values
* Conditions - make decisions based on a set of parameters, ex.: provision based on environment
* Resources (mandatory) - the resources that will be created
* Mappings - create custom mappings, ex.: define AMI (Amazon Machine Image) based on the region
* Transforms - reference code/reusable snippets located in S3 and also for specifying the use of the Serverless Application Model (SAM) for Lambda deployments
* Outputs - user defined data relating to the resources you have built and that can also be used as input to another CloudFormation stack

## Nested stacks
Nested stacks allow re-use of CloudFormation code for common use cases, ex.: standard configuration for a load balancer, application server, etc. Instead of copying the same code every time, you can create a standard template for each common use case and then reference it from within another CloudFormation template. AKA: A template within a template. You can reference a nested stack template using the `Stack` resource type.

## Exam tips
* What it is: manage, configure and provision insfrastructure as code (YAML and JSON)
* Know the structure of a CloudFormation file
* The resources section is the only mandatory section of a template
* Automatic rollback on failure can be configured
* You can easily delete a template from S3 after the stack is deleted
* Nested stacks templates must be uploaded to an S3 bucket