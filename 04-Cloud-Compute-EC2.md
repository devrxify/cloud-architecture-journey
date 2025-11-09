### ## Personal Log: The Resource Reality

*During the EFS module, I tried to compile a complex AWS helper tool on my `t2.micro` instance. The build process was too heavy for the instance's 1GB of RAM, causing the server to completely freeze and become unresponsive. I had to force a reboot from the AWS console to get it back. This taught me that while Free Tier is great for learning, choosing the right instance size for the workload is critical in a real production environment.*

---

# Module 4: Cloud Compute - Amazon EC2

This module focused on the "engine" of the cloud: running virtual servers. I learned how to launch, connect to, and manage virtual machines using Amazon EC2 (Elastic Compute Cloud).

---

### ## 1. Core Concepts

* **EC2 Instance:** *An EC2 instance is essentially a virtual computer that I rent from Amazon's massive data centers. Instead of buying physical hardware, I can spin up a server in minutes, use it for as long as I need*
* **AMI (Amazon Machine Image):** *An AMI is the "template" or blueprint for the server. It contains the operating system (like Ubuntu 24.04 LTS) and any pre-installed software.*
* **Instance Type (e.g., t2.micro):** *This defines the actual hardware specifications of the virtual server, specifically how much CPU power and RAM it has. For example, the `t2.micro` (Free Tier eligible) has 1 vCPU and 1 GiB of memory.*
* **Key Pair:** *This is a secure digital file that acts as my master key for logging into the server. Instead of using a traditional username and password, which can be guessed or stolen, AWS uses this cryptographic key pair to authenticate my identity securely via SSH.*
* **Security Group:** *This acts as a **virtual firewall** that sits directly in front of the EC2 instance. By default, it blocks all incoming traffic. I had to explicitly add an "inbound rule" to allow SSH traffic on port 22 from my IP address so I could connect to it.*

---

