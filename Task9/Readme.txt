# Task 9: Access S3 from Ubuntu using IAM Roles & Policies

Simple Definition
Grant an EC2 instance permission to access Amazon S3 securely using IAM Roles instead of access keys.

Objective
Learn how to use IAM Policies and IAM Roles to allow secure S3 access from an EC2 Ubuntu instance.

Steps Involved

1. IAM Policy Creation:
   - Logged in to AWS Management Console.
   - Navigated to IAM → Policies → Create Policy.
   - Selected JSON or Visual Editor.
   - Allowed all S3 actions (for testing purpose).
   - Named the policy: S3-AllAccess.
   - Saved the policy.

2. IAM Role Creation:
   - Navigated to IAM → Roles → Create Role.
   - Selected trusted entity type: AWS Service.
   - Selected service: EC2.
   - Attached policy: S3-AllAccess.
   - Named the role: MyEC2Role.
   - Created and saved the role.

3. Launch EC2 Instance:
   - Launched a new Ubuntu/Linux EC2 instance.
   - During configuration, attached IAM role: MyEC2Role.
   - Connected to the instance using SSH.

4. Verify S3 Access:
   - Checked AWS CLI installation:
     aws --version
   - Attempted to list S3 buckets:
     aws s3 ls
   - Without IAM role, the command fails due to permission error.
   - Attached IAM role via:
     EC2 → Actions → Security → Modify IAM Role → Select MyEC2Role.
   - Re-ran the command:
     aws s3 ls
   - Successfully listed accessible S3 buckets.

5. Test S3 Operations:
   - Created or accessed an existing S3 bucket.
   - Uploaded files using:
     aws s3 cp filename.txt s3://bucket-name/
   - Listed objects inside bucket:
     aws s3 ls s3://bucket-name/
