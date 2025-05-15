# AWS Infrastructure Project

This project demonstrates how to provision and interact with core AWS services using **Terraform**, **CloudFormation**, and **Boto3**. It also implements automated event-driven logging using **AWS Lambda** and **CloudWatch Logs**.

## 📌 Features

- ✅ Infrastructure provisioning via Terraform and CloudFormation
- ✅ EC2 instance running a web server (Apache)
- ✅ RDS MySQL instance
- ✅ S3 bucket for storing uploaded files
- ✅ AWS Lambda function triggered by S3 uploads
- ✅ CloudWatch integration for Lambda logs
- ✅ Python scripts (using Boto3) to automate interactions
- ✅ GitHub version control and documentation

---

## 🗂 Project Structure

```
aws-infra-terraform/
├── main.tf                       # Terraform script
├── cloud-stack.yaml             # CloudFormation template
├── upload_to_s3.py              # Boto3 script: Create bucket + upload file
├── invoke_lambda.py             # Boto3 script: Manually invoke Lambda
├── README.md                    # Project documentation
└── architecture.png             # AWS diagram (see below)
```

---

## 🖼 Architecture Diagram

![AWS Architecture](architecture.png)

---

## 🚀 Setup Instructions

1. **Terraform**
   - Install Terraform
   - `terraform init`
   - `terraform apply`

2. **CloudFormation**
   - Run:
     ```
     aws cloudformation deploy        --template-file cloud-stack.yaml        --stack-name my-cloud-stack        --capabilities CAPABILITY_NAMED_IAM
     ```

3. **Lambda + S3 Logging**
   - Create a Lambda function using the `lambda_handler` code
   - Add an S3 event trigger for uploads
   - Upload a file to S3 and verify logs in CloudWatch

4. **Python Boto3 Scripts**
   - Install dependencies:
     ```bash
     pip install boto3
     ```
   - Run scripts:
     - `python upload_to_s3.py`
     - `python invoke_lambda.py`

---

## 📂 GitHub Notes

- `.terraform/` is excluded via `.gitignore`
- Commit regularly with meaningful messages
- Ensure large binaries (like Terraform providers) are not pushed

---

## 📎 Author

Lewis Davis  
[GitHub Profile](https://github.com/lewisdavisii)

---