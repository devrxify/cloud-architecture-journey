### ## 💡 Personal Log: The Setup Struggle

This module was my first real test. It took me several hours of hands on work to get a stable lab. I ran into many errors:
* My first attempt with **VirtualBox** failed, and the Ubuntu Server installer kept crashing with a `curtin` error.
* After switching to **VMware**, I installed Ubuntu Desktop but my first user (`aspect`) was created without `sudo` privileges, locking me out. I had to learn to fix this by reinstalling and unchecking "unattended setup." 
(You can say that I was basically learning the linux too :) )
Here are some quick notes on Virtuallization which I learned and gather form various sources. Hope It will help ; ).

---

# Module 2: Virtualization Concepts (VMs vs. Containers)

*A Virtual Machine (VM) is an entire computer (virtual hardware + its own operating system) running on a host machine. It's powerful but heavy.*
*A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.*

---

### ## 1. Understanding Virtual Machines (VMs)

* **What they are:** *A virtual machine (VM) is a software based computer that functions like a physical computer. It's a digitized version of a physical machine, allowing you to run different operating systems and applications on a single physical server. Essentially, VMs enable multiple "guest" machines to run on a single "host" machine.*
* **Analogy:** *A VM is a complete house with its own foundation, plumbing, electrical, and rooms (the guest OS and all its files)*

---

### ## 2. Understanding Containers

* **What they are:** *Containers are a form of operating system level virtualization that packages up an application and its dependencies into a single, portable unit. They provide a consistent and isolated environment for running applications, regardless of the underlying infrastructure.*
* **Analogy:** *If a VM is a complete house with its own foundation, plumbing, electrical, and rooms (the guest OS and all its files)—then a Container is an apartment in a large building.*

---

### ## 3. Key Differences at a Glance

* **Size & Speed:** *VMs are heavy (Gigabytes) & Slow (Minutes) while Containers are lightweight (Megabytes) and Fast (Seconds or less)*
* **Resource Overhead:** *VMs: High (runs a full guest OS) |	Containers: Low (shares the host OS kernel)*
* **Isolation:** *VMs: Virtualizes the Hardware |	Containers: Virtualizes the Operating System*

---

### ## 4. When to Use Which?

* **Use a VM when...**
    * *1. Running Different Operating Systems on a Single Server*
    * *2. High Security and Multi Tenant Environments...because VMs provide strong, hardware level isolation between users.*
    * *3. Running Legacy Applications......because a VM can perfectly replicate an old operating system that the application depends on*

* **Use a Container when...**
    * *1. Microservices Architecture......because each service can be packaged and scaled independently in its own lightweight container.*
    * *2. Solving the "It works on my machine" Problem*
    * *3. CI/CD and DevOps Automation* 
