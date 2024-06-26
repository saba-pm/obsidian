crate iam user and attach policy 
```
# Define an AWS IAM user named "lucy"
resource "aws_iam_user" "admin-user" {
  name = "lucy"  # The name of the IAM user
  tags = {       # Tags associated with the IAM user
    Description = "Technical Team Leader"
  }
}

# Define an AWS IAM policy for admin users
resource "aws_iam_policy" "adminUser" {
  name = "AdminUsers"  # The name of the IAM policy
  policy = <<EOF       # The policy document in JSON format
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",     # Allows all actions
      "Resource": "*"   # On all resources
    }
  ]
}
EOF
}

# Attach the IAM policy to the IAM user
resource "aws_iam_user_policy_attachment" "lucy-admin-access" {
  user       = aws_iam_user.admin-user.name  # The IAM user to attach the policy to
  policy_arn = aws_iam_policy.adminUser.arn  # The ARN of the policy to attach
}

```

- **resource "aws_iam_user" "admin-user"**:
    
    - Creates an IAM user named "lucy".
    - Adds a tag to describe the user's role as "Technical Team Leader".
- **resource "aws_iam_policy" "adminUser"**:
    
    - Defines an IAM policy named "AdminUsers".
    - The policy grants all actions (`"Action": "*"`) on all resources (`"Resource": "*"`) to users with this policy.
- **resource "aws_iam_user_policy_attachment" "lucy-admin-access"**:
    
    - Attaches the "AdminUsers" policy to the IAM user "lucy".


we have another way to define jison policy:
admin_policy.json:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}

```

```
# Define an AWS IAM user named "lucy"
resource "aws_iam_user" "admin-user" {
  name = "lucy"  # The name of the IAM user
  tags = {       # Tags associated with the IAM user
    Description = "Technical Team Leader"
  }
}

# Define an AWS IAM policy for admin users
resource "aws_iam_policy" "adminUser" {
  name = "AdminUsers"  # The name of the IAM policy
  policy = file("admin_policy.json") # Read the policy document from an external file
}

# Attach the IAM policy to the IAM user
resource "aws_iam_user_policy_attachment" "lucy-admin-access" {
  user       = aws_iam_user.admin-user.name  # The IAM user to attach the policy to
  policy_arn = aws_iam_policy.adminUser.arn  # The ARN of the policy to attach
}
```


- **JSON Policy File**:
    
    - Create a file named `admin_policy.json` containing the JSON policy.
- **Terraform Configuration**:
    
    - **resource "aws_iam_user" "admin-user"**: Creates an IAM user named "lucy" with tags.
    - **resource "aws_iam_policy" "adminUser"**:
        - Defines an IAM policy named "AdminUsers".
        - Uses the `file` function to read the policy document from the `admin_policy.json` file.
    - **resource "aws_iam_user_policy_attachment" "lucy-admin-access"**: Attaches the "AdminUsers" policy to the IAM user "lucy".

This approach allows you to manage the IAM policy as a separate JSON file, making it easier to edit and maintain the policy document independently of the Terraform configuration.
