# Systems Manager Parameter Store
Provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, Amazon Machine Image (AMI) IDs, and license codes as parameter values. You can store values as plain text or encrypted data. You can reference Systems Manager parameters in your scripts, commands, SSM documents, and configuration and automation workflows by using the unique name that you specified when you created the parameter.

## Exam tips
* Know what it is - you securely define a parameter value, and then references the parameter in Cloudformation or etc, to avoid passing around the value itself.