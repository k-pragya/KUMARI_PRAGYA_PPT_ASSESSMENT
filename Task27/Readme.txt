TASK 3 — IAM + RBAC + Least Privilege (AWS + Azure)

Objective: Implement role-based access control (RBAC) with least privilege policies in AWS IAM and Azure Entra ID.

AWS Steps (IAM & Least Privilege):

Create IAM User:

Go to AWS IAM → Users → Create User → Name: Developer
Access type: Console/Programmatic (as needed)
Attach Managed Policy:
Policy: AmazonEC2FullAccess
Ensures EC2 operations are allowed

2. Create Custom Policy:

Deny S3 Delete permission:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "*"
    }
  ]
}

3. Attach Policy via Role (Optional):

Create IAM Role → Attach custom policy
Assign user Developer to role

4. Test Permissions:

EC2 access → Allowed
S3 delete → Denied

Azure Steps (Entra ID & RBAC):

1. Create User in Entra ID:

Azure Portal → Microsoft Entra ID → Users → New user → Assign name

2. Assign Roles (Least Privilege):

Reader Role → Resource Group (read-only access)

Contributor Role → Specific VM (full actions on one VM only)

3. Test Permissions:

Verify allowed actions: VM operations, resource viewing

Verify restricted actions: Deleting resources outside assigned scope