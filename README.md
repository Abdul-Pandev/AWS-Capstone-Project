![image](https://github.com/user-attachments/assets/2258be4a-e5dc-4f38-9f50-b77e5a66b7a2)# AWS-Capstone-Project
My first project in AWS Services
<div align ="justify">
  
# INTRODUCTION
This project demonstrates the implementation of a highly available and scalable AWS infrastructure integrated with data logging using DynamoDB and Python. It is divided into three main parts: VPC and subnet setup for secure networking, deployment of an auto-scaling application using Elastic Load Balancer and EC2, and  a  Python-based  integration with DynamoDB for logging student data.  Each component showcases core AWS services, including VPC, EC2, IAM, ALB, Auto Scaling, CloudWatch, and DynamoDB, emphasizing practical cloud architecture, automation, and real-time data storage. The project not only reinforces cloud engineering principles but also provides hands-on experience in securing, scaling, and managing cloud-native applications.
# Vpc, Subnet, Route-tables, Security Groups, Network Acls, Nat Gateway, Internet Gateway
![image](https://github.com/user-attachments/assets/5a8070b6-b4ca-49f1-994d-4bfd1f956e07)


Objective:
To establish a Virtual Private Cloud (VPC) named room_6vpc as the foundational networking environment for cloud infrastructure.

Actions Taken:

VPC Name: room_6vpc
IP Addressing: Enabled automatic assignment of IP addresses to instances launched within the VPC.

CIDR Block: [Specify if known,10.0.0.0/16]

Additional Configurations: No additional configurations or resources (e.g., subnets, route tables, gateways) were created at this stage.

Outcome:

The VPC room_6vpc was successfully created with basic IP assignment settings enabled. It is now ready for further configuration, such as subnet creation, routing, and security group setup.

# Creating Subnets: Public and Private
![image](https://github.com/user-attachments/assets/6318dd01-1236-4293-bdb3-624581f92b60)

Objective:

To create public and private subnets across multiple Availability Zones within the room_6vpc for high availability and secure network segmentation.

Actions Taken:

Public	Subnets:	Created	two	public	subnets,	each	in	a	different	Availability Zone.

Private	Subnets:	Created	two	private	subnets,	each	in	a	different	Availability Zone.

Subnet	Distribution:	Ensured	even	distribution	for	high	availability	and	fault tolerance.

Association:	All	subnets	were	associated	with	the	previously	created	VPC room_6vpc.

Outcome:

Two  public  and  two  private  subnets  were  successfully  created  in  different Availability Zones under room_6vpc, ensuring redundancy and enabling secure deployment of resources.  
# Creating Route Tables
![image](https://github.com/user-attachments/assets/c730ab66-c318-4971-a79b-c0af300a73e5)
![image](https://github.com/user-attachments/assets/3631f0fb-cd04-4b8a-a8c5-54c2ebc5453e)
![image](https://github.com/user-attachments/assets/e1507bc9-cdb0-4622-8da9-e26d9aab7b47)

Objective:

To configure routing for public and private subnets within the room_6vpc by creating and associating dedicated route tables.

Actions Taken:

Route Tables Created:

Public Route Table

Private Route Table

Associations:

Two public subnets were associated with the Public Route Table.

Two private subnets were associated with the Private Route Table.

Purpose: To manage and control traffic routing for both public-facing and internal network resources.

Outcome:

Two route tables were successfully created and associated with their respective
# Creation of Internet Gateway
![image](https://github.com/user-attachments/assets/5c20f636-05ea-4968-bd78-67407b31c24f)

Objective:

To enable internet connectivity for public subnets within the room_6vpc by creating and attaching an Internet Gateway.

Actions Taken:

Internet Gateway Created: An Internet Gateway was created to 	serve as a connection point between the VPC and the internet.

Attachment: The Internet Gateway was successfully attached to 	the room_6vpc.

Purpose: To allow resources in the public subnets to communicate 	with the internet.

Outcome:

The Internet Gateway was successfully created and attached to the room_6vpc, enabling internet access for resources within the public subnets.

# Creation of NAT Gateway
![image](https://github.com/user-attachments/assets/752d3763-d8b6-4562-b9d3-4fc4827ccae9)

Objective:

To enable	secure	outbound	internet	access	for	instances	in	private	subnets	within	the room_6vpc using a NAT Gateway.


Actions Taken:

NAT Gateway Created: A NAT Gateway was created in one of the public subnets.

Elastic IP: An Elastic IP address was allocated and associated with the NAT Gateway.

Routing Update: The private route table was updated to direct outbound traffic to the NAT
Gateway.

Purpose: To allow instances in private subnets to access the internet (e.g., for updates) 	without exposing them to inbound traffic.

Outcome:

A NAT Gateway was successfully deployed and integrated into the private subnet routing, enabling  secure  outbound  internet  connectivity  for  instances  in  the  private  subnets  of room_6vpc.

# Adding Internet Gateway and NaAT Gateway to Public and Private Route respectively 

![image](https://github.com/user-attachments/assets/03eb9672-c441-49fd-af0d-6f864b205213)
![image](https://github.com/user-attachments/assets/0a76beaf-9762-4b6c-b8c5-6ece6d8da24a)

Objective:

To properly route internet-bound traffic from public and private subnets within the room_6vpc using the Internet Gateway and NAT Gateway.


Actions Taken:


Public Route Table:

Edited to route outbound traffic through the Internet Gateway for internet access.
Private Route Table:

Edited	to	route	outbound	traffic	through	the	NAT	Gateway,	ensuring	secure	internet	access	for private subnet instances.
Outcome:

Route tables were successfully updated to direct traffic appropriately — public subnets route through the Internet Gateway, while private subnets securely access the internet via the NAT Gateway.

# Creating Security Groups
![image](https://github.com/user-attachments/assets/0e2c6298-1ad8-40e2-9c0c-4790174df2be)

Objective:

To control and	secure traffic flow	to EC2 instances in	the	room_6vpc by creating	a security group	with essential inbound access rules.

Actions Taken:

Security Group Created: A new security group was created and associated with the VPC room_6vpc.

Inbound Rules Configured:

HTTP (Port 80): Allowed from anywhere (0.0.0.0/0)

HTTPS (Port 443): Allowed from anywhere (0.0.0.0/0)

SSH (Port 22): Allowed from anywhere (0.0.0.0/0) [Consider restricting this for security]

Purpose: To allow web traffic (HTTP/HTTPS) and remote management (SSH) to EC2 instances.


Outcome:

A security group was successfully created and configured to allow inbound access for HTTP, HTTPS, and SSH protocols, ensuring both accessibility and control over instance communications.

# Creating Network ACLs

![image](https://github.com/user-attachments/assets/e8b2e861-7625-4f26-958c-cbd0afe6eff7)

Objective:
To add a layer of security to the subnets in room_6vpc by configuring Network Access Control Lists (ACLs).

Actions Taken:

Network ACLs Created:

A custom Network ACL was created for enhanced subnet-level security.
Separate inbound and outbound rules were defined to manage traffic.

Inbound Rules Allowed:

HTTP (Port 80)

HTTPS (Port 443)

SSH (Port 22)

Subnet Association:
The created ACL was associated with the appropriate subnets in the VPC.


Outcome:

Network ACLs were successfully created and configured with inbound rules for HTTP, HTTPS, and SSH. They were associated with relevant subnets in room_6vpc, enabling stateless traffic control for enhanced network security.


# Part II - LAUNCHING EC2 INSTANCE, AUTO SCALING, AND LOAD BALANCER

# Creating and Configuring an EC2 Instance 
![image](https://github.com/user-attachments/assets/2944ebd0-0b4a-4620-975b-ae8c2892a18f)

Actions Taken:

Launched EC2 Instance: room6-instance-1

Type: t2.micro

Subnet: Public Subnet

Security Group: Custom group allowing traffic from the Load Balancer

OS: Amazon Linux 2

Configured Application Server:

Installed Apache:

Bash script used

sudo yum update -y

sudo yum install httpd -y

sudo systemctl start httpd 

sudo systemctl enable httpd 

echo "<h1>Welcome to Room 6 Web Server</h1>" | sudo tee /var/www/html/index.html

# Creation of Image (Room6 Image)
![image](https://github.com/user-attachments/assets/fa97d835-be8e-41fb-b03b-8f26fa8d5b33)


Created AMI:

Named the AMI: room6 image

Outcome:

room6-instance-1 is functional as an application server. The	AMI	room6	image	serves	as	a	reusable	blueprint	for	automated scaling and recovery.

# Creation of Load Balancer
![image](https://github.com/user-attachments/assets/fb19b669-f31e-47c4-8e04-31d920018da9)

Objective:

To distribute traffic efficiently and ensure application availability using the Application Load Balancer.


Actions Taken:


Created Application Load Balancer: loadbalancer-room6

Type: Internet-facing

Listener: HTTP (port 80)

Mapped to public subnets across availability zones

Security Group: lb-securitygroup

2.Created Target Group: room6target1

Target type: Instance

Protocol: HTTP

Registered instance room6-instance-1 as a target


3. Configured Health Checks:

Path: /

Protocol: HTTP

Healthy threshold: 3

Unhealthy threshold: 2


Outcome:

loadbalancer-room6 successfully distributes traffic to healthy targets.
room6target1 receives consistent updates on instance health and ensures only healthy servers receive traffic.

# Setting up Auto-Scaling
![image](https://github.com/user-attachments/assets/0a6c48bd-37f8-4a28-9eea-3f8f764cabb7)
![image](https://github.com/user-attachments/assets/80f2c527-892e-4a5f-b287-10dafc18b38b)
![image](https://github.com/user-attachments/assets/ba7f3610-4041-49ab-b243-e2160a4f1d84)

Objective:

Enable automatic scaling of EC2 instances based on real-time demand.

Actions Taken:

Created Launch Template: launch6

AMI: room6 image

Instance Type: t2.micro

Security Group: EC2 security group


2. Created Auto Scaling Group: room6-scale

Launch Template: launch6

Attached to Target Group: room6target1

Availability Zones: Spanned across at least 2 AZs

Instance Count:

Minimum: 1

Desired: 2

Maximum: 4

3. Configured Scaling Policies using CloudWatch Alarm: room6-alarm

Scale Out: When average CPU utilization > 60% for 3 minutes

Scale In: When average CPU utilization < 30% for 5 minutes

Outcome:

room6-scale dynamically scales the application environment based on demand. room6-alarm ensures efficient resource usage and performance optimization. The application is now highly available, resilient, and cost-efficient.

# Testing for Load Balancer, Auto Scaling, and Alarms

![image](https://github.com/user-attachments/assets/ad6b85ab-450f-4f97-87a9-013bd55528c9)
using stress --cpu 2 --timeout 60 to stress the instances
![image](https://github.com/user-attachments/assets/e8051a02-da17-4b2a-896e-2832f28350af)
Reaction of alarm after a stressful instance
![image](https://github.com/user-attachments/assets/96108842-646c-4639-aea6-02c379da869d)
Balancing of Loads from Server to server 1

![image](https://github.com/user-attachments/assets/47fcc939-c901-477a-a59d-a6dcefde17b4)
Instances are created because of overload or stress.

# Part III - DynamoDB Table Creation and EC2 IAM Role Assignment for Secure Data Updates

![image](https://github.com/user-attachments/assets/bf48479e-2a0a-4dee-808e-11b6d0da6210)

Objective:

To create	a DynamoDB	table	named	Students to store student records uniquely identified by a StudentID.

Actions Taken:

Logged into the AWS Management Console.

Navigated to the DynamoDB service.

Clicked “Create Table”.

Entered:

Table Name: Students

Partition Key: StudentID (Type: String)

Left other settings at default (no sort key, no secondary indexes).

Clicked “Create” to provision the table.

# Setting Up Role for DynamoDB Table
![image](https://github.com/user-attachments/assets/5bae3dda-b2e3-4a99-a00f-9b0469a57a75)

Objective:

Ensure an EC2 instance can securely communicate with DynamoDB via an IAM role without using access keys.

Actions Taken:

Part A: Create IAM Role with DynamoDB Access

Navigated to the IAM Console > Roles.

Clicked Create Role.

Selected:

Trusted Entity: AWS Service

Use Case: EC2

Clicked Next and added permission:

Policy: AmazonDynamoDBFullAccess

5 . Named the role (e.g., EC2-DynamoDB-Access) and clicked Create Role.

# Assigning Role to EC2- Instance
![image](https://github.com/user-attachments/assets/7ddf5441-f63a-4f53-8c81-8e3a88688988)


Part B: Attach IAM Role to EC2 Instance

Went to EC2 Console > Instances.

Selected the target instance.

Choose Actions > Security > Modify IAM Role.

Selected the created IAM role (EC2-DynamoDB-Access) and clicked Save.

Outcome:

EC2 instance has proper permissions to interact with DynamoDB.

Verified role assignment via successful list-tables command output.

# Installing of Python3 and Boto3
![image](https://github.com/user-attachments/assets/371375a6-be17-451f-87d3-374ad84c3e3a)

Objective:

Set up the necessary tools (Python and Boto3 SDK) to allow interaction with AWS services from the EC2 instance.


Actions Taken:

Checked Python Installation:

Bash


python3 --version


If not installed:

bash

sudo yum install python3 -y

sudo yum install python3-pip -y


Installed Boto3:

bash

pip3 install boto3 --user

Outcome:

Python 3 and Boto3 were successfully installed and configured on the EC2 instance.

EC2 is ready to run Python scripts that use the AWS SDK.

# Inserting Data into DynamoDB with Python

![image](https://github.com/user-attachments/assets/cd504580-485b-40cd-af1c-d85e425fa2ec)

Objective:
Develop a Python script to insert multiple student records into the Students DynamoDB table.

Actions Taken:
Created script file:
bash

nano student_logger.py

2. Adding a Python code to
 
import boto3

# Create a DynamoDB resource using the region

dynamodb = boto3.resource('dynamodb', region_name='us-east-1')


# Reference the Students table table = dynamodb.Table('Students')


# List of students to add

students = [
{'student_id': '001', 'name': 'Alice Appiah', 'course': 'AWS Cloud Fundamentals'},
{'student_id': '002', 'name': 'Rita Okloo', 'course': 'Linux Basics'}
]


# Insert each student into the table

for student in students:
response = table.put_item(Item=student) print(f"Inserted: {student['name']} | Status:
{response['ResponseMetadata']['HTTPStatusCode']}")


Outcome:

The script student_logger.py is now set up to insert student records into DynamoDB.

Data is structured and handled efficiently in JSON format.


# Confirming Data in DynamoDB
![image](https://github.com/user-attachments/assets/47c72200-2acd-4a9e-93b4-f0d8b6c142c0)

Objective:

Execute the script to insert records and validate that the data is reflected in the DynamoDB table.

Actions Taken:

Ran the script on EC2:

bash

python3 student_logger.py


Output confirmed successful insertions:


Inserted: Alice Appiah | Status: 200 Inserted: Rita Okloo | Status: 200



Verified records:

Navigated to DynamoDB Console > Students > Explore Table Items

Confirmed that  both entries were present.



Outcome:

Script executed successfully.

Student records were inserted into the Students table and are visible in the AWS Console.

# Conclusion

Through this project, we successfully designed and deployed a complete cloud-based architecture combining network configuration, application scaling, and serverless  data  storage.  From  creating  a  secure  VPC  environment  to implementing  dynamic  auto-scaling  and  logging  structured  data  into DynamoDB via a Python script, each step was executed using best practices. We  overcame  common  cloud  configuration  challenges  such  as  IAM  role permissions, NAT routing, and script integration, gaining deeper insights into AWS service interactions, automation with Python, and infrastructure security. The result is a robust, flexible, and production-ready setup that reflects real-world cloud application deployment.

# Thank you for following. I hope you have learned a lot through this and you can carry out the same project



</div>
