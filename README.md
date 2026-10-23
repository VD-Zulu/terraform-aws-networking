
Terraform AWS Networking — MZ-UCA Day 10
Project Overview
This project demonstrates the deployment of a multi-tier AWS network using Terraform.

The infrastructure includes public and private subnet tiers, controlled routing, an Internet Gateway, and NAT-based outbound connectivity for private resources.

Architecture
AWS VPC — 10.0.0.0/16

│

├── Public Subnet A — 10.0.1.0/24

├── Public Subnet B — 10.0.2.0/24

│

├── Private Subnet A — 10.0.11.0/24

├── Private Subnet B — 10.0.12.0/24

│

├── Internet Gateway

├── Public Route Table

│ └── 0.0.0.0/0 -> Internet Gateway

│

├── NAT Gateway

│

└── Private Route Table

└── 0.0.0.0/0 -> NAT Gateway
Technologies Used
Terraform

AWS

AWS CLI

Visual Studio Code

Git

GitHub

AWS Resources Created
VPC
Two public subnets
Two private subnets
Internet Gateway
Elastic IP
NAT Gateway
Public route table
Private route table
Route-table associations
Network Design
Public Tier
The public subnets use a route table with a default route pointing to the Internet Gateway. Resources launched into these subnets can communicate directly with the internet when security controls allow it.

Private Tier
The private subnets do not have a direct route to the Internet Gateway. Outbound traffic is routed through the NAT Gateway, providing internet access without exposing private resources directly to inbound internet traffic.

Engineering Explanations
Why does the VPC need an Internet Gateway?
The Internet Gateway provides connectivity between resources inside the VPC and the public internet. Without an Internet Gateway, resources in public subnets would not be able to send or receive internet traffic.

Why must the NAT Gateway be in a public subnet?
The NAT Gateway must be deployed in a public subnet because it requires access to the Internet Gateway. The NAT Gateway receives outbound traffic from private subnets and forwards that traffic to the internet. It also returns responses back to private resources without exposing them directly to inbound internet connectivity.

Terraform Workflow
terraform init
terraform fmt
terraform validate
terraform plan -out=tfplan
terraform apply tfplan
terraform output
terraform state list
terraform destroy
Evidence
Terraform Validation

Terraform Plan

Terraform Apply

Terraform Output

Terraform State

AWS VPC

AWS Subnets

Public Route Table

Private Route Table

NAT Gateway

Key Learning Outcomes
Infrastructure as Code
AWS VPC design
CIDR planning
Public and private subnet design
Internet Gateway routing
NAT Gateway routing
Terraform resource dependencies
State inspection
Infrastructure validation
Infrastructure documentation
Security Notes
No AWS credentials or secrets are stored in this repository.

Terraform state files and local Terraform working directories are excluded from Git using the .gitignore file.

Cleanup
Terraform resources are removed using:

terraform destroy
Author
Cloud Engineering Student — MZ-UCA Cloud Academy

Infrastructure Cleanup
Screenshot: screenshots/12-terraorm-destroy.png