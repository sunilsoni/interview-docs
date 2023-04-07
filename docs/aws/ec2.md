---
layout: default
title: EC2
parent: Amazon Web Services (AWS)
resource: true
desc: "AWS - Elastic Compute Cloud (EC2) interview questions and answers."
categories: [AWS - Elastic Compute Cloud (EC2)]

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


## Elastic Compute Cloud (EC2)

An EC2 instance is nothing but a virtual server in Amazon Web services terminology. It stands for Elastic Compute Cloud. It is a web service where an AWS subscriber can request and provision a compute server in AWS cloud.

An on-demand EC2 instance is an offering from AWS where the subscriber/user can rent the virtual server per hour and use it to deploy his/her own applications.

The instance will be charged per hour with different rates based on the type of the instance chosen. AWS provides multiple instance types for the respective business needs of the user.

Thus, you can rent an instance based on your own CPU and memory requirements and use it as long as you want. You can terminate the instance when it’s no more used and save on costs. This is the most striking advantage of an on-demand instance- you can drastically save on your CAPEX.


EC2 spins up resizable server instances that can scale up and down quickly. An instance is a virtual server in the cloud. With Amazon EC2, you can set up and configure the operating system and applications that run on your instance. Its configuration at launch is a live copy of the Amazon Machine Image (AMI) that you specify when you launched the instance. EC2 has an extremely reduced time frame for provisioning and booting new instances and EC2 ensures that you pay as you go, pay for what you use, pay less as you use more, and pay even less when you reserve capacity. When your EC2 instance is running, you are charged on CPU, memory, storage, and networking. When it is stopped, you are only charged for EBS storage.


### EC2 Key Details
- You can launch different types of instances from a single AMI. An instance type essentially determines the hardware of the host computer used for your instance. Each instance type offers different compute and memory capabilities. You should select an instance type based on the amount of memory and computing power that you need for the application or software that you plan to run on top of the instance.
- You can launch multiple instances of an AMI, as shown in the following figure:

<img src="images/EC2%20Key%20Details.png" width="900"/>


- You have the option of using dedicated tenancy with your instance. This means that within an AWS data center, you have exclusive access to physical hardware. Naturally, this option incurs a high cost, but it makes sense if you work with technology that has a strict licensing policy.
- With EC2 VM Import, you can import existing VMs into AWS as long as those hosts use VMware ESX, VMware Workstation, Microsoft Hyper-V, or Citrix Xen virtualization formats.
- When you launch a new EC2 instance, EC2 attempts to place the instance in such a way that all of your VMs are spread out across different hardware to limit failure to a single location. You can use placement groups to influence the placement of a group of interdependent instances that meet the needs of your workload. There is an explanation about placement groups in a section below.
- When you launch an instance in Amazon EC2, you have the option of passing user data to the instance when the instance starts. This user data can be used to run common automated configuration tasks or scripts. For example, you can pass a bash script that ensures htop is installed on the new EC2 host and is always active.
- By default, the public IP address of an EC2 Instance is released when the instance is stopped even if its stopped temporarily. Therefore, it is best to refer to an instance by its external DNS hostname. If you require a persistent public IP address that can be associated to the same instance, use an Elastic IP address which is basically a static IP address instead.
- If you have requirements to self-manage a SQL database, EC2 can be a solid alternative to RDS. To ensure high availability, remember to have at least one other EC2 Instance in a separate Availability zone so even if a DB instance goes down, the other(s) will still be available.
- A golden image is simply an AMI that you have fully customized to your liking with all necessary software/data/configuration details set and ready to go once. This personal AMI can then be the source from which you launch new instances.
- Instance status checks check the health of the running EC2 server, systems status check monitor the health of the underlying hypervisor. If you ever notice a systems status issue, just stop the instance and start it again (no need to reboot) as the VM will start up again on a new hypervisor.

### EC2 Instance Pricing
- **On-Demand instances** are based on a fixed rate by the hour or second. As the name implies, you can start an On-Demand instance whenever you need one and can stop it when you no longer need it. There is no requirement for a long-term commitment.
- **Reserved instances** ensure that you keep exclusive use of an instance on 1 or 3 year contract terms. The long-term commitment provides significantly reduced discounts at the hourly rate.
- **Spot instances** take advantage of Amazon’s excess capacity and work in an interesting manner. In order to use them, you must financially bid for access. Because Spot instances are only available when Amazon has excess capacity, this option makes sense only if your app has flexible start and end times. You won’t be charged if your instance stops due to a price change (e.g., someone else just bid a higher price for the access) and so consequently your workload doesn’t complete. However, if you terminate the instance yourself you will be charged for any hour the instance ran. Spot instances are normally used in batch processing jobs.

### Standard Reserved vs. Convertible Reserved vs. Scheduled Reserved
- **Standard Reserved Instances** have inflexible reservations that are discounted at 75% off of On-Demand instances. Standard Reserved Instances cannot be moved between regions. You can choose if a Reserved Instance applies to either a specific Availability Zone, or an Entire Region, but you cannot change the region.
- **Convertible Reserved Instances** are instances that are discounted at 54% off of On-Demand instances, but you can also modify the instance type at any point. For example, you suspect that after a few months your VM might need to change from general purpose to memory optimized, but you aren't sure just yet. So if you think that in the future you might need to change your VM type or upgrade your VMs capacity, choose Convertible Reserved Instances. There is no downgrading instance type with this option though.
- **Scheduled Reserved Instances** are reserved according to a specified timeline that you set. For example, you might use Scheduled Reserved Instances if you run education software that only needs to be available during school hours. This option allows you to better match your needed capacity with a recurring schedule so that you can save money.


### EC2 Instance Lifecycle
The following table highlights the many instance states that a VM can be in at a given time.

| Instance state | Description | Billing |
| ------------- | ------------- |--------------|
| `pending` | The instance is preparing to enter the `running` state. An instance enters the pending state when it launches for the first time, or when it is started after being in the `stopped` state.   | Not billed
| `running`  | The instance is running and ready for use.  | Billed |
| `stopping`  | The instance is preparing to be stopped or stop-hibernated.  | Not billed if preparing to stop. Billed if preparing to hibernate |
| `stopped` | The instance is shut down and cannot be used. The instance can be started at any time. | Not billed |
| `shutting-down`  | The instance is preparing to be terminated.  | Not billed |
| `terminated`  | The instance has been permanently deleted and cannot be started.  | Not billed |

**Note**: Reserved Instances that are terminated are billed until the end of their term.

### EC2 Security
- When you deploy an Amazon EC2 instance, you are responsible for management of the guest operating system (including updates and security patches), any application software or utilities installed on the instances, and the configuration of the AWS-provided firewall (called a security group) on each instance.
- With EC2, termination protection of the instance is disabled by default. This means that you do not have a safe-guard in place from accidentally terminating your instance. You must turn this feature on if you want that extra bit of protection.
- Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. Public–key cryptography uses a public key to encrypt a piece of data, such as a password, and the recipient uses their private key to decrypt the data. The public and private keys are known as a key pair.
- You can encrypt your root device volume which is where you install the underlying OS. You can do this during creation time of the instance or with third-party tools like bit locker. Of course, additional or secondary EBS volumes are also encryptable as well.
- By default, an EC2 instance with an attached AWS Elastic Block Store (EBS) root volume will be deleted together when the instance is terminated. However, any additional or secondary EBS volume that is also attached to the same instance will be preserved. This is because the root EBS volume is for OS installations and other low-level settings. This rule can be modified, but it is usually easier to boot a new instance with a fresh root device volume than make use of an old one.


### EC2 Placement Groups
-  Placement groups balance the tradeoff between risk tolerance and network performance when it comes to your fleet of EC2 instances. The more you care about risk, the more isolated you want your instances to be from each other. The more you care about performance, the more conjoined you want your instances to be with each other.
- There are three different types of EC2 placement groups:

  1.) Clustered Placement Groups
  - Clustered Placement Grouping is when you put all of your EC2 instances in a single availability zone. This is recommended for applications that need the lowest latency possible and require the highest network throughput.
  - Only certain instances can be launched into this group (compute optimized, GPU optimized, storage optimized, and memory optimized).

  2.) Spread Placement Groups
  - Spread Placement Grouping is when you put each individual EC2 instance on top of its own distinct hardware so that failure is isolated.
  - Your VMs live on separate racks, with separate network inputs and separate power requirements. Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other.

  3.) Partitioned Placement Groups
  - Partitioned Placement Grouping is similar to Spread placement grouping, but differs because you can have multiple EC2 instances within a single partition. Failure instead is isolated to a partition (say 3 or 4 instances instead of 1), yet you enjoy the benefits of close proximity for improved network performance.
  - With this placement group, you have multiple instances living together on the same hardware inside of different availability zones across one or more regions.
  - If you would like a balance of risk tolerance and network performance, use Partitioned Placement Groups.

- Each placement group name within your AWS must be unique
- You can move an existing instance into a placement group provided that it is in a stopped state. You can move the instance via the CLI or an AWS SDK, but not the console. You can also take a snapshot of the existing instance, convert it into an AMI, and launch it into the placement group where you desire it to be.


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


###  Step 3. Launch Instance

Once your desired Region is selected, come back to the EC2 Dashboard.

Click on ‘Launch Instance’ button in the section of Create Instance (as shown below).

<img src="images/ec2-step3-Launch Instance.png" width="900"/>

Instance creation wizard page will open as soon as you click ‘Launch Instance’.

###  Step 4. Choose AMI


- You will be asked to choose an AMI of your choice. (An AMI is an Amazon Machine Image. It is a template basically of an Operating System platform which you can use as a base to create your instance). Once you launch an EC2 instance from your preferred AMI, the instance will automatically be booted with the desired OS. (We will see more about AMIs in the coming part of the tutorial).
- Here we are choosing the default Amazon Linux (64 bit) AMI.

<img src="images/ec2-stap4-Choose AMI.png" width="900"/>


###  Step 5. Choose EC2 Instance Types

In the next step, you have to choose the type of instance you require based on your business needs.

- We will choose t2.micro instance type, which is a 1vCPU and 1GB memory server offered by AWS.
- Click on “Configure Instance Details” for further configurations

<img src="images/ec2-step5-Choose EC2 Instance Types .png" width="900"/>


- In the next step of the wizard, enter details like no. of instances you want to launch at a time.
- Here we are launching one instance.



###  Step 6. Configure Instance

No. of instances- you can provision up to 20 instances at a time. Here we are launching one instance.

<img src="images/ec2-step6Configure Instance .png" width="900"/>



Under Purchasing Options, keep the option of ‘Request Spot Instances’ unchecked as of now. (This is done when we wish to launch Spot instances instead of on-demand ones. We will come back to Spot instances in the later part of the tutorial).


<img src="images/ec2-step6-Configure Instance Details.png" width="900"/>


Next, we have to configure some basic networking details for our EC2 server.

- You have to decide here, in which VPC (Virtual Private Cloud) you want to launch your instance and under which subnets inside your VPC. It is better to determine and plan this prior to launching the instance. Your AWS architecture set-up should include IP ranges for your subnets etc. pre-planned for better management. (We will see how to create a new VPC in Networking section of the tutorial.
- Subnetting should also be pre-planned. E.g.: If it’s a web server you should place it in the public subnet and if it’s a DB server, you should place it in a private subnet all inside your VPC.

Below,
1. Network section will give a list of VPCs available in our platform.
2. Select an already existing VPC
3. You can also create a new VPC

Here I have selected an already existing VPC where I want to launch my instance.

<img src="images/ec2-step6 VPC.png" width="900"/>


A VPC consists of subnets, which are IP ranges that are separated for restricting access.  Below,

1. Under Subnets, you can choose the subnet where you want to place your instance.
2. I have chosen an already existing public subnet.
3. You can also create a new subnet in this step.

<img src="images/ec2-step6 Subnets.png" width="900"/>


Once your instance is launched in a public subnet, AWS will assign a dynamic public IP to it from their pool of IPs.

- You can choose if you want AWS to assign it an IP automatically, or you want to do it manually later. You can enable/ disable ‘Auto assign Public IP’ feature here likewise.
- Here we are going to assign this instance a static IP called as EIP (Elastic IP) later. So we keep this feature disabled as of now.

<img src="images/ec2-step6-public ip.png" width="900"/>


In the following step, keep the option of IAM role ‘None’ as of now. We will visit the topic of IAM role in detail in IAM services.

<img src="images/ec2-step-iam.png" width="900"/>

you have to do following things

- **Shutdown Behavior** – when you accidently shut down your instance, you surely don’t want it to be deleted but stopped.
- Here we are defining my shutdown behavior as Stop.

<img src="images/ec2-step6-shutdown.png" width="900"/>


- In case, you have accidently terminated your instance, AWS has a layer of security mechanism. It will not delete your instance if you have enabled accidental termination protection.
- Here we are checking the option for further protecting our instance from accidental termination.

<img src="images/ec2-step6-termination.png" width="900"/>

- **Under Monitoring-** you can enable Detailed Monitoring if your instance is a business critical instance. Here we have kept the option unchecked. AWS will always provide Basic monitoring on your instance free of cost. We will visit the topic of monitoring in AWS Cloud Watch part of the tutorial.
- **Under Tenancy**- select the option if shared tenancy. If your application is a highly secure application, then you should go for dedicated capacity. AWS provides both options.

<img src="images/ec2-step6-Tenancy.png" width="900"/>


###  Step 7. Add Storage


Click on ‘Add Storage’ to add data volumes to your instance in next step.

<img src="images/ec2-step7-add-storage.png" width="900"/>

- In the Add Storage step, you’ll see that the instance has been automatically provisioned a General Purpose SSD root volume of 8GB. ( Maximum volume size we can give to a General Purpose volume is 16GB)
- You can change your volume size, add new volumes, change the volume type, etc.
- AWS provides 3 type of **EBS volumes**- 
  1. Magnetic.
  2. General Purpose SSD.
  3. Provisioned IOPs. 
  
 You can choose a volume type based on your application’s IOPs needs.

<img src="images/ec2-step7-add volume.png" width="900"/>



###  Step 8. Tag Instance

- you can tag your instance with a key-value pair. This gives visibility to the AWS account administrator when there are lot number of instances.
- The instances should be tagged based on their department, environment like Dev/SIT/Prod. Etc. this gives a clear view of the costing on the instances under one common tag.
- Here we have tagged the instance as a Dev_Web server 01
- Go to configure Security Groups later

<img src="images/ec2-step8Tag Instance -.png" width="900"/>


###  Step 9. Configure Security Groups

In this next step of configuring Security Groups, you can restrict traffic on your instance ports. This is an added firewall mechanism provided by AWS apart from your instance’s OS firewall.

You can define open ports and IPs.

Since our server is a webserver=, we will do following things

1. Creating a new Security Group
2. Naming our SG for easier reference
3. Defining protocols which we want enabled on my instance
4. Assigning IPs which are allowed to access our instance on the said protocols
5. Once, the firewall rules are set- Review and launch

<img src="images/ec2-step9.png" width="900"/>



###  Step 10. Review Instances

In this step, we will review all our choices and parameters and go ahead to launch our instance.


<img src="images/ec2-step10.png" width="900"/>

In the next step you will be asked to create a key pair to login to you an instance. A key pair is a set of public-private keys.

AWS stores the private key in the instance, and you are asked to download the private key. Make sure you download the key and keep it safe and secured; if it is lost you cannot download it again.

- Create a new key pair
- Give a name to your key
- Download and save it in your secured folder

<img src="images/ec2-step10 Download.png" width="900"/>

When you download your key, you can open and have a look at your RSA private key.



<img src="images/ec2-step10 RSA.png" width="900"/>


Once you are done downloading and saving your key, launch your instance.


<img src="images/ec2-step10 launch.png" width="900"/>



You can see the launch status meanwhile.

<img src="images/ec2-step10 status.png" width="900"/>


You can also see the launch log.

<img src="images/ec2-step10 logs.png" width="900"/>

Click on the ‘Instances’ option on the left pane where you can see the status of the instance as ‘Pending’ for a brief while.

<img src="images/ec2-step10 status1.png" width="900"/>

- Once your instance is up and running, you can see its status as ‘Running’ now.
- Note that the instance has received a Private IP from the pool of AWS.

<img src="images/ec2-step10Running.png" width="900"/>



###  Step 11. Create a EIP and connect to your instance



An EIP is a static public IP provided by AWS. It stands for Elastic IP. Normally when you create an instance, it will receive a public IP from the AWS’s pool automatically. If you stop/reboot your instance, this public IP will change- it’dynamic. In order for your application to have a static IP from where you can connect via public networks, you can use an EIP.

Step 1) On the left pane of EC2 Dashboard, you can go to ‘Elastic IPs’ as shown below.

https://www.guru99.com/creating-amazon-ec2-instance.html#3



---

## Links: 

1. [How to Create EC2 Instance in AWS: Step by Step Tutorial](https://www.guru99.com/creating-amazon-ec2-instance.html)
2. [AWS - Elastic Compute Cloud](https://www.tutorialspoint.com/amazon_web_services/amazon_web_services_elastic_compute_cloud.htm)
3. [EC2](https://www.javatpoint.com/aws-ec2)
