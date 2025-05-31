# 🏗️ Scalable Web Application with ALB and Auto Scaling

## Overview

This solution demonstrates how to deploy a highly available and scalable web application architecture on AWS using Amazon EC2, Auto Scaling Groups (ASG), and an Application Load Balancer (ALB). The system is designed with cost optimization, monitoring, and basic security best practices in mind. The architecture includes public and private subnets across multiple Availability Zones to ensure high availability and scalability of the compute layer.

---

## Solution Architecture

![Architecture Diagram](./architecture/architecture-diagram.png)

The core components of this solution include:

- **Amazon VPC**: Isolated cloud network with public and private subnets across 2 Availability Zones.
- **Amazon EC2**: Web application servers running in private subnets.
- **Auto Scaling Group (ASG)**: Automatically adds/removes EC2 instances based on demand (desire:2, min:2, max:4).
- **Application Load Balancer (ALB)**: Distributes incoming traffic across EC2 instances.
- **Amazon RDS (Optional)**: Highly available backend database deployed in private subnets (Multi-AZ).
- **Amazon CloudWatch**: Monitors instance (CPU..) and application performance.
- **Amazon SNS**: Sends email alerts when alarms are triggered.
- **IAM Roles**: Provide controlled access to AWS services for EC2 and monitoring components.
- **NAT Gateway**: Allows outbound internet access for private instances. Just 1 for cost effectiveness here as iam using the free trial of AWS.
- **Internet Gateway**: Enables public subnet traffic to reach the internet.

---

## Deployment

To deploy the solution manually:

1. **Set up the VPC**:
   - Create a VPC with 1 public and 2 private subnets.
   - Deploy an Internet Gateway and NAT Gateway.

2. **Launch EC2 instances**:
   - Create a launch template with a web server (NGINX).
   - Use this template with the Auto Scaling Group. (Launch template)

3. **Create the ALB**:
   - Place it in public subnets.
   - Target group must include the EC2 instances from private subnets.

4. **Set up Auto Scaling**:
   - Create scaling policies based on CPU or traffic load.

5. **Configure Monitoring & Alerts**:
   - Set up CloudWatch alarms and SNS notifications for health and resource usage.

6. Launch Amazon RDS in private subnets with Multi-AZ.

---

## Cost Considerations

To minimize costs while meeting functional requirements, this project was implemented using:
- Free tier eligible EC2 instances
- Minimal instance counts
- NAT Gateway used only in a single AZ
- No data transfer-heavy workload

---

## File Structure

```bash
.
├── architecture/
│   └── architecture.pdf
├── screenshots/
│   ├── ec2.png
|   ├── securitygroups.png
│   ├── alb.png
|   ├── rds.png
│   ├── cloudwatch.png
│   └── sns.png
├── README.md
