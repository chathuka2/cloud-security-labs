# Day 5: Least-Privilege IAM Policy Simulation & Sandbox Guardrails

## Objective
Verify least-privilege access enforcement and IAM default/implicit deny behavior using the AWS IAM Policy Simulator, while documenting real-world sandbox guardrails in an AWS Skill Builder lab environment.

## Environment & Context
- **Lab Environment:** AWS Skill Builder (`Introduction to AWS Identity and Access Management (IAM)`)
- **Session Identity:** `AWSLabsUser-...` (sandboxed lab session)
- **Custom Simulation Policy:** `Day05-LeastPrivilege-S3ReadOnly` (`s3:ListBucket` and `s3:GetObject` scoped to `arn:aws:s3:::least-privilege-lab-target` and `arn:aws:s3:::least-privilege-lab-target/*`)

## Policy Reference (`Day05-LeastPrivilege-S3ReadOnly`)
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowReadOnlyTargetBucket",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::least-privilege-lab-target",
        "arn:aws:s3:::least-privilege-lab-target/*"
      ]
    }
```
<img width="1920" height="1080" alt="Screenshot (969)" src="https://github.com/user-attachments/assets/616ef99d-ebdb-4317-96c7-6867f306d7d2" />
