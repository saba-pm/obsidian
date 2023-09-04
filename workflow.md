- [ ] Create a key pair in the AWS console.
- [ ] Create an EC2 instance.
- [ ] Add your script to the instance using user data.
- [ ] Open port 80 to allow access to the default Nginx path.
### To achieve this, follow these steps:

##### Step 1: Key Pair Creation 
- [ ] Go to the AWS console and navigate to the EC2 service.
- [ ] Under "Network & Security", select "Key Pairs". 
- [ ] Click on "Create Key Pair" and provide a name for your key pair. 
- [ ] Download and save the private key file (terraform.pem) securely. 
##### Step 2: EC2 Instance Creation 
- [ ] Use Terraform to define your infrastructure configuration.
- [ ] Create a file named "[main.tf](https://main.tf/)" and specify the necessary resources, including the EC2 instance with desired specifications. 
##### Step 3: Adding Script using User Data 
- [ ] In your Terraform configuration, add user data to execute a script on instance launch. 
- [ ] Create a file containing your script (e.g., hello_world.sh).
- [ ] In "[main.tf](https://main.tf/)", include user data in the EC2 resource block, referencing the script file.
##### Step 4: Opening Port 80
- [ ] Modify your Terraform configuration ([main.tf](https://main.tf/)) to include a security group rule allowing inbound traffic on port 80. 
- [ ] Specify an ingress rule for port 80 in the security group associated with your EC2 instance.
#####  Step 5: Run Terraform

- [ ]  Run `terraform init` 
- [ ] Run ``` terraform validate ```
- [ ] Run ``` terraform plan ``` 
- [ ] Run `terraform apply` 