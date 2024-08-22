This is a step by step guy how to set up infrastructure for a data engineering project.

#### Prerequisites:

1. Set up AWS Account

2. Create and launch EC2 instance in AWS

Make sure to save the pem file and note down it's location on your computer

3. Register on Rapid API: https://rapidapi.com/


#### 1. How to connect to your EC2 instance 

**1. Open up your terminal and execute the following commands:**
(https://stackoverflow.com/questions/54133300/how-to-access-and-modify-a-ssh-file-on-mac)

```
open -t ~/.ssh/config
```

**2. Once open, fill in the following information**
```
# Alias to your machine
Host [any-alias-for-your-remote-machine]
    HostName [public-ip-address-of-your-remote-machine]
    User ec2-user
    IdentityFile [the-full-path-to-your-pem-file]
```

***3. Now you can log in to your EC2 instance***

```
ssh [any-alias-for-your-remote-machine]
```

To exit: 
```
exit
```

If you don't want to set up the config file, you can always log in to the EC2 instance like this:

```
ssh -i /path/to/pem_file/key_pair.pem ec2-user@[public-ip-address-of-your-remote-machine]
```

If this doesn't work, and you get `Permissions denied` error, fix the permissions:

```
chmod 400 bla-bla/my_folder/key_pair.pem
chmod 400 ~/.ssh/id_rsa
```

*More information*: https://stackoverflow.com/questions/54133300/how-to-access-and-modify-a-ssh-file-on-mac

#### 2. Install docker and docker-compose 

**2.1 On local machine**
Extract the zip file and run the following commands one by one:

`docker-compose build`

`docker-compose up`

or 

`docker-compose up -d`

You can access airflow on your web browser with http://localhost:8080, username and password =  airflow

**2.1 On your EC2 instance**

Copy docker folder from local machine to your EC2 instance:

`scp -r -i bla-bla/key-pair.pem path/to/folder ec2-user@ip-address:path/to/file `
