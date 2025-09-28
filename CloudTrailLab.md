# Lab: Monitor AWS Activity with CloudTrail (Multi-Region)
Objective

In this lab, you will set up AWS CloudTrail to log API activity across multiple regions. You will then verify the logs in an S3 bucket by performing actions in a different region.

## Steps
### Step 1: Create a CloudTrail Trail

1. Sign in to the AWS Management Console.
2. Navigate to CloudTrail.
3. Click Create trail.
4. Click the 3 lines -> go to Trails -> Create trail
5. Enter a Trail name (e.g., multi-region-trail).
- Under Storage location, choose Create new S3 bucket and provide a unique name (e.g., cloudtrail-lab-logs-<yourname>) or choose an existing bucket.
- Log file SSE-KMS encryption - disable it for the lab. If you choose to enable it a EKS customer managerd key will be created in KMS that will be used to encrypt and decrypt the data.
- Keep Additional settings as default
- explore CloudWatch Logs option, enable it and choose the appropriate role and log group name.
- Click Next
- Here you will see option to collect different types of event, choose default and click next
6. Create trail.

### Step 2: Verify Log Storage in S3

1. Go to the S3 Console.
2. Open the bucket you created (e.g., cloudtrail-lab-logs-<yourname>).
3. Wait a few minutes and check for the first set of CloudTrail log files being delivered.

### Step 3: Generate Activity in a Different Region

1. Switch to a different AWS region (e.g., from N. Virginia to Mumbai).
2. Perform an activity, such as launching a new EC2 instance:
3. Go to EC2 Console.
4. Click Launch Instance and configure a minimal instance (e.g., Amazon Linux 2, t2.micro).
5. Launch the instance.

### Step 4: Validate Multi-Region Logging

1. Return to the S3 bucket where your CloudTrail logs are stored.
2. Navigate through the log folder structure and verify the new oject created for the other region.
