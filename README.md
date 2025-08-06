# Automating VPC Deployment with CloudFormation
This document outlines the essential components of an AWS Virtual Private Cloud (VPC), key security best practices, and a CloudFormation template to automate its deployment.
The example template  will deploy a completely new VPC incorporating a number of AWS security best practices which include:

- A VPC with CIDR block of 10.0.0.0/16
- Two Availability Zones (AZ's) lablled AZ-I and AZ-2 on both us-east-1a and us-east-1b
- Two Public and Two private subnets
- One Internet Gateway
- Two NAT Gateway for the two private subnets

---

## VPC Architecture:
![VPC Architecture](/images/VPC.png)

---

## VPC
The VPC itself is the foundational component. It's a logically isolated network that you define within an AWS region. You specify a range of IP addresses for the VPC in the form of a Classless Inter-Domain Routing (CIDR) block, such as ``10.0.0.0/16``.

## Subnets
A subnet is a range of IP addresses within a VPC. You can create different types of subnets:

- Public Subnet: Subnets that have a route to an Internet Gateway. You place resources like web servers and load balancers here that need to be directly accessible from the internet.

- Private Subnet: Subnets that do not have a route to an Internet Gateway. This is where you place sensitive resources like databases and application servers that should not be directly exposed to the internet.

### Internet Gateway (IGW)
An Internet Gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. It provides a target for routes in your route tables for internet-routable traffic.

### NAT Gateway
A NAT Gateway (Network Address Translation) allows instances in a private subnet to connect to the internet or other AWS services, but prevents the internet from initiating a connection with those instances. This is a best practice for securely allowing outbound traffic from private resources.

### Route Tables
A route table contains a set of rules, called routes, that determine where network traffic from your subnets is directed. Each subnet in your VPC must be associated with a route table. The default route table that comes with a VPC has a local route that allows communication within the VPC itself. To enable internet access, you add a route to the Internet Gateway.
The skills you learn will help you secure your workloads in alignment with the AWS Well-Architected Framework .

---

## 🛡️ Security Best Practices
When designing your VPC, consider these security best practices:
- Principle of Least Privilege: Only allow the necessary ports and protocols for inbound and outbound traffic. Don't use 0.0.0.0/0 unless absolutely required.
- Use Private Subnets: Place all sensitive data and application components (e.g., databases, backend services) in private subnets, where they are not directly accessible from the internet.
- Leverage NAT Gateway: Use a NAT Gateway to enable outbound internet access for instances in private subnets. This keeps your private instances secure while allowing them to download updates or connect to external APIs.
- Layered Security: Use both Security Groups and Network ACLs to create a layered defense. Security Groups offer granular, instance-level control, while NACLs provide a broader, subnet-level policy.
- Regular Auditing: Regularly review and audit your Security Group and NACL rules to ensure they align with your security posture and business needs.

---

## Requirements
- An AWS account  that you are able to use for testing, that is not used for production or other purposes.

**NOTE: You will be billed for any applicable AWS resources used if you complete this lab that are not covered in the AWS Free Tier . It is recommended to delete the CloudFormation stack when you have completed the lab.**

---

## Author
- D-cyberguy | Cloud Security Engineer
- Ha5hcat | Cloud Security Engineer

---

## References & useful resources
- [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)
- [Security in Amazon Virtual Private Cloud](https://docs.aws.amazon.com/vpc/latest/userguide/security.html)

---

## Steps:
- [Create VPC Stack](/vpc-stack.yaml)
- Delete stack from the CloudFormation panel after use.


