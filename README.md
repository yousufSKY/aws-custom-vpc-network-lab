# AWS Custom VPC Architecture with Public and Private Subnets

![AWS](https://img.shields.io/badge/AWS-VPC-orange?style=for-the-badge&logo=amazonaws)
![EC2](https://img.shields.io/badge/Amazon-EC2-orange?style=for-the-badge&logo=amazon-aws)
![Networking](https://img.shields.io/badge/Cloud-Networking-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## Project Overview

This project demonstrates the design and implementation of a secure and scalable custom network architecture on AWS using Amazon VPC.

The architecture consists of one custom VPC containing multiple subnets distributed across Availability Zones, custom route tables, an Internet Gateway, security groups, and EC2 instances for connectivity validation.

The primary objective of this project was to gain hands-on experience with AWS networking fundamentals and understand how routing, subnet isolation, and internet connectivity work within a cloud environment.

---

## Architecture Diagram

![Architecture Diagram](./Architecture-diagram-VPC.png)

---

## Architecture Components

### Networking Resources

| Resource | Configuration |
|-----------|--------------|
| VPC | `172.31.0.0/16` |
| Public Subnets | 1 |
| Private Subnets | 3 |
| Internet Gateway | 1 |
| Route Tables | 3 |
| Security Groups | 1 |
| EC2 Instances | Amazon Linux 2 |

---

## CIDR Design

### VPC CIDR

```text
172.31.0.0/16
```

### Subnet Allocation

| Subnet | Type | Availability Zone | CIDR Block |
|---------|------|-------------------|------------|
| Subnet_1 | Public | us-east-2a | 172.31.0.0/20 |
| Subnet_2 | Private | us-east-2b | 172.31.16.0/20 |
| Subnet_3 | Private | us-east-2c | 172.31.32.0/20 |
| Subnet_4 | Private | us-east-2c | 172.31.48.0/20 |

---

## Route Table Configuration

### RT_1 (Public Route Table)

| Destination | Target |
|------------|--------|
| 172.31.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

Associated Subnet:

- Subnet_1 (Public)

---

### RT_2 (Private Route Table)

| Destination | Target |
|------------|--------|
| 172.31.0.0/16 | Local |

Associated Subnet:

- Subnet_2

---

### RT_3/RT_4 (Private Route Table)

| Destination | Target |
|------------|--------|
| 172.31.0.0/16 | Local |

Associated Subnets:

- Subnet_3
- Subnet_4

---

## Security Configuration

A custom Security Group was created for EC2 instances.

### Inbound Rules

| Type | Protocol | Source |
|-------|----------|--------|
| SSH | TCP 22 | My IP |
| ICMP | All | 0.0.0.0/0 |
| Custom Rules | As Required | VPC CIDR |

### Outbound Rules

| Type | Destination |
|-------|-------------|
| All Traffic | 0.0.0.0/0 |

---

## Implementation Steps

### 1. Created a Custom VPC

- Created a new VPC named `Custom_VPC`
- Assigned CIDR block `172.31.0.0/16`

---

### 2. Created Multiple Subnets

- Created one public subnet.
- Created three private subnets.
- Distributed subnets across multiple Availability Zones.

---

### 3. Created Route Tables

- Created dedicated route tables.
- Associated route tables with respective subnets.

---

### 4. Configured Internet Gateway

- Created an Internet Gateway.
- Attached it to the custom VPC.
- Added default route (`0.0.0.0/0`) in the public route table.

---

### 5. Configured Security Groups

- Allowed SSH access.
- Enabled ICMP traffic for connectivity testing.

---

### 6. Launched EC2 Instances

- Launched Amazon Linux EC2 instances inside the public subnet.
- Assigned public IP addresses.
- Connected securely using SSH.

---

### 7. Connectivity Validation

The following tests were performed successfully:

✅ EC2 instance successfully accessed the internet.

✅ Public subnet routing verified.

✅ ICMP ping tests performed.

✅ External systems were able to reach the public instance.

✅ Route table associations validated.

---

## Validation Tests

| Test | Result |
|-------|--------|
| Internet Connectivity | Passed |
| Public IP Reachability | Passed |
| Ping from External Machine | Passed |
| Route Table Verification | Passed |
| VPC Resource Validation | Passed |

---

## AWS Services Used

- Amazon VPC
- Amazon EC2
- Internet Gateway
- Route Tables
- Security Groups
- Subnets
- Elastic Network Interfaces

---

## Repository Structure

```text
.
├── README.md
├── LICENSE
├── architecture-diagram.png
└── screenshots/
    ├── 01-console-home.png
    ├── 02-navigating-to-VPC.png
    ├── 03-Regions-in_VPC.png
    ├── ...
    └── 27-Instance-public-IP_accessible.png
```

---

## Screenshots

Detailed implementation screenshots can be found inside the `screenshots/` directory.

Examples include:

- VPC Creation
- Subnet Creation
- Route Table Configuration
- Internet Gateway Attachment
- Security Group Creation
- EC2 Launch
- Connectivity Testing

---

## Key Learning Outcomes

- Designing custom AWS VPC architectures.
- Understanding CIDR block allocation and subnetting.
- Configuring route tables and subnet associations.
- Implementing public and private network segmentation.
- Managing Internet Gateway connectivity.
- Configuring AWS Security Groups.
- Launching and validating EC2 connectivity.
- Troubleshooting networking issues in AWS.

---

## Future Enhancements

- Add NAT Gateway for private subnet internet access.
- Deploy EC2 instances inside private subnets.
- Implement Bastion Host architecture.
- Add Network ACL custom rules.
- Configure VPC Flow Logs.
- Implement High Availability architecture.
- Integrate Load Balancer and Auto Scaling.

---

## Author

**Syed Yousuf**

Computer Science Engineer | Cloud & DevOps Enthusiast

GitHub: https://github.com/yousufSKY

LinkedIn: https://www.linkedin.com/in/syed-yousufuddin-a64265276

---

## License

This project is licensed under the MIT License.
