# SECURITY.md

## Security Review and Improvements

This document explains the security risks identified in the existing Terraform infrastructure, improvements made, and activity tracking observations for AWS services.

---

## Existing Infrastructure

The Terraform project includes:

* VPC
* Public Subnet
* Internet Gateway
* Route Table
* Security Group
* EC2 Instance

The infrastructure was initially created for learning Infrastructure as Code using Terraform on AWS.

---

## Identified Security Risks

### 1. SSH Access Open to Entire Internet

Initially, the security group allowed SSH access from:

```hcl
cidr_blocks = ["0.0.0.0/0"]
```

This means anyone on the internet could attempt SSH access to the EC2 instance.

### Risk

This increases the chances of:

* Brute force attacks
* Unauthorized login attempts
* Security breaches

---

### 2. Overly Permissive Security Rules

HTTP and SSH rules were broadly open without restrictions.

### Risk

This creates unnecessary exposure and increases attack surface.

---

### 3. Lack of Proper Resource Tagging

Resources had only basic naming and lacked structured tags like:

* Environment
* Owner
* Project

### Risk

This makes auditing, ownership tracking, and cost management difficult.

---

### 4. Limited Monitoring Awareness

No initial focus on CloudTrail, CloudWatch, or VPC Flow Logs.

### Risk

Without monitoring, suspicious activity may go unnoticed.

---

## Security Improvements Implemented

### 1. Restricted SSH Access

Updated SSH rule from:

```hcl
cidr_blocks = ["0.0.0.0/0"]
```

to:

```hcl
cidr_blocks = ["15.237.110.147/32"]
```

Only the Terraform server is now allowed to SSH into the EC2 instance.

### Benefit

This significantly reduces external attack risk.

---

### 2. Controlled HTTP Access

HTTP (Port 80) remains open only for intended public web access.

### Benefit

Access is allowed only where required.

---

### 3. Improved Resource Tagging

Added structured tags:

```hcl
tags = {
  Name        = "Terraform-EC2"
  Environment = "Internship"
  Project     = "DevOps-Terraform"
  Owner       = "Amith"
}
```

### Benefit

Improves management, visibility, and auditing.

---

## Best Practices Followed

* Principle of Least Privilege
* Restrict SSH access to known IP only
* Avoid unnecessary open ports
* Use Infrastructure as Code for repeatable security
* Maintain proper resource tagging
* Verify changes using Terraform state and AWS Console
* Use CloudTrail and CloudWatch for auditing

---

## Activity Tracking and Observability

---

## IAM

### Activities Generated

* User login attempts
* Access key creation
* Role creation/deletion
* Policy changes
* MFA enable/disable
* Permission updates

### Where to View

* AWS CloudTrail
* IAM Console
* CloudWatch (if integrated)

### Why Important

Helps detect:

* Unauthorized access
* Privilege escalation
* Suspicious permission changes

---

## EC2

### Activities Generated

* Instance launch/start/stop/terminate
* Security group changes
* EBS volume attach/detach
* Key pair usage
* Network interface changes

### Where to View

* AWS CloudTrail
* Amazon CloudWatch
* EC2 Monitoring tab

### Why Important

Helps detect:

* Unexpected instance launches
* Unauthorized shutdowns
* Resource misuse
* Performance issues

---

## VPC

### Activities Generated

* Subnet creation
* Route table updates
* Internet Gateway attachment
* Network ACL changes
* Traffic flow monitoring

### Where to View

* CloudTrail
* VPC Flow Logs
* CloudWatch Logs

### Why Important

Helps detect:

* Network misconfigurations
* Suspicious traffic patterns
* Unauthorized routing changes

---

## S3

### Activities Generated

* Bucket creation/deletion
* Object upload/download/delete
* Permission changes
* Public access changes
* Lifecycle policy updates

### Where to View

* CloudTrail
* S3 Server Access Logs
* CloudWatch
* S3 Console

### Why Important

Helps detect:

* Data leaks
* Unauthorized access
* Public exposure of sensitive data

---

## Final Outcome

The infrastructure is now more secure, properly documented, and follows better operational practices.

This task improved understanding of:

* Cloud security fundamentals
* Secure Terraform practices
* AWS monitoring and auditing
* Infrastructure documentation standards

