Before executing your Terraform code, you must create a key pair in AWS. Once you have created the key pair, you will receive a .pem file. Copy this file to the desired location and ensure that you remember the name of the key pair as "terraform". If you have chosen a different name for your key pair, please make sure to update the name accordingly in the subsequent steps.

## Create an AWS Key Pair for EC2 Instance


##### Step 1
- Search for “key pairs” in the **AWS console** and check the first item in the **Features** section
##### Step 2
- Create the .pem key and download it.
##### Step 3
- copy the key to current directory and change permission 
```
cp ~/KeyName.pem .
chmod 400 KeyName.pem
```


