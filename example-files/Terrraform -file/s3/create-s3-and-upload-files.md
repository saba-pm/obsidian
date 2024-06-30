main.tf
```
// Define an AWS S3 bucket resource named "finance"
resource "aws_s3_bucket" "finance" {
  // Specify the bucket name
  bucket = "finance-21092020"
  
  // Add tags to the S3 bucket for description purposes
  tags = {
    Description = "Finance and Payroll"
  }
}

// Define an AWS S3 bucket object resource named "finance-2020"
resource "aws_s3_bucket_object" "finance-2020" {
  // Specify the content of the object (source file path)
  content = "/root/finance/finance-2020.doc"
  
  // Specify the key (name) for the object in the bucket
  key = "finance-2020.doc"
  
  // Specify the S3 bucket where this object will be stored
  bucket = aws_s3_bucket.finance.id
}

```

1. **S3 Bucket Resource**:
    
    - The `aws_s3_bucket` resource named `finance` is created.
    - The `bucket` attribute specifies the name of the S3 bucket.
    - The `tags` block adds a description tag to the bucket for organizational purposes.
2. **S3 Bucket Object Resource**:
    
    - The `aws_s3_bucket_object` resource named `finance-2020` is created.
    - The `content` attribute specifies the local file path of the object to be uploaded.
    - The `key` attribute sets the name of the file in the S3 bucket.
    - The `bucket` attribute links this object to the `finance` bucket using its ID.

This configuration creates an S3 bucket named `finance-21092020` and uploads a file `finance-2020.doc` to this bucket


Now attach iam policy for who can access these file or how can work with that
```
// Declare a variable named "filename" with a default list of file paths
variable "filename" {
  default = [
    "/root/pets.txt", // Path for pets file
    "/root/dogs.txt", // Path for dogs file
    "/root/cats.txt", // Path for cats file
    "/root/cows.txt", // Path for cows file
    "/root/ducks.txt" // Path for ducks file
  ]
}

// Define an AWS S3 bucket resource named "finance"
resource "aws_s3_bucket" "finance" {
  // Specify the bucket name
  bucket = "finance-21092020"
  
  // Add tags to the S3 bucket for description purposes
  tags = {
    Description = "Finance and Payroll" // A tag to describe the bucket's purpose
  }
}

// Define an AWS S3 bucket object resource named "finance-2020"
resource "aws_s3_bucket_object" "finance-2020" {
  // Specify the content of the object (source file path)
  content = "/root/finance/finance-2020.doc" // Path to the local file to be uploaded
  
  // Specify the key (name) for the object in the bucket
  key = "finance-2020.doc" // The name of the file in the S3 bucket
  
  // Specify the S3 bucket where this object will be stored
  bucket = aws_s3_bucket.finance.id // Reference the "finance" bucket's ID
}

// Define a data source for an AWS IAM group named "finance-analysts"
data "aws_iam_group" "finance-data" {
  // Specify the name of the IAM group
  group_name = "finance-analysts"
}

// Define an AWS S3 bucket policy resource named "finance-policy"
resource "aws_s3_bucket_policy" "finance-policy" {
  // Specify the S3 bucket to which this policy will apply
  bucket = aws_s3_bucket.finance.id

  // Define the policy in JSON format
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": "*", // Allow all actions
      "Effect": "Allow", // Allow these actions
      "Resource": "arn:aws:s3:::${aws_s3_bucket.finance.id}/*", // Apply to all objects in the finance bucket
      "Principal": {
        "AWS": [
          "${data.aws_iam_group.finance-data.arn}" // Allow actions for the finance-data IAM group
        ]
      }
    }
  ]
}
EOF
}

```

1. **Data Source Declaration**:
    
    - `data "aws_iam_group" "finance-data"`: Declares a data source to fetch information about an existing IAM group named `finance-analysts`.
    - `group_name = "finance-analysts"`: Specifies the name of the IAM group to fetch.
2. **S3 Bucket Policy Resource**:
    
    - `resource "aws_s3_bucket_policy" "finance-policy"`: Declares a new S3 bucket policy resource named `finance-policy`.
    - `bucket = aws_s3_bucket.finance.id`: Specifies the ID of the S3 bucket to which this policy will apply.
    - `policy = <<EOF ... EOF`: Defines the bucket policy in JSON format.
        - `"Version": "2012-10-17"`: Specifies the version of the policy language.
        - `"Statement"`: Contains the policy statement.
            - `"Action": "*"`: Allows all actions.
            - `"Effect": "Allow"`: Allows the specified actions.
            - `"Resource": "arn:aws:s3:::${aws_s3_bucket.finance.id}/*"`: Specifies the resource ARN for all objects in the `finance` bucket.
            - `"Principal"`: Specifies the principal (IAM entity) allowed to perform the actions.
                - `"AWS": ["${data.aws_iam_group.finance-data.arn}"]`: Allows the `finance-analysts` IAM group to perform the actions on the bucket.

### Summary:

This combined Terraform configuration creates an S3 bucket, uploads a file to the bucket, and applies a bucket policy that grants the `finance-analysts` IAM group permission to perform all actions on the objects in the bucket. The variable `filename` is also declared, although it is not directly used in the new additions.