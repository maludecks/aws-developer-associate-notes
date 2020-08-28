# IAM
Identity and Access Management (IAM) allows management of users and their level of access to AWS. IAM consists of:
* Users
* Groups
* Policies/Policy documents
* Roles

## What IAM gives you
* Centralized control over an AWS account
* Shared access to an AWS account
* Granular permissions (enable different levels of access to different users)
* Identity federation (including Active Directory, Facebook, etc)
* Multi-factor authentication 
* Provide temporary access for users/devices and services, as necessary
* Set up password rotation policy 
* Integrates with many AWS services
* Supports PCI DSS compliance (for payment industry)

## Critical terms
* Users = People
* Groups = Collection of users under one set of permissions (every user in the group gets the same set of permissions, for instance a marketing team, or database admins).
* Roles = Used to define a set of permissions. You can create a role and assign them to AWS resources. Allows services to interact with each other on your behalf (for example, allow full access to S3 through EC2s on behalf of my account).
* Policy = A document that defines one or more permissions. A policy document is a JSON that contains a `Version` (date) and a `Statement` that consists of `Effect`, `Action` and `Resource`. 

## Creating users 
A user can be added to a group, which is assigned to one (or more) policies; Or, you can attach the user to policies directly, without a group. A user can both be in a group and have directly assigned permissions. 

## Important notes
* IAM is universal: it does not apply to regions
* Root account: the first account created when you first setup your AWS account. It has complete admin access by default. Should be used carefully.
* New users have **no permissions** by default
* New users are assigned an *access key* and a *secret access key*  when first created
* Access key/secret access key != User/password. User/Password are used to login into the AWS console. Access key/secret access key are used for CLI, SDK and APIs.
* You can only view the access key/secret access key once when creating the user. If you lose them, you have to regenerate them.
* Always setup MFA and follow the security steps on the root account (for instance password rotation policies).

## Inline Policies x Managed Policies x Custom Policies
* Managed Policies - IAM policy created and administered by AWS, policies for common use cases based on job functions. You can't change the permissions attached to these policies.
* Custom Policies - is a standalone policy that you create and administer (only) inside your own AWS account. Recommended where existing AWS policies don't fit the requirements.
* Inline Policies - IAM policy which is actually embedded within the user, group or role to which it applies (1:1 relationship between entity and policy). When you delete the entity the policy is also deleted.

## IAM Policy Simulator
You can use the [IAM Policy Simulator](https://policysim.aws.amazon.com) to validate that a policy works as expected. You can also test policies already attached to a user (great for troubleshooting).

## Exam tips
* Least Privilege - always give the minimum amount of access required
* Create groups - always assign users to groups. Groups permissions are assigned by policy documents
* Secret Access Key - you only see it once. If you don't save it, you can delete it and generate it again
* Never use just one access key - every user should have their own access keys. Save it, but somewhere safe
* You can use the CLI on your PC - you can install the CLI in any computer
* Roles:
  * Grant access between AWS resources. You have to know how to read a JSON policy document
  * Allow you to **not** use access keys
  * Preferred from a security perspective. Access keys are difficult to manage/securely store/share
  * Controlled by policies
  * You can change a policy on a role and it will take immediate effect
  * You can attach/detach roles to a running EC2 instance without having to stop or terminate it
* You can't edit permissions of *Managed Policies*
* You can validate policies through the IAM Policy Simulator