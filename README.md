
# AWS Compute 

---

## Nội dung chính

Module này giới thiệu và thực hành các dịch vụ compute & storage cốt lõi của AWS:

* **Compute:** Amazon EC2, AMI, Lightsail, Auto Scaling, Elastic Load Balancing
* **Storage:** Amazon EBS, EFS, FSx (Windows, Lustre, NetApp ONTAP, OpenZFS), Amazon S3
* **So sánh với On-Premise (NAS, SAN, RAID, Data Center, Backup & DR)**

---

## Compute Services

### 🔹 Amazon EC2 (Elastic Compute Cloud)

* Máy chủ ảo linh hoạt, scale nhanh, nhiều loại instance.
* Thành phần: AMI, Instance Type, EBS, Instance Store, Key Pair, Security Group, User Data/Metadata.
* Pricing: On-Demand, Reserved, Savings Plans, Spot, Dedicated Host.
* **Use case:**

  * Web hosting, backend API.
  * Database (self-managed).
  * AI/ML training, HPC.
  * Big Data cluster (Hadoop/Spark).
  * CI/CD, test environment.
  * Disaster Recovery (AMI, snapshot).

---

### 🔹 Amazon Lightsail

* VPS đơn giản, predictable monthly cost.
* Có sẵn app template (WordPress, LAMP, Node.js).
* Bao gồm instance, storage, load balancer, DB.
* **Use case:**

  * Blog/website nhỏ.
  * Startup MVP/demo.
  * Dev/test sandbox.
  * Small e-commerce.
  * PoC workload trước khi migrate lên EC2/ECS.

---

## Storage Services

### 🔹 Amazon EBS (Elastic Block Store)

* Block storage cho 1 instance.
* SSD (gp3/io1/io2), HDD (st1/sc1).
* Snapshot lưu S3.
* **Use case:** Database, boot volume, app I/O latency thấp.

---

### 🔹 Amazon EFS (Elastic File System)

* File storage NFS cho Linux.
* Multi-AZ, auto scale, trả phí theo dùng.
* **Use case:** Web farm, microservices, container apps, user home dir, hybrid cloud.

---

### 🔹 Amazon FSx (Managed File System)

* Các loại FSx:

  * **Windows File Server:** SMB/NTFS, AD integration.
  * **Lustre:** HPC, AI/ML, big data (link S3).
  * **NetApp ONTAP:** snapshot, replication, deduplication, hybrid cloud.
  * **OpenZFS:** snapshot, clone, data integrity cho Linux/Unix.

---

### 🔹 Amazon S3 (Simple Storage Service)

* Object storage, durability 11x9.
* Lifecycle policies, cross-region replication.
* **Use case:** Backup, archive, static content, data lake.

---

## So sánh Storage

| Đặc điểm       | **EBS** (Block)                 | **EFS** (File, NFS)                | **FSx** (File, enterprise/HPC)               | **S3** (Object)                        |
| -------------- | ------------------------------- | ---------------------------------- | -------------------------------------------- | -------------------------------------- |
| Kiểu lưu trữ   | Block device                    | File system (POSIX)                | File system (SMB, NFS, Lustre, iSCSI)        | Object storage                         |
| OS hỗ trợ      | Linux & Windows                 | Linux                              | Windows (SMB), Linux (NFS/ZFS/Lustre)        | Mọi hệ (API/SDK/CLI)                   |
| Multi-instance | Không (trừ Multi-Attach)        | Có (multi-EC2 mount)               | Có (multi-client access)                     | Không trực tiếp                        |
| Scale          | Resize thủ công                 | Auto scale MB → PB                 | Theo FSx type (scale-out, HA cluster)        | Auto scale “vô hạn”                    |
| HA/DR          | Snapshot, cross-AZ replicate    | Multi-AZ (Standard), One Zone      | Multi-AZ option, backup daily, replication   | Durability 11x9, CRR, versioning       |
| Use case       | DB, boot volume, low-latency IO | Web farm, microservices, log share | Windows FS, HPC Lustre, Enterprise ONTAP/ZFS | Backup, archive, static web, data lake |

---

## OOn-Prem vs AWS

### On-Prem

* **NAS (NFS/SMB, file-level)** → file share, user home dir.
* **SAN (block-level, Fibre Channel/iSCSI)** → database, ERP, HPC, virtualization.
* Backup = tape/disk → restore chậm.
* DR site = tốn kém (cold/warm/hot site).
* Quản lý rack, RAID, cooling, điện, bảo trì phần cứng.

### AWS

* **NAS** → thay bằng **EFS, FSx Windows**.
* **SAN** → thay bằng **EBS, FSx ONTAP, Instance Store**.
* **Tape archive** → thay bằng **S3, Glacier**.
* **DR site** → cross-region replication, Pilot Light, Warm Standby, Multi-Site Active/Active.
* Pay-as-you-go (OPEX), HA/DR built-in, giảm CAPEX & vận hành.

---

## Best Practices

* **EC2:** chạy đa AZ, mix pricing (On-Demand + Spot + Savings Plans), dùng IAM Role thay key.
* **Lightsail:** dùng cho small workload, migrate lên EC2 khi scale.
* **EFS:** bật Lifecycle → Infrequent Access để giảm chi phí.
* **FSx:** chọn loại theo workload (Windows/HPC/Enterprise).
* **S3:** enable versioning, lifecycle, replication.
* **Networking:** plan IP, dùng NACL + SG, Shared VPC nên tách subnet theo participant.
* **Monitoring:** bật CloudWatch, VPC Flow Logs, DNS query logs.
* **Backup/DR:** dùng AWS Backup, snapshot EBS, cross-region replication.

---

## Lab thực hành

### AWS Study Group

* [Lab tuần này – 000004](https://000004.awsstudygroup.com/vi/)
* [Lab tuần trước – 000003](https://000003.awsstudygroup.com/vi/)

Chuẩn rồi 🚀 mình sẽ bổ sung thêm **tài liệu chính thức AWS** + **link lab thực hành** để README recap của bạn đủ trọn bộ tham khảo và hands-on.

---

## Tài liệu tham khảo mở rộng

### 🔹 Compute

* [Amazon EC2 – Concepts](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
* [Amazon Machine Images (AMI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
* [Amazon Lightsail – What is Lightsail?](https://docs.aws.amazon.com/lightsail/latest/userguide/what-is-amazon-lightsail.html)
* [Amazon EC2 Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/auto-scaling-groups.html)
* [Elastic Load Balancing with Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)

### 🔹 Storage

* [Amazon Elastic Block Store (EBS)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
* [Amazon Elastic File System (EFS)](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)
* [Amazon FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)
* [Amazon FSx for Lustre](https://docs.aws.amazon.com/fsx/latest/LustreGuide/what-is.html)
* [Amazon FSx for NetApp ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/what-is.html)
* [Amazon FSx for OpenZFS](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/what-is.html)
* [Amazon S3 – Overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)





