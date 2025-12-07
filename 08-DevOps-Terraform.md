# Module 8: DevOps - Infrastructure as Code (Terraform)

In this module, I moved from "ClickOps" (manual AWS Console work) to **Infrastructure as Code (IaC)**. I used **Terraform** to automate the provisioning of a complete cloud environment.

---

### 1. Core Concepts

* **Infrastructure as Code (IaC):** Treating infrastructure (servers, networks) like software. Instead of clicking buttons, I write a "Blueprint" file, and Terraform builds it.
* **Terraform Workflow:**
    * **Init:** Download the AWS plugins.
    * **Plan:** Preview what will be built (Safety check).
    * **Apply:** Actually build the resources in the cloud.
    * **Destroy:** Delete everything in one command.
* **State File:** Terraform keeps a file (`terraform.tfstate`) that remembers every resource it created, so it knows exactly what to manage or delete later.

---

### 2. The Architecture I Built (Code)

I wrote a Terraform script to build a custom VPC with a Public Subnet, Internet Gateway, and an EC2 instance protected by a Security Group.

**My `main.tf` Blueprint:**

```hcl
provider "aws" {
  region = "eu-north-1"
}

# 1. The Network (VPC)
resource "aws_vpc" "my_capstone_vpc" {
  cidr_block = "10.0.0.0/16"
  tags = { Name = "Terraform-VPC" }
}

# 2. The Subnet (Public)
resource "aws_subnet" "my_public_subnet" {
  vpc_id            = aws_vpc.my_capstone_vpc.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "eu-north-1a"
  tags = { Name = "Terraform-Public-Subnet" }
}

# 3. The Internet Gateway
resource "aws_internet_gateway" "my_igw" {
  vpc_id = aws_vpc.my_capstone_vpc.id
}

# 4. The Security Group (Firewall)
resource "aws_security_group" "my_sg" {
  name   = "allow_ssh"
  vpc_id = aws_vpc.my_capstone_vpc.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# 5. The Server
resource "aws_instance" "my_server" {
  ami                    = "ami-09a9858973b288bdd" # Ubuntu 24.04 (Stockholm)
  instance_type          = "t3.micro"
  subnet_id              = aws_subnet.my_public_subnet.id
  vpc_security_group_ids = [aws_security_group.my_sg.id]

  tags = { Name = "Terraform-Capstone-Server" }
}
