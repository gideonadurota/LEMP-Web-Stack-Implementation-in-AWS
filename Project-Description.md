# LEMP Stack Implementation #

Prerequisites:
* VS Code
* AWS Account
* GitHub Personal Access Token

## 1. Launch EC2 Instance ##

* I logged into my AWS console
* I navigated to EC2 and clicked on create instance
* I created a free tier instance adding security rules for ssh (port 22) and http (port 80)
* I downloaded the ssh key 

## 2. Install NGINX server ##

* I launched terminal and ran the command below to give the necessary permissions to the pem file

`sudo chmod 0400 lempwebstack.pem`

* ssh into the ec2 instance 

`ssh -i lempwebstack.pem user@ip-address`

* In order to install NGINX server, first I updated the packages on the ubuntu server

`sudo apt update -y`
`sudo apt install nginx -y`
`sudo systemctl status nginx`

* I confirmed that I could reach the apache website on localhost 

`curl http://localhost:80`

* I got the public ip address of the server using the command `curl -s http://169.254.169.254/latest/meta-data/public-ipv4` and navigated to the address on my browser.

## 3. Install MySql DB ##

The next step was to install and configure MySQL on the server

* use ‘apt’ to acquire and install this software:

`sudo apt install mysql-server -y`

* Set the mysql root password by first logging in as root user using `sudo mysql` then run the script

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'rootpassword';`

* I ran a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running `sudo mysql_secure_installation`. You can accept the remaining prompts to finish mysql configuration


**Note:** At the time of this writing, the native MySQL PHP library mysqlnd doesn’t support caching_sha2_authentication, the default authentication method for MySQL 8. For that reason, when creating database users for PHP applications on MySQL 8, you’ll need to make sure they’re configured to use mysql_native_password instead.

