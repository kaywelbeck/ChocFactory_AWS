# Steps to Create an S3 Bucket on AWS

## Step 1: Log in to AWS Management Console
- Go to the AWS Management Console.
- Log in with your credentials.

## Step 2: Navigate to S3
- In the AWS Management Console, type S3 in the search bar and select S3 from the services list.

## Step 3: Create a Bucket
- Click on the **Create bucket** button.

## Step 4: Configure Bucket Settings
- **Bucket Name:** Enter a unique name for your bucket (e.g., `chocfactory-bucket`). The name must be globally unique across all of AWS.
- **Region:** Choose the AWS region where you want the bucket to be created. It's typically best to choose the same region as your other resources (like your RDS instance) for latency and cost efficiency.
- **Object Ownership:** Set to ACLs disabled (recommended) for better security.

## Step 5: Configure Options (Optional)
- **Versioning:** Enable versioning if you want to keep multiple versions of an object (this can be useful for backups).
- **Logging:** You can enable server access logging if you want to track requests to the bucket.
- **Tags:** You can add tags for organization and cost tracking.

## Step 6: Set Permissions
- **Block Public Access Settings:**  
  It’s recommended to leave all four options enabled to block public access unless you specifically need your bucket to be public (for static website hosting, for example).
- **Bucket Policy:** You can set a bucket policy later if you need to allow specific users or services access to the bucket.

## Step 7: Review and Create
- Review all your settings to ensure they are correct.
- Click **Create bucket**.

## Step 8: Verify the Bucket
- Once created, you should see your new bucket listed in the S3 dashboard.
- You can click on the bucket name to open it and configure further settings, upload files, or manage permissions.
