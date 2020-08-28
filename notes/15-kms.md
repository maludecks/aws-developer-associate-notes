# KMS
Key Management Service (KMS) is a managed service to create and control encryption keys used to encrypt data.

## Integrations
* EBS
* S3
* Redshift
* ElasticTranscoder
* Amazon WorkMail 
* RDS
* and more

## Customer Master Key (CMK)
Consists of: 
* Alias
* Creation date 
* Description
* Key state
* Key material (either AWS or customer provided)
* Can **never** be exported

How to create one: 
* Define alias, description and key material
* Define key **Administrative Permissions**: IAM users/roles that can administer (but not use) the key through KMS API
* Define key **Usage Permissions**: IAM users/roles that can use (but not manage) the key to encrypt and decrypt data

## Envelope encryption 
The process of using the master key to encrypt a data key (called the envelope key), and then use the envelope key to encrypt the data. Basically **not** using the master key for data encryption. For decryption, you take the envelope key, decrypt it to plain text using the master key and an encryption algorithm, and then use the plain text to decrypt the data.

## Exam tips
* What KMS is 
* KMS is multi-tenant whereas CloudHSM is dedicated hardware
* Encryption keys are regional 
* Keys in KMS can never be exported
* Know these API calls: 
  * `aws kms encrypt`
  * `aws kms decrypt`
  * `aws kms re-encrypt`
  * `aws kms enable-key-rotation`
* Know what's a CMK (Customer Master Key) 
* Envelope key = CMK encrypts envelope key, envelope key encrypts data