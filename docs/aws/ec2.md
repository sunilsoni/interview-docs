---
layout: default
title: AWS EC2
parent: Amazon Web Services (AWS)

---

# AWS - Elastic Compute Cloud (EC2)
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

Amazon EC2 provides cloud hosted virtual machines, called `instances`, to run applications.

---

##EC2 instance

An EC2 instance is nothing but a virtual server in Amazon Web services terminology. It stands for Elastic Compute Cloud. It is a web service where an AWS subscriber can request and provision a compute server in AWS cloud.

An on-demand EC2 instance is an offering from AWS where the subscriber/user can rent the virtual server per hour and use it to deploy his/her own applications.

The instance will be charged per hour with different rates based on the type of the instance chosen. AWS provides multiple instance types for the respective business needs of the user.

Thus, you can rent an instance based on your own CPU and memory requirements and use it as long as you want. You can terminate the instance when it’s no more used and save on costs. This is the most striking advantage of an on-demand instance- you can drastically save on your CAPEX.


---

## Types of EC2 Computing Instances


| Instances Types   | Use Case | Example |
|-------------------|----------|---------|
| General Instances | For applications that require a balance of performance and cost.| email responding systems, where you need a prompt response as well as the it should be cost effective, since it doesn’t require much processing.|
| Compute Instances | For applications that require a lot of processing from the CPU.         |   analysis of data from a stream of data, like Twitter stream      |
| Memory Instances  | For applications that are heavy in nature, therefore, require a lot of RAM.         | when your system needs a lot of applications running in the background i.e multitasking.       |
| Storage Instances |  For applications that are huge in size or have a data set that occupies a lot of space.        |  When your application is of huge size.       |
| GPU Instances     |  For applications that require some heavy graphics rendering.        | 3D modelling etc.       |


Now, every instance type has a set of instances which are optimized for different workloads:


| General Instances | Compute Instances |  Memory Instances | Storage Instances | GPU Instances | 
|-----------------|----------|---------|---------|---------|
| t2         |  c4    |  r3   | i2| g2 |
| m4         |  c3    |  x1   | d2|  |  
| m3         |          |         |  |  |  


---

## 

---

## Links: 

1. [How to Create EC2 Instance in AWS: Step by Step Tutorial](https://www.guru99.com/creating-amazon-ec2-instance.html)
2. [AWS - Elastic Compute Cloud](https://www.tutorialspoint.com/amazon_web_services/amazon_web_services_elastic_compute_cloud.htm)
3. [EC2](https://www.javatpoint.com/aws-ec2)
