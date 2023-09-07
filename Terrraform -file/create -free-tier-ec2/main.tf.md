
```terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-1"
}

module "ami-ubuntu" {
  source  = "andreswebs/ami-ubuntu/aws"
  version = "1.1.0"
}

resource "aws_instance" "app_server" {
  ami           = module.ami-ubuntu.ami_id
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Instance"
  }
  root_block_device {
    volume_type           = "gp2"
    volume_size           = 8
    delete_on_termination = true
  }
  ebs_block_device {
    device_name           = "/dev/sda1"
    delete_on_termination = true
    volume_size           = 8
    volume_type           = "gp2"
  }

}
