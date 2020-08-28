# CodeBuild
Continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy

## Exam tips 
* Remember what it is
* By default, CodeBuild expects a configuration file called `buildspec.yml` to be in the root directory, but you can override it by manually inserting build commands in the console in CodeBuild
* You can also override environment variables through CodeBuild console
* By default, all logs are sent to CloudWatch
* CodeBuild uses the BuildSpec file as a specification of build commands and settings. “secrets-manager” syntax can be used to retrieve API Keys stored in AWS Secrets Manager