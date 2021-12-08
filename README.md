# Terrafom_remote_state_file_in_s3

# Terraform state file on s3 backend 
[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](#)


When you  are building an infrastrucre using IAC (infrastructure as code) tool terraform, a state file is generated locally in the directory and it contains all the details about your infrastrure  that means it act as a database for your infrastrucre. This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment. 

Here in this project I have uploaded the tfstate file to remote backup s3 bucket So we can easily manage state file.

## Prerequisites.
- S3 storage
- IAM user who have the  full privilleages to s3 bucket 

## Features
- Terraform writes the state data to a remote data store and it  make more easier to modify or manage the infrastructure.


**Please note: To setup the tstate file in remote end initially we need an IAM user details wth s3 full access and s3 bucket**

Here I already created a s3 bucket "remotetfstate" for my project and I'm setting the backend to s3

```hcl
terraform {
        backend "s3"{
        bucket      = "remotetfstate"
        key         = "terraform/terraform.tfstate"
        region      = "ap-south-1"
        encrypt     = true
        }
}
```

Now Backend initialization required, The "backend" is the interface that Terraform uses to store state, perform operations, etc.  The Terraform configuration that we are using is a custom configuration for the Terraform backend. Changes to backend configurations require reinitialization. This allows terraform to set up the new configuration, copy existing state, etc. So  we have to run "terraform init" with either the "-reconfigure" or "-migrate-state" flags to
use the current configuration.

Output: 

```
jisjo@jisjo-$ terraform init -reconfigure

Initializing the backend...

Successfully configured the backend "s3"! Terraform will automatically
use this backend unless the backend configuration changes.

Initializing provider plugins...
- Finding latest version of hashicorp/aws...
- Installing hashicorp/aws v3.68.0...
- Installed hashicorp/aws v3.68.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

```

Lets validate the terraform files using
```sh 
terraform validate
```

Lets plan the architecture and verify once again.

```sh
terraform plan
```
Lets apply the above architecture to the AWS.
```sh 
terraform apply
```
So lets first checkout our s3 bucket -

![alt text](https://github.com/sruthymanohar/Terraform-statefile-on-s3/blob/main/Capture1.PNG)

Here we can see that our state file is working fine in remote end s3  and locally you can see that it becomes an empty file.

```sh 
-rw-r--r-- 1 root root  199 Sep  1 17:32 main.tf
-rw-r--r-- 1 root root  143 Sep  1 13:36 provider.tf
-rw-r--r-- 1 root root    0 Sep  1 14:53 terraform.tfstate
-rw-r--r-- 1 root root 3809 Sep  1 14:53 terraform.tfstate.backup
[root@ip-172-31-8-241 awsproject]#
```
# Conclusion

Here in this project terraform writes the state data to a remote data store and it  make more easier to modify or    manage the infrastructure



⚙️ Connect with Me
 
  <a href="https://www.linkedin.com/in/sruthy-manohar-9a9b54150/">
     <p> <img align="left" alt="Abhishek's LinkedIN" width="22px" src="https://raw.githubusercontent.com/peterthehan/peterthehan/master/assets/linkedin.svg" /> </p>
   </a> 
