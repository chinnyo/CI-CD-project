In this project I will creat a multi-environment pipeline to deploy applications to a Dev and Prod environment using EC2 instances, CodeDeploy, CodePipeline and GitHub. I will be using Visual Studio Code to push any updates locally to our remote repository.

Launch 2 instances (Amazon Linux2, t2.micro), name them Dev and Prod and attach instance profile (role for CodeDeploy) to EC2. On the User data script configure the installation of Apache and CodeDeploy agent:

UserData script

#!/bin/bash

#install Apache
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd

#install CodeDeploy agent
yum install ruby -y
yum install wget -y

#Amazon S3 bucket contains the CodeDeploy Resource Kit files for your region. For a list of bucket names and region identifiers see Resource kit bucket names by Region on the AWS documentation.
wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install

#To execute permissions on the install file:
chmod +x ./install

#To install the latest version of the CodeDeploy agent:
./install auto

