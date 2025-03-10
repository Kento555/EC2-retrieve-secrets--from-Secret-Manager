# EC2-retrieve-secrets--from-Secret-Manager
EC2 to retrieve secrets from the AWS Secret Manager

To authorize an EC2 instance to retrieve secrets from AWS Secrets Manager, you'll need to perform the following:

Create an IAM Role for your EC2 instance with permissions to access Secrets Manager.
Attach the IAM Role to the EC2 instance.
Ensure that the EC2 instance's IAM role has the appropriate permissions to call secretsmanager:GetSecretValue for the specific secret.

2️⃣ IAM Policy (JSON) to Allow EC2 to Retrieve Secrets from Secrets Manager
The IAM policy should allow the EC2 instance to perform the secretsmanager:GetSecretValue action on the specified secret.

Here's the IAM policy that grants EC2 permissions to retrieve the secret prod/cart-service/credentials:
