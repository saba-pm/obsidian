```
variable "region" {
  default = "us-east-1"
}
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
    region  = var.region
}


module "ami-ubuntu" {

  source = "andreswebs/ami-ubuntu/aws"

   version = "1.1.0"

}

module "ec2_instances" {
    source = "terraform-aws-modules/ec2-instance/aws"
    version = "3.5.0"
    count = 1

    name = "ec2-nginx-demo"

    ami = module.ami-ubuntu.ami_id
    instance_type = "t2.micro"
    vpc_security_group_ids = [aws_security_group.nginx_demo.id]
    key_name = var.key_name
    user_data = file("userdata.tpl")

    tags = {
        Name = "NginxDemo"
    }
}

resource "aws_default_vpc" "default" {

}

resource "aws_security_group" "nginx_demo" {
    name = "nginx_demo"
    description = "SSH on port 22 and HTTP on port 80"
    vpc_id = aws_default_vpc.default.id

    ingress {
        from_port = 22
        to_port = 22
        protocol = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
    }

    ingress {
        from_port = 80
        to_port = 80
        protocol = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
    }

    egress {
        from_port        = 0
        to_port          = 0
        protocol         = "-1"
        cidr_blocks      = ["0.0.0.0/0"]
    }
}
```