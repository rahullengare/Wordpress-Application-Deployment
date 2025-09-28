# Wordpress-Application-Deployment
## **WordPress Introduction:**

WordPress is a free and open-source content management system (CMS) written in PHP. It’s widely used for building blogs, business websites, e-commerce stores, and portfolios. WordPress powers more than 40% of websites worldwide because of its flexibility, ease of use, and large ecosystem of plugins and themes.

It runs on a web server (Apache or Nginx), requires PHP, and stores data in a MySQL/MariaDB database. WordPress is a great choice for both beginners and advanced users who want to quickly launch dynamic websites.

---

## **About Project:**

This project demonstrates how to deploy a basic **WordPress application** on an **AWS EC2 instance**. The main goal is to set up a cloud server, install WordPress with its required dependencies (PHP, Apache, and MySQL), and configure it so it can be accessed via a public IP.

The process includes launching an EC2 instance, installing a web server, configuring PHP, setting up a MySQL database, downloading WordPress, and serving it using **Apache**. This provides a practical introduction to hosting CMS-based applications in the cloud.

---

## **Technologies Used:**

- **WordPress** – Open-source CMS used to build websites
- **Apache HTTP Server** – Web server used to host WordPress
- **PHP** – Server-side scripting language required by WordPress
- **MariaDB/MySQL** – Database engine to store WordPress data
- **AWS EC2 (Amazon Elastic Compute Cloud)** – Virtual server where WordPress is hosted
- **Amazon Linux** – The operating system used on the EC2 instance

---

## **Step 1: Launch an EC2 Instance**

1. Go to AWS Console → EC2
2. Launch Instance
    - Name → wordpress
    - Choose AMI → Amazon Linux
    - Instance type → t2.micro
    - Key pair → pem_server_key
    - Security group → launch-wizard-1 (allow ports: 22, 80, 3306)

![Project Screenshot](/images/launch-instance.png)

## **Step 2: SSH into EC2 Instance**

```bash
ssh -i "pem-server-key.pem" ec2-user@ec2-98-84-171-44.compute-1.amazonaws.com
```

![Project Screenshot](/images/connect-instance.png)

## Step 3: Install LAMP in **Amazon Linux**

1. Update your system

```bash
sudo yum update
```

2. Install Apache your LAMP server then Start & enable 

```bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

3. Install MYSQL your LAMP server then Start & enable

```bash
sudo yum install mariadb105-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

4. Install PHP your LAMP server then Start & enable

```bash
sudo yum install php -y
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
```

## **Step 4 : Install wordpress**

1. Go in default directory of httpd

```bash
cd /var/www/html
```

2. Install wordpress

```bash
sudo wget https://wordpress.org/latest.tar.gz
ls
```

3. Now unzip file

```bash
sudo tar -xvzf <file-name>
#sudo tar -xvzf latest.tar.gz
```

4. give permission to file 

```bash
sudo chmod -R 777 wordpress
```

![Project Screenshot](/images/wordpress-done.png)

## **Step 5 : Create Database for Wordpress Envt.**

1. Go to mysql & change/set there password

```
sudo mysql
alter user root@localhost identified by "root";
exit;
```

2. Re Enter into mysql database with password

```
sudo mysql -u root -p
#password 
root
```

3. Create a Database & Show to check then Exit

```
create database wordpressdb;
show databases;
exit;
```

![Project Screenshot](/images/database.png)

## **Step 6 : Install Connector between frontend and database**

1. Install connector

```
sudo yum install php8.4-mysqlnd.x86_64 -y

```

2. Now restart the all packages

```bash
sudo systemctl restart httpd
sudo systemctl restart mariadb
sudo systemctl restart php-fpm
# OR -> sudo systemctl restart httpd mariadb php-fpm
```

## **Step 7 : Now configure wordpress application**

1. Enter ip address then / to wrodpress 

```bash
http://98.84.171.44/wordpress/
```
![Project Screenshot](/images/wordpress-run.png)

2. Now Click on Let's go showing the follwing Output
3. Make configuration

```bash
# Database Name -> Wordpressdb
# username -> root
# password -> root
# Database Host -> localhost
```
![Project Screenshot](/images/wordpress-info.png)

4. Then click on **Submit**
![Project Screenshot](/images/wordpress-run-application.png)
5. Click on run installation then fill information 

```bash
Site Title -> TechBlog
Username -> root
Password -> root
Your Email -> lengarerahul5@gmail.com
Search engine visibility -> Checl-in the box
```

6. Now Click on Install Wordpress
![Project Screenshot](/images/wordpress-blog.png)
8. Now Scussesfullty install or steup
![Project Screenshot](/images/wordpress-success.png)
10. Now click on Log In with Email & password
![Project Screenshot](/images/wordpress-login.png)
12. Application wordpress is running Now
![Project Screenshot](/images/wordpress-done-on-ec2.png)
## **Step 8: Terminate Your Instance**

1. Go to AWS Console → EC2 Instances
2. Select your instance
3. Click **Instance State → Terminate intance**

![Project Screenshot](/images/delete-instance.png)
![Project Screenshot](/images/delete-instance2.png)
