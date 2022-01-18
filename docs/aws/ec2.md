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

## EC2 instance

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
|-------------------|----------|---------|-------------------|---------------|
| - t2              |  - c4    |  - r3   | - i2                | - g2            |
| - m4                |  - c3    |  - x1   | - d2                |               |  
| - m3                |          |         |                   |               |  


---

##  EC2 Pricing

Amazon EC2 instances are priced per second according to five different options:

- On-demand
- Spot instances (discounted short-term capacity if available)
- Savings Plans (commitment to a certain amount of usage)
- Reserved Instances (discounted reserved long-term capacity)
- Dedicated Hosts (on-demand hourly or by reserved instances)




---

##  Launch an on-demand EC2 instance in AWS Cloud


###  Step 1. Login and access to AWS services

Login to your AWS account and go to the AWS Services tab at the top left corner.
Here, you will see all of the AWS Services categorized as per their area viz. Compute, Storage, Database, etc. For creating an EC2 instance, we have to choose Computeà EC2 as in the next step.

<img src="images/ec2-Step1.png" width="900"/>

Open all the services and click on EC2 under Compute services. This will launch the dashboard of EC2.


Here is the EC2 dashboard. Here you will get all the information in gist about the AWS EC2 resources running.

<img src="images/ec2-step1-EC2 dashboard.png" width="900"/>



###  Step 2. Choose the AWS Region

On the top right corner of the EC2 dashboard, choose the AWS Region in which you want to provision the EC2 server.

Here we are selecting N. Virginia. AWS provides 10 Regions all over the globe.

<img src="images/ec2-step2-AWS Region.png" width="900"/>


###  Step 3.Launch Instance

Once your desired Region is selected, come back to the EC2 Dashboard.

Click on ‘Launch Instance’ button in the section of Create Instance (as shown below).

<img src="images/ec2-step3-Launch Instance.png" width="900"/>

Instance creation wizard page will open as soon as you click ‘Launch Instance’.

###  Step 4. Choose AMI


- You will be asked to choose an AMI of your choice. (An AMI is an Amazon Machine Image. It is a template basically of an Operating System platform which you can use as a base to create your instance). Once you launch an EC2 instance from your preferred AMI, the instance will automatically be booted with the desired OS. (We will see more about AMIs in the coming part of the tutorial).
- Here we are choosing the default Amazon Linux (64 bit) AMI.

<img src="images/ec2-stap4-Choose AMI.png" width="900"/>


###  Step 5.



###  Step 6.





---

## Links: 

1. [How to Create EC2 Instance in AWS: Step by Step Tutorial](https://www.guru99.com/creating-amazon-ec2-instance.html)
2. [AWS - Elastic Compute Cloud](https://www.tutorialspoint.com/amazon_web_services/amazon_web_services_elastic_compute_cloud.htm)
3. [EC2](https://www.javatpoint.com/aws-ec2)
