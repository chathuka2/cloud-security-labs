# Day 3: AWS IAM Lab — Users, Groups, Policies & Least Privilege

## Lab Overview
- **Lab:** Introduction to AWS Identity and Access Management (IAM)
- **Region:** `ap-northeast-1` (Asia Pacific - Tokyo)
- **Test Resources:** S3 bucket `labstack-6662601a-a356-4` and EC2 instance `i-0919402af19fb5adf`
- **Knowledge Check Result:** Passed (`1/1`, 100%)

## Key IAM Concepts Observed
- **IAM Users & Groups:** Users start with no permissions or group memberships; assigning users to groups simplifies permission management at scale.
- **Managed vs. Inline Policies:**
  - **Managed Policies** (`AmazonS3ReadOnlyAccess`, `AmazonEC2ReadOnlyAccess`) are reusable policies that apply immediately to any attached users/groups.
  - **Inline Policies** (`EC2-Admin-Policy`) are embedded directly on a single group or user for specific role requirements.
- **Policy Structure:** Statements evaluate `Effect` (`Allow`/`Deny`), `Action` (API operations), and `Resource` (target ARNs or `*`).

## Least-Privilege Role Mapping & Verification
| IAM User | IAM Group | Policy / Access Scope | Verification Results |
| :--- | :--- | :--- | :--- |
| `user-1` | `S3-Support` | `AmazonS3ReadOnlyAccess` (S3 read-only) | Listed buckets and opened `labstack-6662601a-a356-4`; restricted/no EC2 instance visibility |
| `user-2` | `EC2-Support` | `AmazonEC2ReadOnlyAccess` (EC2 read-only) | Viewed EC2 instance `i-0919402af19fb5adf`, blocked (`Not authorized`) on Stop instance, no S3 buckets listed |
| `user-3` | `EC2-Admin` | `EC2-Admin-Policy` (View, Start, Stop EC2 & view CloudWatch alarms) | Viewed EC2 instance `i-0919402af19fb5adf` and initiated Stop instance successfully |

## Security Takeaway
Enforcing least privilege through group-based policies limits blast radius—support staff get read visibility for their assigned service without administrative or cross-service privileges, while operational changes are restricted to authorized roles.
