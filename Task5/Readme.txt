Task 5: Static Website Hosting in Amazon S3
Objective

Step 1: Create S3 Bucket
        Go to S3 → Create bucket → give a unique name.
        Uncheck Block all public access.
        Click Create.

Step 2: Upload File
        Open bucket → Upload index.html and assets.
        Ensure index.html is at the root.

Step 3: Set Permissions
        Permissions → Bucket Policy → Edit.
        Add JSON policy (replace YOUR-BUCKET-NAME):
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}

Step 4: Enable Static Website Hosting
        Properties → Static website hosting → Enable.
        Index document: index.html.
        Copy Bucket website endpoint.

Step 5:Test
       Paste endpoint in browser:
       http://<bucket-name>.s3-website-<region>.amazonaws.com

Proof of Completion

Screenshot of the S3 bucket with files uploaded.
Screenshot of the Bucket Policy applied.
Screenshot of the website opened in a browser.
