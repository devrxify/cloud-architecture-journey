### Personal Log: The EFS Nightmare

The S3 (Object) and EBS (Block) labs were straightforward, but the EFS (File) lab was a massive challenge. It took me a 3-4 days to solve.

**The Problem:** My servers could not mount the EFS drive and kept giving `Connection timed out` or `mount.nfs4: mount point... does not exist` errors.

**What I did:**
1.  I used `telnet` to prove it was a network block.
2.  I checked my **Security Group (EC2)** and **Network ACL (NACL)**. They were both correct.
3.  The final problem was the **EFS Mount Target's** own Security Group. It wasn't allowing inbound `NFS` traffic from my EC2 instances. I had to add a rule to allow my EC2 Security Group as a source.
4.  All my efforts on Server_1 as I told ya that I was learning linux as well so Idk about Linux libararies, so I talked to an AWS expert in Discord (We met accidently while playing Minecraft lmao ), he helped me alot in this process. Used Gemini AI, but couldn't get the concept.
5. After mounting the EFS file in Server_1 I moved to mount same file in Server_2, and thanks to my free tier AWS, Server_2 kept getting crash :_). My `t2.micro` server (with only 1GB RAM) wasn't powerful enough to compile the `amazon-efs-utils` helper tool.
ENJOY THE NOTES ><

---

# Module 3: Cloud Storage - Amazon S3 (Object Storage)

Cloud storage is the "filing cabinet" and "warehouse" of the internet. It's where applications store and access data, from user profile pictures to massive scientific datasets. Unlike the single hard drive in your laptop, cloud storage is designed to be incredibly durable, scalable, and accessible from anywhere.

---

###  1. What is Object Storage (Amazon S3)?

* *A system for storing massive amounts of unstructured data. Data isn't stored in folders but as individual objects, each with a unique ID, metadata (data about the data), and the data itself (like a photo or a video file).
Think of a giant valet parking service for data. You give the valet your car (your data), and they give you a unique ticket (the object ID). You don't know or care where they park it you only need the ticket to get your exact car back. The lot is infinitely large, and they can handle any type of vehicle.*

---

###  2. Key S3 Concepts Practiced

* **Buckets:** *A bucket is a container for your data. Think of it as a main folder for a project. The most important rule is that its name must be globally unique, like a website domain name. No two people in the world can have an S3 bucket with the same name.*
* **Objects:** *An object is the actual data you store in a bucket. It's essentially a file, but it also includes metadata (data about the file, like its size, last modified date, etc.).*
* **Presigned URLs:** *This is a secure way to grant temporary access to a private object. Instead of making your file public for everyone, you generate a special, time limited link. It's like a temporary guest pass that expires after a set time, making it perfect for secure, short term sharing.*
* **Versioning:** *This is a safety net for your data. When you enable versioning, S3 keeps a complete history of every version of a file. If you accidentally delete or overwrite an object, you can easily restore a previous version. Think of it as a super powered "undo" button for your storage.*
* **Resource Cleanup:** *This is the professional habit of deleting resources you no longer need to avoid clutter and costs. For a versioned bucket, this is a two step process: you first have to delete the "delete marker" and all the old versions of an object before you can delete the bucket itself.*

---

###  3. The Other Storage Types (A Preview)

* **Block Storage (EBS):** *Block Storage provides raw blocks of storage that function as a virtual hard drive for a cloud server (like an EC2 instance).*
* **File Storage (EFS):** *File Storage provides a shared network drive that multiple servers can connect to and use at the same time. It uses a familiar folder and file hierarchy.*
