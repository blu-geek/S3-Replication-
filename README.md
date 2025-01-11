
# Setting Up  Cross Region Replication of S3 Buckets 

# Why Replication?
- Replication enables automatic, asynchronous copying of objects across Amazon S3 buckets. Buckets that are configured for object replication can be owned by the same AWS account or by different accounts. You can copy objects between different AWS Regions or within the same Region.
- Replicate objects while retaining metadata — You can use replication to make copies of your objects that retain all metadata, such as the original object creation time and version IDs. This capability is important if you need to ensure that your replica is identical to the source object
- Replicate objects into different storage classes — You can use replication to directly put objects into S3 Glacier, S3 Glacier Deep Archive, or another storage class in the destination bucket. You can also replicate your data to the same storage class and use lifecycle policies on the destination bucket to move your objects to a colder storage class as its ages. K21Academy Maintain object copies under different ownership — Regardless of who owns the source object, you can tell Amazon S3 to change replica ownership to the AWS account that owns the destination bucket. This is referred to as the owner override option. You can use this option to restrict access to object replicas.
- Replicate objects within 15 minutes — You can use S3 Replication Time Control (S3 RTC) to replicate your data in the same AWS Region or across different Regions in a predictable time frame. S3 RTC replicates 99.99 percent of new objects stored in Amazon S3 within 15 minutes (backed by a service level agreement).

<img width="775" alt="Screenshot 2025-01-11 at 13 43 17" src="https://github.com/user-attachments/assets/58b21734-d44a-40ad-856f-2ab93a4e7021" />

<img width="740" alt="Screenshot 2025-01-11 at 13 50 26" src="https://github.com/user-attachments/assets/9f7e1d77-d607-4e45-a24e-fa09c7757f2b" />


# Activity Guide: S3 Cross-Region Replication

1. Set Up the AWS Environment

AWS Account:
Ensure you have an active AWS account (Free or Paid).
Download Required Files:
Download and unzip necessary files.

2. Create a Source Bucket

- Open S3 Console:
Log in to the AWS Management Console, search for S3, and click Create Bucket.
- Configure Source Bucket:
Enter a unique bucket name (e.g., val-source-bucket).
Select the US East (N. Virginia) region for the bucket.
- Set Object Ownership and Access:
Disable ACLs and unblock public access.
Acknowledge the confirmation.
- Upload Files:
Upload files to the source bucket.

3. Create a Destination Bucket

- Create Bucket in a Different Region:
Name the destination bucket (e.g., k21-destination-bucket).
Choose the Asia Pacific (Mumbai) region.
- Configure Replication Settings:
Copy settings from the source bucket (except public access settings).
Disable block public access manually.

4. Create a Rule for Replication
- Enable Versioning:
Ensure versioning is enabled on both source and destination buckets.
- Configure Replication Rule:
In the source bucket, go to Management > Replication Rules > Create Rule.
Name the rule (e.g., Cross-Region-Replication-Rule).
Set the rule scope to apply to all objects.
- Select Destination Bucket:
Choose the destination bucket in the Browse S3 section.
- Assign IAM Role:
Allow AWS to create a role automatically.

5. Test the Replication

- Upload Objects to Source Bucket:
Upload new files to the source bucket.
- Verify Replication:
Open the destination bucket to confirm replication of uploaded files.
# Note: Files uploaded before the replication rule was created will not replicate.

6. Clean Up Resources

- Delete Destination Bucket:
Suspend versioning, delete all objects (including versions), and then delete the bucket.
- Delete Source Bucket:
Remove the replication rule, suspend versioning, delete objects, and then delete the bucket.

7. Troubleshooting

- Issue: Files Not Replicated:
Ensure versioning is enabled on both buckets.
- Issue: IAM Role Issues:
Verify that the IAM role associated with replication has the necessary permissions.
