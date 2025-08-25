# Terraform AWS Shopping Website & Web Application Deployment

This project demonstrates how to deploy a **shopping website** and a **scalable, secure web application** on AWS using **Terraform**.  
It provisions multiple AWS services to ensure **high availability, security, and performance**.

---

## Project Overview

By following this project, you will:

- Understand how to provision AWS resources using Terraform  
- Deploy a **shopping website** with authentication and caching  
- Learn how to set up **EC2 instances behind an ALB** with Auto Scaling  
- Implement **secure user authentication with Amazon Cognito**  
- Integrate **Amazon RDS** and **Amazon ElastiCache** for database and caching optimization  
- Gain hands-on experience building a complete AWS cloud infrastructure  

---

## Key Services Used

- **VPC Module** – Networking (VPC, subnets, NAT, routing, gateways)  
- **Security Groups** – Secure inbound/outbound rules for EC2, ALB, RDS, Redis  
- **EC2 + ASG Module** – Web application servers with Auto Scaling  
  - EC2 instances fetch website package from S3 (`s3://your-bucket/WebSite.zip`)  
  - User data injects Cognito config into `index.html` automatically at boot 
- **Application Load Balancer (ALB)** – HTTPS-enabled traffic distribution (ACM cert required)  
- **Amazon Cognito** – Authentication and user management  
- **Amazon RDS (MySQL)** – Managed relational database with initial schema & data  
- **Amazon ElastiCache (Redis)** – Optional performance caching layer (disabled by default as it takes longer to deploy)


---

## Architecture Diagram

![AWS Architecture Diagram](./Project-Diagram.png)  
*Shows EC2, ALB, ASG, Cognito, RDS, and ElastiCache workflow.*

---

## Features

- Fully automated deployment with **Terraform**  
- **High availability** and **scalability**  
- Secure authentication with **Cognito**  
- Optimized database performance with **RDS + Redis**  
- Integration of shopping website frontend with Cognito and database backend  
- **Cost** – Free Tier friendly

---

## Prerequisites

- Terraform >= 1.3  
- Download and extract `Terraform_Full_Project.zip`
- Change `<Your-Region>` in `/variables.tf`
- ACM Certificate ARN for your ALB domain in `/variables.tf`
- Create your own profile and change `<Your-Profile>` in `/provider.tf` 
- Download `WebSite.zip` and upload to S3 bucket (update bucket path in `/modules/asg/user_data.sh.tftpl`)  
- Terraform modules structure [here](./Structure)

---

## Getting Started

1. **Clone or unzip** the project:
   ```bash
   unzip Terraform_Full_Project.zip -d terraform_project
   cd terraform_project
   ```

2. **Initialize Terraform**:
   ```bash
   terraform init
   ```

3. **Review the plan**:
   ```bash
   terraform plan
   ```

4. **Apply the configuration**:
   ```bash
   terraform apply
   ```

5. **Access the app** using the ALB endpoint once deployed.

---

## Example `variables.tf`

```hcl
aws_region          = "us-east-1"
project_name        = "shopping"
db_username         = "admin"
db_password         = "YourStrongPassword123"
acm_certificate_arn = "arn:aws:acm:us-east-1:123456789012:certificate/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

---

## Notes

- EC2 runs in **public subnets**, ALB routes traffic to EC2  
- To run EC2 in **private subnets**, NAT Gateway is required for S3 and manage EC2  
- Cognito integration injects values into `index.html` during boot  
- DB tables will be created in RDS are products and cart

---

## Resources

- **[Bootstrap](https://getbootstrap.com/)** – UI framework for styling and responsive design  
- **[Getty Images](https://www.gettyimages.com/)** – Stock images used in the project  

## License

This project is licensed under the [**MIT License**](./LICENSE)  
