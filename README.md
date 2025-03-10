# EC2-retrieve-secrets--from-Secret-Manager   
EC2 to retrieve secrets from the AWS Secret Manager   
   
1️⃣ To authorize an EC2 instance to retrieve secrets from AWS Secrets Manager, need to perform the following:   
   
- Create an IAM Role for your EC2 instance with permissions to access Secrets Manager.   
- Attach the IAM Role to the EC2 instance.   
- Ensure that the EC2 instance's IAM role has the appropriate permissions to call secretsmanager:GetSecretValue for the specific secret.   
   
2️⃣ IAM Policy (JSON) to Allow EC2 to Retrieve Secrets from Secrets Manager      
   
- The IAM policy should allow the EC2 instance to perform the secretsmanager:GetSecretValue action on the specified secret.
- Here's the IAM policy that grants EC2 permissions to retrieve the secret prod/cart-service/credentials:   
   

IAM Policy JSON Example:
```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "secretsmanager:GetSecretValue",
            "Resource": "arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-*"
        }
    ]
}
```

Explanation:   
Effect: "Allow" – This allows the action.
Action: "secretsmanager:GetSecretValue" – This grants the ability to retrieve a secret value from Secrets Manager.

   
Resource: The ARN for the specific secret you want the EC2 instance to access.
In this case, for the secret named prod/cart-service/credentials, the ARN will be arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-*.
   
prod/cart-service/credentials is the secret name.
The * is a wildcard that matches all versions of the secret (Secrets Manager versioning).
   

3️⃣ Deriving the ARN for the Specific Secret:

```
arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-*```
```
   
- **arn**: The standard identifier prefix.
- **aws**: The AWS partition.
- **secretsmanager**: The service name.
- **us-east-1**: The **AWS region** where your secret is stored.
- **123456789012**: Your **AWS account ID**.
- **secret**: The resource type.
- **prod/cart-service/credentials**: The **secret name**.
- `*` is a wildcard representing any version of the secret.


4️⃣ How to Attach IAM Policy to EC2 Role**

1. Create an IAM **role** that the EC2 instance will assume.
2. Attach the IAM policy (above) to the EC2 role.
3. When launching your EC2 instance, assign the IAM role to the instance.
   
### **Testing Access**
   
After attaching the IAM role to the EC2 instance, you can use the AWS SDK or CLI on the EC2 instance to verify that the secret can be retrieved:
   
```bash
aws secretsmanager get-secret-value --secret-id prod/cart-service/credentials
```
---


