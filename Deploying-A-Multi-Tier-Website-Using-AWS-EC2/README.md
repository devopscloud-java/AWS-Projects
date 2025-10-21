EC2 Auto Scaling with RDS Integration
📘 Description

Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the AWS cloud. It removes the need to invest in physical hardware upfront, enabling faster development and deployment of applications. EC2 allows you to launch virtual servers, configure networking and security, and manage storage. With EC2, you can easily scale up or down to handle changing demands, ensuring efficient performance and cost optimization.

🧩 Problem Statement

Company ABC wants to migrate their existing product infrastructure to AWS. The product currently consists of:

A MySQL Database

A PHP-based Website

To ensure high availability and scalability, the company wants to enable Auto Scaling for the website hosted on EC2.

⚙️ Steps to Solve
1. Launch an EC2 Instance

Go to the EC2 Dashboard in the AWS Management Console.

Click Launch Instance and choose an Amazon Linux 2 or Ubuntu AMI.

Select an instance type (e.g., t2.micro).

Configure instance details such as VPC, subnet, and IAM role if required.

Add security groups that allow HTTP (port 80), HTTPS (port 443), and SSH (port 22).

Launch and connect to your instance using SSH.

2. Enable Auto Scaling (Minimum 2 Instances)

Create an Auto Scaling Group (ASG) using the instance as a template (via Launch Template or Configuration).

Set desired capacity = 2, minimum = 2, maximum = 4 for scaling flexibility.

Attach an Elastic Load Balancer (ELB) to evenly distribute traffic between instances.

3. Create an RDS Instance

Navigate to RDS > Databases > Create Database.

Choose MySQL as the engine type.

Select Free tier or desired instance type.

Database details:

DB Name: intel

Master Username: admin

Master Password: intel123

Enable Public access (optional, for testing) and ensure proper VPC & subnet group configuration.

4. Create Database and Table in RDS

Once RDS is running:

Connect to the database using MySQL client or phpMyAdmin:

mysql -h <RDS-endpoint> -u admin -p


Create database and table:

CREATE DATABASE intel;
USE intel;
CREATE TABLE data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    value VARCHAR(100)
);

5. Change Hostname in the Website Code

Update your PHP website configuration to point to the RDS endpoint instead of localhost.

$servername = "your-rds-endpoint.amazonaws.com";
$username = "admin";
$password = "intel123";
$dbname = "intel";
$conn = new mysqli($servername, $username, $password, $dbname);


Redeploy or upload the updated PHP files to the EC2 instance.

6. Allow Traffic from EC2 to RDS Instance

Edit the RDS Security Group:

Add an Inbound Rule allowing MySQL/Aurora (port 3306) from the EC2 Security Group.

7. Allow All Traffic to EC2 Instance

Edit the EC2 Security Group:

Add an Inbound Rule allowing All traffic (0.0.0.0/0) for testing or restrict to required ports (80, 443, 22) for production.

🧠 Key Takeaways

Auto Scaling ensures high availability and fault tolerance.

RDS simplifies database management and improves reliability.

Security Groups control inbound/outbound access between EC2 and RDS.

Proper hostname configuration connects your web app to the cloud database seamlessly.

✅ Output

Highly available web application hosted on AWS EC2 instances.

Auto Scaling ensures uptime during traffic spikes.

Backend data stored securely in RDS MySQL instance.

🏷️ Tags

AWS EC2 AutoScaling RDS MySQL PHP Cloud Computing
