# 🚀 AWS Infrastructure Deployment with Terraform

## 📌 Overview

This project demonstrates a **production-ready AWS infrastructure** built and fully automated using **Terraform**.
It provisions a secure and scalable environment following **AWS best practices**, including networking isolation, private databases, and remote state management.

The infrastructure supports deploying a **Node.js web application** running on EC2 and connected securely to an **RDS MySQL database** inside a private subnet.

---

## 🏗 Architecture

The infrastructure follows a **three-tier design**:

* **Networking Layer**

  * Custom VPC
  * Public & Private Subnets
  * Internet Gateway & NAT Gateway
* **Compute Layer**

  * EC2 Web Server (Public Subnet)
  * Auto-configured via Terraform `remote-exec`
* **Database Layer**

  * RDS MySQL (Private Subnet)
  * Access restricted to EC2 only
* **State Management**

  * S3 Remote Backend for Terraform state

---

## 🧱 Infrastructure Components

### 🔹 Networking

* VPC with CIDR `10.0.0.0/16`
* Public Subnet (`10.0.0.0/24`)
* Private Subnet (`10.0.1.0/24`)
* Internet Gateway for public access
* NAT Gateway for private subnet outbound traffic
* Route tables & subnet associations

### 🔹 Security

* Separate Security Groups for:

  * EC2 Web Server
  * RDS Database
* Database port **3306** allowed **only from EC2**
* Web application exposed on **port 3000**
* Principle of **least privilege**

### 🔹 Compute

* EC2 instance running **Amazon Linux 2**
* Auto-generated **4096-bit RSA key**
* Secure SSH access using Terraform-managed key pair
* Node.js application automatically installed and started

### 🔹 Database

* RDS MySQL 5.7
* Instance type: `db.t3.micro`
* Deployed in private subnet
* Credentials managed via Terraform variables

### 🔹 Terraform Backend

* Remote state stored in **Amazon S3**
* Enables team collaboration
* Prevents state conflicts

---

## 📂 Project Structure

```
├── provider.tf
├── vpc.tf
├── security_group.tf
├── ec2.tf
├── rds.tf
├── s3.tf
├── backend.tf
├── variables.tf
├── outputs.tf
└── README.md
```

---

## ⚙️ Prerequisites

* AWS Account
* Terraform v1.5+
* AWS CLI configured
* IAM user with required permissions

---

## 🚀 Deployment Steps

```bash
terraform init
terraform plan
terraform apply
```

After deployment:

* EC2 Public IP will be displayed in outputs
* Node.js app accessible via:

```
http://<EC2_PUBLIC_IP>:3000
```

---

## 🔐 Variables

Sensitive values are managed using variables:

```hcl
MYSQL_USER
MYSQL_PASSWORD
```

You can define them via:

* `terraform.tfvars`
* Environment variables
* CI/CD secrets (recommended)

---

## 📈 DevOps Best Practices Applied

✔ Infrastructure as Code (IaC)
✔ Remote State Management
✔ Network Isolation
✔ Secure Database Access
✔ Automated Provisioning
✔ Scalable Architecture

---

## 🎯 Use Cases

* DevOps portfolio project
* Terraform hands-on practice
* AWS infrastructure reference
* Interview-ready demo project

---

## 👨‍💻 Author

**Seif Allah Osama Ahmed**
DevOps / Cloud Engineer

---

## ⭐ Final Notes

This project focuses on **clean architecture, security, and automation**, making it suitable for real-world cloud environments and DevOps workflows.
