# AWS Cloud Infrastructure Deployment on AWS

## Project Overview

This project demonstrates how to deploy a static website on an AWS EC2 instance, configure network access, store project information in Amazon S3, and securely access S3 using an IAM role.

The goal is to gain hands-on experience with core AWS infrastructure and security concepts relevant to a Junior Cloud Engineer role.

## Architecture

**Request flow:**

User Browser → Internet Gateway → EC2 Instance (Ubuntu + Nginx)

**Storage and permissions:**

EC2 Instance → IAM Role → Private S3 Bucket

## AWS Services Used

- **Amazon EC2:** Virtual server to host the website.
- **Amazon VPC:** Network environment for the EC2 instance.
- **Subnet:** Network segment containing the instance.
- **Internet Gateway:** Enables internet connectivity through the VPC route table.
- **Security Groups:** Controls inbound network access.
- **Amazon S3:** Stores project documentation.
- **AWS IAM:** Grants the EC2 instance limited access to S3.
- **Nginx:** Web server used to host the static webpage.
- **AWS CLI:** Used to test AWS permissions from the EC2 terminal.

## Implementation Steps

### 1. Launch EC2 Instance
- Launched an Ubuntu EC2 instance in the Mumbai region (`ap-south-1`).
- Connected to the instance using SSH and EC2 Instance Connect.

### 2. Configure the Web Server
- Installed Nginx on Ubuntu.
- Enabled and started the Nginx service.
- Created a custom HTML webpage and verified it through the public IP address.

### 3. Configure Networking
- Reviewed the VPC and subnet configuration.
- Verified the route table's local route and default route to the Internet Gateway.
- Configured security group rules for HTTP and restricted SSH access.

### 4. Configure Amazon S3
- Created a private S3 bucket.
- Uploaded `project-details.txt`.
- Kept public access blocked.

### 5. Configure IAM Role
- Created an EC2 IAM role named `EC2-Project-S3-ReadOnly-Role`.
- Attached a custom policy named `ProjectBucketReadOnlyPolicy`.
- Granted only the permissions required to list the project bucket and read its objects.
- Attached the role to the EC2 instance.

### 6. Validate Permissions
- Used `aws sts get-caller-identity` to verify the assumed IAM role.
- Used the AWS CLI to list the S3 bucket contents and read `project-details.txt`.
- Tested an upload and confirmed that it was denied, demonstrating restricted permissions.

## Security Practices

- Used an IAM role instead of storing long-term AWS access keys on EC2.
- Followed the principle of least privilege for S3 access.
- Kept S3 Block Public Access enabled.
- Restricted SSH access instead of allowing SSH from all IP addresses.

## Screenshots

Project screenshots are available in the `screenshots/` directory.

## Key Learnings

- Launching and connecting to an EC2 instance.
- Hosting a website using Nginx on Ubuntu.
- Understanding VPCs, subnets, route tables, and Internet Gateways.
- Configuring security groups.
- Using S3 for private object storage.
- Attaching IAM roles to EC2 instances.
- Testing AWS permissions using the AWS CLI.

## Region

AWS Asia Pacific (Mumbai) — `ap-south-1`

## Future Improvements

- Automate infrastructure provisioning using Terraform.
- Configure monitoring and alarms with Amazon CloudWatch.
- Set up HTTPS using a domain name and TLS certificate.
- Implement automated deployment using a CI/CD pipeline.
