# 🌐 AWS VPC Infrastructure with Terraform + Application Load Balancer

This project provisions a secure and scalable **AWS Virtual Private Cloud (VPC)** using **Terraform**, along with an **Application Load Balancer (ALB)** for distributing traffic across EC2 instances. The infrastructure ensures **high availability**, **network isolation**, and is designed to be **modular and reusable** for real-world applications.

---

## 🚀 Features

- ✅ Custom VPC with configurable CIDR block
- ✅ Public and Private Subnets across multiple Availability Zones
- ✅ Internet Gateway for public subnet access
- ✅ NAT Gateway for secure internet access from private subnets
- ✅ Route Tables with proper routing rules
- ✅ Application Load Balancer (ALB) with:
  - HTTP Listener
  - Target Group
  - Health Checks
- ✅ Security Groups for EC2 and ALB
- ✅ Output of important resource attributes (e.g., VPC ID, ALB DNS)
- ✅ Clean, production-ready Terraform code

---

## 🧱 Architecture Overview
```
[ Internet ]
     |
     |--> [ Application Load Balancer ]
                 |
        +--------+--------+
        |                 |
 Public Subnets     Private Subnets
   (EC2 Instances)     (DB, App Tiers)
        |                 |
        +--------+--------+
                 |
           NAT Gateway (optional)
```

---

## 📁 Project Structure

```
terraform-vpc-alb/
├── main.tf               # Terraform root module
├── variables.tf          # Input variables for customization
├── outputs.tf            # Output values to display after apply
├── vpc.tf                # VPC, subnets, IGW, NAT, routing
├── alb.tf                # ALB, target group, listener
├── security.tf           # Security groups for ALB & EC2
├── terraform.tfvars      # Actual values for variables
├── provider.tf           # AWS provider configuration
└── README.md             # Documentation
```

---


## ⚙️ Prerequisites

- AWS CLI configured (\`aws configure\`)
- Terraform installed (v1.0+)
- IAM user/role with VPC, EC2, and ALB permissions

---

## 🚀 Deployment Steps

\`\`\`bash
# Step 1: Initialize the project
terraform init

# Step 2: Review the execution plan
terraform plan

# Step 3: Apply the configuration
terraform apply
\`\`\`

Confirm with \`yes\` when prompted.

---

## 🌐 Access the Load Balancer

After successful deployment, Terraform will output the DNS name of your ALB:

\`\`\`bash
terraform output alb_dns_name
\`\`\`

Visit the ALB DNS name in your browser or use \`curl\` to test:

\`\`\`bash
curl http://<alb_dns_name>
\`\`\`

---

## 📌 Notes

- Modify \`terraform.tfvars\` to change the CIDR blocks, subnet counts, or instance types.
- ALB health checks and listeners are set up for port 80 (HTTP). You can extend this to HTTPS.
- Security groups are open to port 80 for public traffic — restrict this in production.

---

## 🔒 Security Considerations

- Ensure IAM roles and Terraform state are securely managed.
- Use remote backends like S3 with state locking via DynamoDB in production.
- Always restrict CIDR ranges in security groups (avoid \`0.0.0.0/0\` unless necessary).

---

## 👨‍💻 Author

**Mohit Dushyant Matte**  
DevOps & AWS Cloud Enthusiast  
[🔗 LinkedIn](https://www.linkedin.com/in/mohit-matte-a6496a240/)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- [Terraform AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS Load Balancer Docs](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
