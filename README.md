# Autoscaling Project

This project demonstrates how to set up and configure an autoscaling environment using AWS. It involves creating a VPC, subnets, EC2 instances, an Application Load Balancer (ALB), and CloudWatch alarms to automatically scale the number of instances based on CPU utilization.


## Project Overview

The goal of this project is to create a highly available and scalable infrastructure using AWS services. The infrastructure includes:

- A Virtual Private Cloud (VPC) with public and private subnets
- EC2 instances in private subnets
- An AMI for the autoscaling group
- An Application Load Balancer (ALB) in public subnets
- CloudWatch alarms to monitor and manage CPU utilization
- Autoscaling policies to increase or decrease the number of instances

## Architecture

The architecture consists of the following components:

- **VPC**: A custom VPC with two public subnets and two private subnets.
- **Subnets**: Two public subnets and two private subnets.
- **Route Tables**: Configured route tables for public and private subnets.
- **EC2 Instances**: Two private instances, one in each private subnet, with a user data script for initialization.
- **AMI**: Created an AMI from one of the private instances for use in the autoscaling group.
- **Autoscaling Group**: Configured to use the AMI to launch instances based on scaling policies.
- **Application Load Balancer (ALB)**: Created in the public subnets and connected to the autoscaling group.
- **CloudWatch Alarms**: Monitors CPU utilization and triggers scaling policies.

## Setup and Configuration

### VPC and Subnets

1. **Create a VPC**:
   - Navigate to the VPC dashboard in the AWS console.
   - Create a new VPC with a suitable CIDR block.

2. **Create Subnets**:
   - Create two public subnets in different availability zones.
   - Create two private subnets in different availability zones.

3. **Configure Route Tables**:
   - Create and configure a route table for the public subnets with a route to the internet gateway.
   - Create and configure a route table for the private subnets.

### EC2 Instances and AMI

4. **Launch EC2 Instances**:
   - Launch two EC2 instances in the private subnets.
   - Use the user data script provided below for initialization.

5. **Create an AMI**:
   - Create an AMI from one of the EC2 instances to use in the autoscaling group.

### Autoscaling Group and Load Balancer

6. **Create an Autoscaling Group**:
   - Use the AMI created in the previous step.
   - Configure the autoscaling group with the desired capacity, minimum, and maximum instances.

7. **Create an Application Load Balancer (ALB)**:
   - Create an ALB in the public subnets.
   - Configure the ALB to route traffic to the instances in the autoscaling group.

### CloudWatch Alarms and Scaling Policies

8. **Create CloudWatch Alarms**:
   - Create a CloudWatch alarm to monitor CPU utilization.

9. **Create Scaling Policies**:
   - Create a policy to increase instances if CPU utilization is greater than 70%.
   - Create a policy to decrease instances if CPU utilization is less than 20%.

## EC2 User Data Script

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>This message from : $(hostname -i)</h1>" > /var/www/html/index.html
```

## Deployment

1. **Deploy the VPC and Subnets**:
   - Follow the setup and configuration steps for creating the VPC and subnets.

2. **Deploy EC2 Instances and AMI**:
   - Launch the EC2 instances and create the AMI.

3. **Deploy the Autoscaling Group and ALB**:
   - Set up the autoscaling group and ALB as described.

4. **Configure CloudWatch Alarms and Scaling Policies**:
   - Set up the CloudWatch alarms and scaling policies to manage the instances based on CPU utilization.

## Summary

This project demonstrates a complete autoscaling setup using AWS services. By following the steps outlined in this README, you can create a scalable and highly available infrastructure. The configuration ensures that the number of instances adjusts automatically based on the CPU utilization, optimizing performance and cost-efficiency.
