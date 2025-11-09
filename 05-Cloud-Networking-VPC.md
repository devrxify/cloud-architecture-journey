### ## Personal Log: The Hidden Cost Trap
In this module, I set up a custom VPC private network. Gone through simple step and boom : ). Just delete the "NAT Gateway" before deleteing the VPC.


# Module 5: Cloud Networking - Amazon VPC

This module was about building a private, isolated network in the cloud. Instead of using the default public network, I architected a custom Virtual Private Cloud (VPC) from scratch.

---

### ## 1. Core Networking Components

* **VPC (Virtual Private Cloud):** A VPC is my own private, isolated section of the AWS cloud. It's like building a secure wall around my cloud resources, giving me complete control over the IP address range and who is allowed to enter or leave the network.
* **Subnet:** A subnet is a smaller, segmented "neighborhood" inside the VPC, usually located in a specific Availability Zone.
* **Public Subnet:** Has a direct route to the Internet Gateway, allowing servers inside it to talk to the internet.
* **Private Subnet:** Does NOT have a direct route to the internet, making it more secure for things like databases.
* **Internet Gateway (IGW):** This is the "secure gate" that connects my private VPC to the outside internet. Without an attached IGW, resources inside the VPC cannot be reached from the web, even if they have public IPs.
* **Route Table:** These are the "traffic signs" for the network. They tell data packets where to go. For a subnet to be public, its route table must have a rule sending all internet-bound traffic (`0.0.0.0/0`) to the Internet Gateway.


