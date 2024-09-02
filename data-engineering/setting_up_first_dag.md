This is a step by step guy how to set up infrastructure for a data engineering project.

#### Prerequisites:

1. Complete steps in the first doc


#### 1. Create a role on AWS that will have access to your S3 bucket

**1. Create an access key in IAM for your user



**2. Enter the access key and secret access key information in Airflow
On your local machine go to Airflow, Admin -> Connections -> Add a new record

- give a name in connection_id
- select s3 in connection type
- in Extra field enter your connection details in following format:

{"aws_access_key_id": "_youraccesskeyid_", 
"aws_secret_access_key": "_yoursecretaccesskey_"}

