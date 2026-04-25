# AWS VPC + EC2 using Terraform

## Project Overview

This project demonstrates Infrastructure as Code (IaC) using Terraform on AWS.

Resources created:

- VPC
- Public Subnet
- Internet Gateway
- Route Table
- Security Group
- EC2 Instance

The project also includes security improvements such as restricted SSH access and proper resource tagging.

---

## Technologies Used

- AWS
- Terraform
- EC2
- VPC
- IAM
- Security Groups
- GitHub

---

## Security Improvements

- Restricted SSH access to Terraform server IP only
- Removed overly permissive access rules
- Added structured resource tagging
- Created SECURITY.md for documentation
- Reviewed AWS activity tracking for IAM, EC2, VPC, and S3

---

## Files Included

- main.tf
- provider.tf
- variables.tf
- terraform.tfvars
- outputs.tf
- SECURITY.md
- README.md

---

## Author

Amith
