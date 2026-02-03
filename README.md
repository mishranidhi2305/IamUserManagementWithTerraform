AWS IAM User Management with Terraform 

📌 Overview

This project demonstrates AWS IAM user and group management using Terraform, with users defined in a CSV file.
It follows a data-driven, Infrastructure as Code approach similar to Azure AD user management.

🛠️ What This Project Creates

26 IAM Users with AWS Console access

3 IAM Groups

Education

Managers

Engineers

Automatic group membership based on user attributes

User tags (DisplayName, Department, JobTitle)

Local Terraform state (no S3 backend)

📋 Prerequisites

AWS CLI configured

Terraform v1.0+

IAM permissions for user and group management

🚀 Quick Start
terraform init
terraform plan
terraform apply -auto-approve

Verify in AWS IAM Console:

Users → 26 users created
Groups → Members assigned dynamically

📁 Project Structure
day16/
├── provider.tf
├── main.tf        # User creation 
├── groups.tf      # Groups & memberships
├── users.csv      # User data
├── output.tf
├── local.tf       #CSV parsing
├── data.tf        #Datasource
└── README.md

⚙️ How It Works

Reads users from users.csv

Creates IAM users with format: {first_initial}{lastname}

Enables console access with password reset

Assigns users to groups based on:

Department

Job Title

👥 Groups

Education → Department = Education

Managers → Job title contains Manager / CEO

Engineers → Department = Engineering (currently empty)

➕ Add Users

Update users.csv and run:

terraform apply

🔐 Password Note

Terraform creates login profiles but does not return passwords.
Users must set passwords on first login or via AWS Console/CLI.

🧹 Cleanup
terraform destroy


⚠️ Deletes all IAM users and groups created by Terraform.

✅ Key Takeaways

CSV-driven user management

Fully automated IAM provisioning

Idempotent & repeatable

Easy to extend with policies and MFA
