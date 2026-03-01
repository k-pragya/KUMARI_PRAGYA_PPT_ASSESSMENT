Task 6: S3 Replication and Lifecycle Policy

Simple Definition
Configure replication and lifecycle rules in S3 to automate data redundancy and storage cost management.

Objective
Understand cost optimization and backup strategies by managing object transitions and cross-bucket replication.

Steps Involved
1. Versioning: Enabled versioning on both source and destination buckets to maintain object history and meet replication requirements.
2. Replication Rule (RRI): Set up an automated rule to replicate all objects from the source bucket to a target destination bucket using a dedicated IAM role.
3. Lifecycle Management (LFCI): Created a rule to automate storage class transitions for cost efficiency:
   - Current Versions: Move to Standard-IA (30 days) and Expire (60 days).
   - Noncurrent Versions: Move to Standard-IA (40 days) and eventually delete.
4. Redundancy Check: Verified that objects uploaded to the source were successfully copied to the destination bucket.

 Proof Of Completion
* S3 Management Screenshot: Showing the RRI replication rule in an Enabled state.
* Lifecycle Rule Screenshot: Showing the LFCI transitions and expiration timelines.
* Replication Proof: Screenshot of the destination bucket containing replicated objects.