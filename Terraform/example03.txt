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
  region = "us-east-2"
}

resource "aws_instance" "app_server_name" {
  ami           = "ami-0c7c4e3c6b4941f0f"
  instance_type = "t2.micro"

  tags = {
    Name = "Example-AWS-Instance"
  }
}