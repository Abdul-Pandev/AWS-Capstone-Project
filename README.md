# AWS-Capstone-Project
My first project in AWS Services
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
