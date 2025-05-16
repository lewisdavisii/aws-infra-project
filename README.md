# AWS Infrastructure Project

This project demonstrates how to provision and interact with core AWS services using **Terraform**, **CloudFormation**, and **Boto3**. It also implements automated event-driven logging using **AWS Lambda** and **CloudWatch Logs**.

This AWS architecture consists of a Virtual Private Cloud (VPC) with both public and private subnets to separate the application and database layers. In the public subnet, EC2 instances run behind an Application Load Balancer (ALB) to handle incoming web traffic, with autoscaling configured to adjust capacity based on demand. The private subnet hosts a relational database, specifically Amazon RDS, which remains inaccessible from the internet to enhance security. Static assets, logs, and other objects are stored in an Amazon S3 bucket, while an AWS Lambda function is configured to automatically trigger upon file uploads to the bucket, logging those events to Amazon CloudWatch for observability. Security Groups control traffic between all services, and the entire infrastructure is defined and deployed through CloudFormation templates. Version control is maintained through GitHub, enabling reliable tracking of changes and potential integration with CI/CD workflows for automated deployments.

To implement this cloud infrastructure, I used a combination of the AWS Management Console, the AWS Command Line Interface (CLI), and Python scripts using the Boto3 SDK. I began by defining all necessary resources—such as the VPC, subnets, EC2 launch templates, an autoscaling group, RDS instance, Lambda function, and security configurations—within a CloudFormation template and deployed them using aws cloudformation deploy. I configured the EC2 instance to serve a basic HTML website using Apache and verified the web server was functioning by accessing its public DNS. I then created and configured a Lambda function to log details of any new file uploaded to an S3 bucket, tested it with file uploads and manual invocation, and verified that logs were successfully generated in CloudWatch. Python scripts were also created to automate S3 bucket creation, file uploads, listing EC2 instances, retrieving EC2 metadata, and invoking Lambda functions. All progress and code were regularly committed and pushed to a GitHub repository for version control and collaboration.

During development, several challenges arose that required troubleshooting and refinement. One major issue involved GitHub’s file size restriction, which caused push failures due to a large Terraform provider executable. This was resolved using git-filter-repo to permanently remove the large file from version history and a .gitignore file was added to prevent similar problems in the future. Another problem was CloudFormation stack failures caused by incorrect VPC or subnet configurations, particularly for the RDS instance and Auto Scaling Group. These were fixed by ensuring subnets spanned multiple Availability Zones and that DNS support was enabled in the VPC. I also encountered permission issues when configuring IAM roles for Lambda to access S3 and CloudWatch, which were resolved by creating specific policies with the required permissions and attaching them properly.

Looking ahead, there are several ways to improve scalability, maintainability, and automation in this architecture. First, implementing a CI/CD pipeline using AWS CodePipeline or GitHub Actions would automate deployments and streamline updates. Modularizing the CloudFormation templates by separating networking, compute, and application layers would increase flexibility and make the infrastructure easier to maintain. Integrating Secrets Manager or SSM Parameter Store for environment-specific configuration values would enhance security and scalability. Additionally, introducing services like Amazon API Gateway in front of the Lambda function would allow for more controlled and scalable access. Finally, adding robust monitoring and alerting using CloudWatch Alarms and AWS Systems Manager would provide better insight into system performance and enable proactive response to issues.

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
