# Project 2 - SMART SERVERLESS AUTOMATION PIPELINE

## Complete Step-by-Step Industry Level Project Guide   
         
> **What you will build (One-line):**   
> A **smart serverless automation pipeline** where code changes automatically trigger a workflow that **builds, tests, and deploys a serverless application on AWS** without managing any servers.

This is written in **very simple English**, exactly how **industry DevOps + Cloud engineers** explain and work.

---

## 1️⃣ What is a Smart Serverless Automation Pipeline?

### Simple Meaning

A **Smart Serverless Automation Pipeline** means:

* You write code
* You push code to GitHub
* Pipeline runs automatically
* AWS builds and deploys your app
* No servers to manage
* Fully automated

### Real-Life Example

Like ATM machine:

* You insert card (push code)
* System processes automatically (pipeline)
* You get money (deployment done)

---

## 2️⃣ Industry Architecture (Flow)

GitHub → GitHub Actions (CI/CD) → AWS Lambda → API Gateway → CloudWatch

---

## 3️⃣ Tools Used (Industry Standard)

| Tool           | Purpose              |
| -------------- | -------------------- |
| GitHub         | Store source code    |
| GitHub Actions | Automation pipeline  |
| AWS Lambda     | Serverless compute   |
| API Gateway    | Expose API           |
| IAM            | Security permissions |
| CloudWatch     | Logs & monitoring    |

---

## 4️⃣ Step 1: Create Project Folder (Local Machine)

### Command (Terminal)

```bash
mkdir smart-serverless-pipeline
cd smart-serverless-pipeline
```

👉 **Result:** Project folder created.

---

## 5️⃣ Step 2: Create Serverless Application Code

### File Name: `lambda_function.py`

📍 **Where to create:** Inside `smart-serverless-pipeline` folder

```python
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Smart Serverless Automation Pipeline is working successfully!'
    }
```

### Explanation

* `lambda_handler` → AWS Lambda entry point
* `event` → Input request
* `context` → Runtime info

👉 **Result:** Lambda function logic ready.

---

## 6️⃣ Step 3: Test Code Locally (Optional)

```bash
python lambda_function.py
```

👉 **Result:** No error means code is correct.

---

## 7️⃣ Step 4: Create GitHub Repository

### Commands

```bash
git init
git add .
git commit -m "Initial serverless app"
```

👉 Push this repo to GitHub (new repository).

---

## 8️⃣ Step 5: Create GitHub Actions Pipeline

### Folder Structure (Very Important)

```text
smart-serverless-pipeline/
├── lambda_function.py
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 9️⃣ Step 6: GitHub Actions Pipeline Code

### File: `.github/workflows/deploy.yml`

📍 **Where to add:** Inside `.github/workflows/`

```yaml
name: Serverless CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ap-south-1

    - name: Zip Lambda function
      run: zip function.zip lambda_function.py

    - name: Deploy to AWS Lambda
      run: |
        aws lambda update-function-code \
        --function-name SmartServerlessFunction \
        --zip-file fileb://function.zip
```

---

## 🔟 Step 7: Create Lambda Function in AWS (One Time)

### Command (AWS CLI)

```bash
aws lambda create-function \
--function-name SmartServerlessFunction \
--runtime python3.9 \
--role arn:aws:iam::<ACCOUNT_ID>:role/LambdaExecutionRole \
--handler lambda_function.lambda_handler \
--zip-file fileb://function.zip
```

📍 **Where to run:** Terminal (once only)

👉 **Result:** Lambda function created.

---

## 1️⃣1️⃣ Step 8: Add GitHub Secrets

📍 **Where:** GitHub Repo → Settings → Secrets → Actions

Add:

* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`

👉 **Result:** Pipeline can access AWS securely.

---

## 1️⃣2️⃣ Step 9: Push Code to Trigger Pipeline

```bash
git push origin main
```

👉 **Result:**

* GitHub Actions pipeline starts
* Lambda code updated automatically

---

## 1️⃣3️⃣ Step 10: Expose Lambda Using API Gateway

### Create API

```bash
aws apigateway create-rest-api --name SmartServerlessAPI
```

👉 Connect API Gateway to Lambda.

👉 **Result:** Public API endpoint generated.

---

## 1️⃣4️⃣ Step 11: Test Application

### Browser or CURL

```bash
curl https://<api-id>.execute-api.ap-south-1.amazonaws.com/prod
```

👉 **Output:**

```
Smart Serverless Automation Pipeline is working successfully!
```

---

## 1️⃣5️⃣ Monitoring and Logs

### View Logs

```bash
aws logs tail /aws/lambda/SmartServerlessFunction --follow
```

👉 **Result:** Real-time execution logs.

---

## 1️⃣6️⃣ Final Project Outcome

✔️ Fully serverless application
✔️ No server management
✔️ Automated CI/CD pipeline
✔️ Secure IAM integration
✔️ Scalable and cost-efficient

---

## 1️⃣7️⃣ Resume Project Description (Industry Ready)

> "Designed and implemented a Smart Serverless Automation Pipeline using GitHub Actions and AWS Lambda, enabling automatic deployment of serverless applications on code push, with secure IAM access, API Gateway integration, and CloudWatch monitoring."

---

## 1️⃣8️⃣ Interview Explanation (Simple)

> "Whenever code is pushed to GitHub, GitHub Actions automatically packages the Lambda code and deploys it to AWS. The function is exposed through API Gateway, fully serverless, scalable, and monitored using CloudWatch."

---

## 1️⃣9️⃣ Next Enhancements (Advanced)

* Terraform for infrastructure
* DynamoDB integration
* EventBridge automation
* Multi-environment pipeline (dev/prod)
* Email alerts using SNS

---

💡 **If you want:**

* Architecture diagram image
* PDF version
* Terraform version
* MCA exam answer format

Just tell me 👍
