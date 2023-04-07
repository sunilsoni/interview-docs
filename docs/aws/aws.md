---
title: Amazon Web Services (AWS)
has_children: true
nav_order: 2
permalink: docs/aws
resource: true
desc: "Amazon Web Services (AWS) interview questions and answers."
categories: [Amazon Web Services (AWS)]
---

# Amazon Web Services (AWS)
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

AWS stands for Amazon Web Service; it is a collection of remote computing services also known as a cloud computing platform. This new realm of cloud computing is also known as IaaS or Infrastructure as a Service.

---

---

Key components of AWS:

## Elastic Cloud Compute (EC2)

Elastic Cloud Compute (EC2) is one of the first web service interfaces when AWS was released, allowing users to create and configure compute machines within the cloud. EC2 allows users to create VM (virtual machine) on the Amazon cloud for running applications that can be accessed via the Internet. The software can be configured on cloud servers based on your specifications. You select the operating system (i.e., Microsoft Windows or Linux) best suited to your requirements or applications, and you get the operating system pre-installed. EC2 provides the actual host server and operating system.

If you want any additional software, you must manually install it on top of the OS as a developer. So, if you want JDK (Java Development Kit), you can install Java. You can also install Tomcat, a database, and so on. It’s almost like getting a brand-new laptop that only has the operating system, and you need to install your tools on top of it.

---

## Amazon Relational Database Service (RDS)

The Amazon Relational Database Service (RDS) is Amazon’s managed relational database
service. RDS lets you provision a number of popular relational database management systems
(RDBMSs) including Microsoft SQL Server, Oracle, MySQL, and PostgreSQL.

You can always install and configure your own database server on an EC2 instance. But
RDS offers several advantages over this. When you create an RDS database instance, Amazon
sets up one or more compute instances and takes care of installing and configuring the RDBMS
of your choice. These compute instances are not EC2 instances that you can secure shell (SSH)
into, but they are connected to a virtual private cloud (VPC) of your choice, allowing your
applications running on AWS or on-premises to take full advantage of an RDS-hosted database.
Like EC2 instances, RDS instances use Elastic Block Service (EBS) volumes for storage.

To achieve the level of performance and availability you need, you can choose a multi-Availability
Zone (multi-AZ) deployment to have database instances in multiple Availability
Zones. RDS can also perform manual or automatic EBS snapshots that you can easily
restore to new RDS instances. RDS can also handle the hard work of installing patches and
upgrades during scheduled maintenance windows.



### Database Engines
When you create an RDS instance, you must choose a database engine, which is the specific
RDBMS that will be installed on your instance. You can have only one database engine per
instance, but you can provision multiple instances if need be. 

Amazon RDS supports the following six database engines:

-  MySQL
-  MariaDB
-  Oracle
-  PostgreSQL
-  Microsoft SQL Server
-  Amazon Aurora

With the exception of Amazon Aurora, these database engines are either open source or
commercially available products found in many data center environments. Amazon Aurora
is a proprietary database designed for RDS, but it’s compatible with existing MySQL and
PostgreSQL databases. Being able to use RDS to deploy an RDBMS that you’re already
familiar with makes migrating such databases from on-premises to RDS much easier.

### Licensing

Depending on the database engine you choose, you must choose one of two licensing
options: license included or bring your own license (BYOL):

**License included** 
The license is included in the pricing for each RDS instance. The
Microsoft SQL Server and Oracle database engine options offer this license model. The
free database engines—MariaDB, MySQL, and PostgreSQL—exclusively use the license
included model.

**Bring your own license** 
In this model, you must provide your own license to operate the
database engine you choose. Unlike the license-included option, licensing costs are not built
into RDS pricing. This model is currently available only for Oracle databases.

### Instance Classes

Implementing a relational database—even one backed by RDS—requires some capacity
planning to ensure the database gives you the level of availability and performance your
application needs.
When you deploy an RDS instance, you must choose a database instance class that
defines the number of virtual CPUs (vCPU), the amount of memory, and the maximum
network and storage throughput the instance can support. 

There are three instances classes you can choose from: 
1. Standard, 
2. Memory Optimized, and 
3. Burstable Performance.

### 1. Standard

The Standard instance class will meet the requirements of most applications. The latest generation
Standard instance class offers the following specs:
- Between 2 and 96 vCPU
- 8–384 GB memory

### 2. Memory Optimized
The Memory Optimized instance class is for applications with the most demanding database
requirements. This class offers the most disk throughput and network bandwidth. 
The latest-generation instance class provides the following:
-  Between 4 and 128 vCPU
-  122–3,904 GB memory

Database instances use EBS storage. Both the Standard and Memory Optimized instance
class types are EBS-optimized, meaning they provide dedicated bandwidth for transfers to
and from EBS storage.

### 3. Burstable Performance
The Burstable Performance instance class is for nonproduction databases that have minimal
performance requirements, such as those for test and development purposes. The latestgeneration
Burstable Performance instance class has the lowest network bandwidth and
disk throughput and offers the following:

- Between 2 and 8 vCPU
- 1–32 GB memory

It can be difficult to predict exactly how many RDS instances you need and how much
compute power, memory, and network and storage throughput each of those instances
needs. Thankfully, RDS makes it easy to right-size your database deployments in two ways:
scaling vertically and scaling horizontally.

### Scaling Vertically

Scaling vertically refers to changing the way resources are allocated to a specific instance.
After creating an instance, you can scale up to a more powerful instance class to add more
memory or improve computing or networking performance. Or you can scale down to a
less powerful class to save on costs.

### Storage

The level of performance an RDS instance can achieve depends not only on the instance
class you choose but also on the type of storage. New RDS instances use EBS volumes, and
the maximum throughput a volume can achieve is a function of both the instance class and
the number of input/output operations per second (IOPS) the EBS volume supports. IOPS
measure how fast you can read from and write to a volume. Higher IOPS generally means
faster reads and writes. RDS offers three types of storage: general-purpose SSD, provisioned
IOPS SSD, and magnetic.

### General-Purpose SSD
General-purpose SSD storage is good enough for most databases. You can allocate a
volume of between 20 GB and 32 TB. The number of IOPS per volume depends on how
much storage you allocate. The more storage you allocate, the better your read and write
performance will be.

If you’re not sure how much storage to provision, don’t worry. General-purpose SSD
volumes can temporarily achieve a higher number of IOPS through a process called
bursting. During spikes of heavy read or write activity, bursting will kick in automatically and give your volume an added performance boost. This way, you don’t have to allocate an
excessive amount of storage just to get enough IOPS to meet peak demand.

### Provisioned IOPS SSD
Provisioned IOPS SSD storage allows you to specify the exact number of IOPS (in thousands)
that you want to allocate per volume. Like general-purpose SSD storage, you can allocate
up to 32 TB. But unlike general-purpose SSD storage, provisioned IOPS SSD storage doesn’t
offer bursting, so it’s necessary to decide beforehand the maximum number of IOPS you’ll
need. However, even if your needs change, you can always adjust the number of IOPS later.


### Magnetic
Magnetic storage is available for backward compatibility with legacy RDS instances.
Unlike the other storage options, it doesn’t use EBS, and you can’t change the size of a
magnetic volume after you create it. Magnetic volumes are limited to 4 TB in size and
1,000 IOPS.
You can increase the size of an EBS volume after creating it without causing an outage
or degrading performance. You can’t, however, decrease the amount of storage allocated,
so be careful not to go overboard.
You can also migrate from one storage type to another, but doing so can result in a short
outage of typically a few minutes. But when migrating from magnetic to EBS storage, the
process can take up to several days. During this time, the instance is still usable but may
not perform optimally.


### Scaling Horizontally with Read Replicas
In addition to scaling up by choosing a more powerful instance type or selecting high-IOPS
storage, you can improve the performance of a database-backed application by adding
additional RDS instances that perform only reads from the database. These instances are
called read replicas.

In a relational database, only the master database instance can write to the database. A
read replica helps with performance by removing the burden of read-only queries from the
master instance, freeing it up to focus on writes. Hence, read replicas provide the biggest
benefit for applications that need to perform a high number of reads. Read replicas are also
useful for running computationally intensive queries, such as monthly or quarterly reports
that require reading and processing large amounts of data from the database.

### High Availability with Multi-AZ
Even if you use read replicas, only the master database instance can perform writes against
your database. If that instance goes down, your database-backed application won’t be able
to write data until it comes back online. To ensure that you always have a master database
instance up and running, you can configure high availability by enabling the multi-AZ
feature on your RDS instance.

With multi-AZ enabled, RDS creates an additional instance called a standby database
instance that runs in a different Availability Zone than your primary database instance.
The primary instance instantly or synchronously replicates data to the secondary instance,
ensuring that every time your application writes to the database, that data exists in multiple
Availability Zones.
If the primary fails, RDS will automatically fail over to the secondary. The failover can
result in an outage of up to two minutes, so your application will experience some interruption,
but you won’t lose any data.
With multi-AZ enabled, you can expect your database to achieve a monthly availability
of 99.95 percent. It’s important to understand that an instance outage may occur for reasons
other than an Availability Zone outage. Routine maintenance tasks such as patching or
upgrading the instance can result in a short outage and trigger a failover.
If you use the Amazon Aurora database engine—Amazon’s proprietary database engine
designed for and available exclusively with RDS—you can take advantage of additional
benefits when using multi-AZ. When you use Aurora, your RDS instances are part of an
Aurora cluster. All instances in the cluster use a shared storage volume that’s synchronously
replicated across three different Availability Zones. Also, if your storage needs increase, the
cluster volume will automatically expand up to 64 TB.

### Backup and Recovery
Whether or not you use multi-AZ, RDS can take manual or automatic EBS snapshots of
your instances. Snapshots are stored across multiple Availability Zones. If you ever need to
restore from a snapshot, RDS will restore it to a new instance. This makes snapshots useful
not only for backups but also for creating copies of a database for testing or development
purposes.
You can take a manual snapshot at any time. You can configure automatic snapshots
to occur daily during a 30-minute backup window. RDS will retain automatic snapshots
between 1 day and 35 days, with a default of 7 days. Manual snapshots are retained until
you delete them.
Enabling automatic snapshots also enables point-in-time recovery, a feature that saves
your database change logs every 5 minutes. Combined with automated snapshots, this gives
you the ability to restore a failed instance to within 5 minutes before the failure—losing no
more than 5 minutes of data.
---

## Route 53

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) service. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.

### Route53 Key Details:
- DNS is used to map human-readable domain names into an internet protocol address similarly to how phone books map company names with phone numbers.
- AWS has its own domain registrar.
- When you buy a domain name, every DNS address starts with an SOA (Start of Authority) record. The SOA record stores information about the name of the server that kicked off the transfer of ownership, the administrator who will now use the domain, the current metadata available, and the default number of seconds or TTL.
- NS records, or Name Server records, are used by the Top Level Domain hosts (.org, .com, .uk, etc.) to direct traffic to the Content servers. The Content DNS servers contain the authoritative DNS records.
- Browsers talk to the Top Level Domains whenever they are queried and encounter domain name that they do not recognize.
    1. Browsers will ask for the authoritative DNS records associated with the domain.
    2. Because the Top Level Domain contains NS records, the TLD can in turn query the Name Servers for their own SOA.
    3. Within the SOA, there will be the requested information.
    4. Once this information is collected, it will then be returned all the way back to the original browser asking for it.
- In summary: Browser -> TLD -> NS -> SOA -> DNS record. The pipeline reverses when the correct DNS record is found.
- Authoritative name servers store DNS record information, usually a DNS hosting provider or domain registrar like GoDaddy that offers both DNS registration and hosting.
- There are a multitude of DNS records for Route53. Here are some of the more common ones:
    - **A records**: These are the fundamental type of DNS record. The “A” in A records stands for “address”. These records are used by a computer to directly pair a domain name to an IP address. IPv4 and IPv6 are both supported with "AAAA" referring to the IPv6 version. **A: URL -> IPv4** and **AAAA: URL -> IPv6**.
    - **CName records**: Also referred to as the Canonical Name. These records are used to resolve one domain name to another domain name. For example, the domain of the mobile version of a website may be a CName from the domain of the browser version of that same website rather than a separate IP address. This would allow mobile users who visit the site and to receive the mobile version. **CNAME: URL -> URL**.
    - **Alias records**: These records are used to map your domains to AWS resources such as load balancers, CDN endpoints, and S3 buckets. Alias records function similarly to CNames in the sense that you map one domain to another. The key difference though is that by pointing your Alias record at a service rather than a domain name, you have the ability to freely change your domain names if needed and not have to worry about what records might be mapped to it. Alias records give you dynamic functionality. **Alias: URL -> AWS Resource**.
    - **PTR records**: These records are the opposite of an A record. PTR records map an IP to a domain and they are used in reverse DNS lookups as a way to obtain the domain name of an IP address. **PTR: IPv4 -> URL**.
- One other major difference between CNames and Alias records is that a CName cannot be used for the naked domain name (the apex record in your entire DNS configuration / the primary record to be used). CNames must always be secondary records that can map to another secondary record or the apex record. The primary must always be of type Alias or A Record in order to work.
- Due to the dynamic nature of Alias records, they are often recommended for most use cases and should be used when it is possible to.
- TTL is the length that a DNS record is cached on either the resolving servers or the users own cache so that a fresher mapping of IP to domain can be retrieved. Time To Live is measured in seconds and the lower the TTL the faster DNS changes propagate across the internet. Most providers, for example, have a TTL that lasts 48 hours.
- You can create health checks to send you a Simple Notification if any issues arise with your DNS setup.
- Further, Route53 health checks can be used for any AWS endpoint that can be accessed via the Internet. This makes it an ideal option for monitoring the health of your AWS endpoints.

### Route53 Routing Policies:
- When you create a record, you choose a routing policy, which determines how Amazon Route 53 responds to DNS queries. The routing policies available are:
    - Simple Routing
    - Weighted Routing
    - Latency-based Routing
    - Failover Routing
    - Geolocation Routing
    - Geo-proximity Routing
    - Multivalue Answer Routing
- **Simple Routing** is used when you just need a single record in your DNS with either one or more IP addresses behind the record in case you want to balance load. If you specify multiple values in a Simple Routing policy, Route53 returns a random IP from the options available.
- **Weighted Routing** is used when you want to split your traffic based on assigned weights. For example, if you want 80% of your traffic to go to one AZ and the rest to go to another, use Weighted Routing. This policy is very useful for testing feature changes and due to the traffic splitting characteristics, it can double as a means to perform blue-green deployments. When creating Weighted Routing, you need to specify a new record for each IP address. You cannot group the various IPs under one record like with Simple Routing.
- **Latency-based Routing**, as the name implies, is based on setting up routing based on what would be the lowest latency for a given user. To use latency-based routing, you must create a latency resource record set in the same region as the corresponding EC2 or ELB resource receiving the traffic. When Route53 receives a query for your site, it selects the record set that gives the user the quickest speed. When creating Latency-based Routing, you need to specify a new record for each IP.
- **Failover Routing** is used when you want to configure an active-passive failover set up. Route53 will monitor the health of your primary so that it can failover when needed. You can also manually set up health checks to monitor all endpoints if you want more detailed rules.
- **Geolocation Routing** lets you choose where traffic will be sent based on the geographic location of your users.
- **Geo-proximity Routing** lets you choose where traffic will be sent based on the geographic location of your users *and* your resources. You can choose to route more or less traffic based on a specified weight which is referred to as a bias. This bias either expands or shrinks the availability of a geographic region which makes it easy to shift traffic from resources in one location to resources in another. To use this routing method, you must enable Route53 traffic flow. If you want to control global traffic, use Geo-proximity routing. If you want traffic to stay in a local region, use Geolocation routing.
- **Multivalue Routing** is pretty much the same as Simple Routing, but Multivalue Routing allows you to put health checks on each record set. This ensures then that only a healthy IP will be randomly returned rather than any IP.

---

## CloudWatch

Amazon CloudWatch is a monitoring and observability service. It provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.

### CloudWatch Key Details:
- CloudWatch collects monitoring and operational data in the form of logs, metrics, and events.
- You can use CloudWatch to detect anomalous behavior in your environments, set alarms, visualize logs and metrics side by side, take automated actions, troubleshoot issues, and discover insights to keep your applications
  running smoothly.
- Within the compute domain, CloudWatch can inform you about the health of EC2 instances, Autoscaling Groups, Elastic Load Balancers, and Route53 Health Checks.
  Within the storage and content delivery domains, CloudWatch can inform you about the health of EBS Volumes, Storage Gateways, and CloudFront.
- With regards to EC2, CloudWatch can only monitor host level metrics such as CPU, network, disk, and status checks for insights like the health of the underlying hypervisor.
- CloudWatch is *NOT* CloudTrail so it is important to know that only CloudTrail can monitor AWS access for security and auditing reasons. CloudWatch is all about performance. CloudTrail is all about auditing.
- CloudWatch with EC2 will monitor events every 5 minutes by default, but you can have 1 minute intervals if you use Detailed Monitoring.

![Screen Shot 2020-06-17 at 8 16 23 PM](https://user-images.githubusercontent.com/13093517/84963455-71af6a00-b0d7-11ea-8168-15dd791bf000.png)

- You can customize your CloudWatch dashboards for insights.
- There is a multi-platform CloudWatch agent which can be installed on both Linux and Windows-based instances. This agent enables you to select the metrics to be collected, including sub-resource metrics such as per-CPU core. You can use this single agent to collect both system metrics and log files from Amazon EC2 instances and on-premises servers.
- The following metrics are not collected from EC2 instances via CloudWatch:
    - Memory utilization
    - Disk swap utilization
    - Disk space utilization
    - Page file utilization
    - Log collection
- If you need the above information, then you can retrieve it via the official CloudWatch agent or you can create a custom metric and send the data on your own via a custom script.
- CloudWatch's key purpose:
    - Collect metrics
    - Collect logs
    - Collect events
    - Create alarms
    - Create dashboards

### CloudWatch Logs:
- You can use Amazon CloudWatch Logs to monitor, store, and access your log files from Amazon EC2 instances, AWS CloudTrail, Amazon Route 53, and other sources. You can then retrieve the associated log data from CloudWatch Logs.
- It helps you centralize the logs from all of your systems, applications, and AWS services that you use, in a single, highly scalable service.
- You can create log groups so that you join logical units of CloudWatch Logs together.
- You can stream custom log files for further insights.

### CloudWatch Events:
- Amazon CloudWatch Events delivers a near real-time stream of system events that describe changes in AWS resources.
- You can use events to trigger lambdas for example while using alarms to inform you that something went wrong.

### CloudWatch Alarms:
- CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define.
- For example, you can create custom CloudWatch alarms which will trigger notifications such as surpassing a set billing threshold.
- CloudWatch alarms have two states of either `ok` or `alarm`

### CloudWatch Metrics:
- CloudWatch Metrics represent a time-ordered set of data points.
- These basically are a variable you can monitor over time to help tell if everything is okay, e.g. Hourly CPU Utilization.
- CloudWatch Metrics allows you to track high resolution metrics at sub-minute intervals all the way down to per second.

### CloudWatch Dashboards:
- CloudWatch dashboards are customizable home pages in the CloudWatch console that you can use to monitor your resources in a single view
- These dashboards integrate with CloudWatch Metrics and CloudWatch Alarms to create customized views of the metrics and alarms for your AWS resources.




### CloudWatch Metrics

CloudWatch Metrics is a feature that collects numeric performance metrics from both AWS and non-AWS resources such as on-premises servers. A metric is a variable that contains a timeordered set of data points. Each data point contains a timestamp, a value, and optionally a unit of measure. For example, a data point for the CPU Utilization metric for an EC2 instance may contain a timestamp of December 25, 2018 13:37, a value of 75, and Percent as the unit of measure. All AWS resources automatically send their metrics to CloudWatch. These metrics include things such as EC2 instance CPU utilization, S3 bucket sizes, and DynamoDB consumed read and write capacity units. CloudWatch stores metrics for up to 15 months. You can graph metrics to view trends and how they change over time.

**Figure:** Using CloudWatch to graph the CPU Utilization metric for an EC2 Instance

<img src="aws/images/CloudWatch-Metrics.png" width="900"/>

### CloudWatch Alarms

A CloudWatch alarm watches over the value of a single metric. If the metric crosses a threshold that you specify (and stays there), the alarm will take an action. For example, you might configure an alarm to take an action when the average CPU utilization for an instance exceeds 80% for five minutes. The action can be one of the following:

**Notification using Simple Notification Service**
The Simple Notification Service (SNS)allows applications, users, and devices to send and receive notifications from AWS. SNS uses a publisher-subscriber model, wherein a publisher such as an AWS service generates a notification and a subscriber such as an end user receives it. The communication channel that SNS uses to map publishers and subscribers is called a topic. 
SNS can send notifications to subscribers via a variety of protocols including the following:

- HTTP(S)
- Simple Queue Service (SQS)
- Lambda
- Mobile push notification
- Email
- Email-JSON
- Short Message Service (SMS) text messages

**Auto Scaling action** 
By specifying an EC2 Auto Scaling action, the EC2 Auto Scaling service can add or remove EC2 instances in response to changing demand. For example, if a metric indicates that instances are overburdened, you can have EC2 Auto Scaling respond by adding more instances.

**EC2 action**
If you’re monitoring a specific instance that’s having a problem, you can use an EC2 action to stop, terminate, or recover the instance. Recovering an instance migrates the instance to a new EC2 host, something you may need to do if there’s a physical hardware problem on the hardware hosting the instance.


### CloudWatch Dashboards

CloudWatch dashboards are your one-stop shop for keeping an eye on all of your important metrics. You can create multiple dashboards and add to them metric graphs, the latest values for a metric, and CloudWatch alarms. You can save your dashboards for future use and share them with others. Dashboards can also visualize metrics from multiple AWS Regions, so you can keep an eye on the global health of your infrastructure. 

Sample CloudWatch dashboard.

<img src="aws/images/CloudWatch dashboard.png" width="900"/>

### CloudWatch Logs
CloudWatch Logs collects and stores log files from AWS and non-AWS sources and makes it easy to view, search, and extract custom metrics from them.

**Log Events, Streams, and Groups**

You configure your applications and AWS services to send log events to CloudWatch Logs.
A log event is analogous to a line in a log file and always contains a timestamp and an
event message. Many AWS services produce their own logs called vended logs that you can
stream to CloudWatch Logs. Such logs include Route 53 DNS query logs, VPC flow logs,
and CloudTrail logs. CloudWatch Logs can also receive custom logs from your applications,
such as web server access logs.

CloudWatch Logs organizes log events by log streams by storing log events from the
same source in a single log stream. For example, web server access logs from a specific
EC2 instance would be stored in one log stream, while Route 53 DNS query logs would be
stored in a separate log stream.

CloudWatch further organizes log streams into log groups. To organize related log
streams, you can place them into the same log group. For instance, if you have several log
streams that are collecting web server log events from multiple web servers, you can group
all of those log streams into a single log group.
   
CloudWatch Logs stores log events indefinitely by default, but you can configure a log
group’s retention settings to delete events automatically. Retention settings range from
1 day to 10 years. You can also archive your logs by exporting them to an S3 bucket.

### Metric Filters
A metric fi lter extracts data from log events in a log group and stores that data in a custom
CloudWatch metric. For example, suppose a log event from a database server contains the
time in milliseconds it takes to run a query. You may extract that value and store it as a
CloudWatch metric so you can graph it and create an alarm to send a notifi cation when it
exceeds a certain threshold.

You can also use metric fi lters to track the number of times a particular string occurs.
This is useful for counting the number of times a particular event occurs in a log, such as
an error code. For example, you might want to track how many times a 403 Forbidden
error appears in a web server log. You can confi gure a metric fi lter to count the number of
times the error occurs in a given timeframe—fi ve minutes, for example—and record that
value in a CloudWatch custom metric.

### CloudWatch Events
The CloudWatch Events feature lets you continuously monitor for specifi c events that represent
a change in your AWS resources—particularly write-only API operations—and take an
action when they occur. 

For example, an EC2 instance going from the running state to the stopped state would be an event. 
An IAM user logging into the AWS Management Console would also be an event. CloudWatch Events can then automatically and immediately take actions in response to those events.

You start by creating a rule to defi ne the events to monitor, as well as the actions you
want to take in response to those events. You defi ne the action to take by selecting a target,
which is an AWS resource. 

Some targets you can choose from include the following:

■✓ Lambda functions

■✓ EC2 instances

■✓ SQS queues

■✓ SNS topics

■✓ ECS tasks

CloudWatch responds to events as they occur, in real time. Unlike CloudWatch alarms,
which take action when a metric crosses and remains crossing a numeric threshold,
CloudWatch events trigger immediately. For example, you can create a CloudWatch event
to send an SNS notifi cation whenever an EC2 instance terminates. Or you could trigger a
Lambda function to process an image fi le as soon as it hits an S3 bucket.

Alternatively, you can create a schedule to automatically perform actions at regular
intervals. For example, to save money you might create a schedule to shut down development
instances every day at 7 p.m., after the developers have ideally stopped working!

---

## CloudTrail

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With it, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, API calls, and other AWS services. It is a regional service, but you can configure CloudTrail to collect trails in all regions.

### CloudTrail Key Details:
- CloudTrail Events logs API calls or activities.
- CloudTrail Events stores the last 90 days of events in its Event History. This is enabled by default and is no additional cost.
- This event history simplifies security analysis, resource change tracking, and troubleshooting.
- There are two types of events that can be logged in CloudTrail: management events and data events.
- Management events provide information about management operations that are performed on resources in your AWS account.
- Think of Management events as things normally done by people when they are in AWS. Examples:
    - a user sign in
    - a policy changed
    - a newly created security configuration
    - a logging rule deletion
- Data events provide information about the resource operations performed on or in a resource.
- Think of Data events as things normally done by software when hitting various AWS endpoints. Examples:
    - S3 object-level API activity
    - Lambda function execution activity
- By default, CloudTrail logs management events, but not data events.
- By default, CloudTrail Events log files are encrypted using Amazon S3 server-side encryption (SSE). You can also choose to encrypt your log files with an AWS Key Management Service (AWS KMS) key. As these logs are stored in S3, you can define Amazon S3 lifecycle rules to archive or delete log files automatically. If you want notifications about log file delivery and validation, you can set up Amazon SNS notifications.


CloudTrail keeps detailed event logs of every action that occurs against your AWS resources. Each event that CloudTrail logs includes the following parameters:
- The service. Specifically, this is the address of the service’s global endpoint, such as iam.amazonaws.com for IAM.
- The name of the API action performed, such as RunInstances, CreateUser, or PutObject.
- The region the resource is located in. For global services, this is always us-east-1.
- Response elements. In the case of an API operation that changes or creates a resource, this contains information about the results of the action. For example, the response elements for a RunInstances action to launch an EC2 instance would yield information such as the instance ID and private IP address.
- The principal that made the request. This may include the type of principal (IAM user or role), its Amazon resource name (ARN), and the name.
- The date and time of the request, given in coordinated universal time (UTC).
- The IP address of the requester.

### API and Non-API Events

The events CloudTrail logs consist of two different actions: API and non-API actions. API actions include things such as launching an instance, creating an S3 bucket, creating a new IAM user, or taking an EBS snapshot. Note that the term API action has nothing to do with how the action was performed. For example, terminating an EC2 instance is an API event whether you do it via the AWS Management Console, the AWS command-line interface, or an AWS software development kit. Non-API actions include everything else, such as logging into the management console.


### Management and Data Events
CloudTrail also classifies events along two other dimensions: management events and data events.

Management events—also known as control plane operations—are operations that a principal (such as a user or service) attempts to execute against an AWS resource.
Management events include write-only events—API operations that modify or might modify resources, and read-only events that read resource information but don’t make any changes. For example, the RunInstances API operation can create an EC2 instance, so it would be a write-only event. On the other hand, the DescribeInstances API operation returns a list of EC2 instances but doesn’t make any changes, so it’s a read-only operation. Data events consist of S3 object-level activity and Lambda function executions, both of which tend to be high volume. As such, CloudTrail treats data events as separate from management events. And when it comes to S3 object-level operations, CloudTrail draws a distinction between read-only events like GetObject and write-only events such as PutObject and DeleteObject .



### Event History
When you open an AWS account, CloudTrail begins logging all of your management events automatically. It stores 90 days of management events in the event history, which you can view, search, and download at any time. The event history log doesn’t record data events. For each region, CloudTrail maintains a separate event history log containing the events that occurred in that region. But events generated by global services including IAM and Route 53 are included in the event history for every region.


### Trails
If you want to customize the types of events CloudTrail logs—such as specifi c management or data events—or if you need to store more than 90 days of event history, you need to create a trail. A trail is a confi guration that directs CloudTrail to record specifi ed events in log fi les and deliver them to an S3 bucket. A trail can log events from either a single region or all regions. You can choose to log management events, data events, or both. You can also choose whether to log read-only or write-only events, or both. CloudTrail doesn’t provide a way to search trail logs, which are written in JavaScript Object Notation (JSON) format. But you can download the log fi les directly from S3. You can also confi gure CloudTrail to send a trail log to CloudWatch Logs, making them available for storage, searching, and metric fi ltering.


### Log File Integrity Validation
Log fi le integrity validation is an optional feature that provides assurance that no
CloudTrail log fi les are surreptitiously modifi ed or deleted. Here’s how it works: every time
CloudTrail writes a log fi le to the trail’s S3 bucket, it calculates and stores a cryptographic hash of the fi le, which is a unique value based on the contents of the log fi le itself. If anyone modifies the file, even by one bit, the hash of the modified file will be completely different than the original hash. This can tell you whether anyone has tampered with the log file, but it can’t tell you exactly how it’s been modified.

Log files can be encrypted using server-side encryption with Amazon S3-managed
encryption keys (SSE-S3) or server-side encryption with AWS KMS-managed keys
(SSE-KMS).

---
## Cost Explorer

AWS Cost Explorer is a feature of AWS Billing and Cost Management that offers configurable reports and graphs to help you understand how each of your AWS services impacts your monthly bill.

AWS Cost Explorer offers the following three categories of reports:
- Cost and usage reports
- Reservation reports
- Reserved instance recommendations

### Cost and Usage
You can generate cost and usage reports to give you a graphical view of your daily and monthly costs and usage over time. Cost Explorer can also show you the forecast for the current month, 3 months out, and 12 months out, helping you plan ahead. Figure 6.18 shows the monthly costs for the last 12 months and a forecast for the current month.

**Figure**: Cost and usage report showing monthly costs

<img src="aws/images/Cost and usage.png" width="900"/>

You can go back as far as one year and filter or group by several parameters including but not limited to the following:

- Service
- Availability Zone
- Region
- Instance type
- Usage type
- Tag
- API operation
- Charge type
- Platform

This can help you quickly see which services are incurring the greatest costs and how those services costs are trending over time. Figure 6.19 shows the monthly costs for the last 12 months grouped by service.

**Figure** :  Cost and usage report showing monthly costs grouped by service

<img src="aws/images/Cost and usage report showing monthly costs grouped by service.png" width="900"/>

In addition to letting you create your own custom reports, Cost Explorer offers the following five default cost and usage reports:

- **Monthly costs by service**
Displays your top five most expensive services over the past six months. The top five services are graphed individually, while other services are aggregated and graphed as a single bar.

- **Monthly costs by linked account** 
Shows your costs for your top five linked accounts over the past six months. The top five linked accounts are grouped individually, and the rest are aggregated and graphed as one bar.

- **Monthly EC2 running hours costs and usage**
Displays two monthly graphs showing the costs and running hours for your EC2 instances.

- **Daily costs**
Shows your monthly spend for the last six months and a forecast for the current month.

- **AWS marketplace**:
The Core Compute Services, the AWS Marketplace allows vendors to make their products and services available to you via AWS. License, subscription, and usage costs are bundled together and billed through AWS. This report shows you how much you’ve spent on AWS Marketplace solutions.


### Reservation reports
Cost Explorer offers the following two built-in reservation reports to give you insight on how much you are saving—or could have saved—with instance reservations. Instance reservations allow you to save money by prepaying for compute instances including those used by Amazon EC2, Amazon Elasticsearch Service, Amazon ElastiCache, Amazon RDS, and Amazon Redshift.  

### Reserved Instances Utilization

The Reserved Instances (RI) Utilization report shows you the percentage of your reserved instances you’ve used and how much money you’ve saved or overspent by using reserved instances. The RI Utilization report also shows you your net savings from reserved instances, giving you insight into whether you’ve had too few or too many reserved instances. Figure 6.20 shows a sample reservation utilization for a six-month time range.

**Figure** :  RI Utilization report

<img src="aws/images/RI Utilization report.png" width="900"/>

### Reserved Instances Coverage

The Reserved Instances Coverage report tells you how many of your running instance hours are covered by instance reservations, how much you’ve spent for on-demand instances, and how much you could have saved by purchasing reserved instances. Figure 6.21 shows a graph of reservation coverage for the past 12 months, as well as the average coverage percentage and the total on-demand costs.

**Figure**:  RI Coverage report

<img src="aws/images/RI Coverage report.png" width="900"/>

### Reserved instance recommendations

Cost Explorer can provide reserved instance recommendations to help reduce your costs.
Here’s how recommendations work: Cost Explorer analyzes your on-demand instance
usage over the past 7, 30, or 60 days. It then searches for all available reserved instances
that would cover that usage. Finally, it selects the most cost-effective reserved instances and
recommends them.

Costs Explorer makes recommendations separately for each service such as EC2 or RDS.
You can also customize the recommendations by selecting a reserved instance term and
payment option.

Keep in mind that for the purposes of making reserved instance recommendations, Cost
Explorer ignores any usage that’s already covered by a reservation. So, if your instances
are already fully covered by instance reservations, Cost Explorer will not make any
recommendations.



---

## Amazon DynamoDB
DynamoDB is Amazon’s managed nonrelational database service. It’s designed for highly
transactional applications that need to read from or write to a database tens of thousands
of times a second.


### Items and Tables

The basic unit of organization in DynamoDB is an item, which is analogous to a row or
record in a relational database. DynamoDB stores items in tables. Each DynamoDB table
is stored across one or more partitions. Each partition is backed by solid-state drives,
and partitions are replicated across multiple Availability Zones in a region, giving you a
monthly availability of 99.99 percent.
Each item must have a unique value for the primary key. An item can also consist of
other key-value pairs called attributes. Each item can store up to 400 KB of data, more
than enough to fill a book! To understand this better, consider the sample shown in
Table 9.2.

Table : A Sample DynamoDB Table


| Username (Primary Key) | LastName | FirstName | FavoriteColor |
|-----------|---------|---------|---------|
|   hburger        |  Burger       | Hamilton |  |
|   dstreet        |  Street       | Della | Fuchsia |
|  pdrake         |   Drake      | Paul | Silver |
|   perry        |         | Perry |  |


Username, LastName, FirstName, and FavoriteColor are all attributes. In this table,
the Username attribute is the primary key. Each item must have a value for the primary
key, and it must be unique within the table. Good candidates for primary keys are things
that tend to be unique, such as randomly generated identifiers, usernames, and email
addresses.

Other than the primary key, an item doesn’t have to have any particular attributes.
Hence, some items may contain several attributes, while others may contain only one or
two. This flexibility makes DynamoDB the database of choice for applications that need
to store a wide variety of data without having to know the nature of that data in advance.
However, every attribute must have a defined data type, which can be one of the following:

**Scalar** 
A scalar data type has only one value and can be a string, a number, binary data,
or a Boolean value.

**Set** 
A set data type can have multiple scalar values, but each value must be unique within the set.

**Document** 
The document data type is subdivided into two subtypes: list and map.
Document data types can store values of any type. List documents are ordered, whereas
map documents are not. Document data types are useful for storing structured data,
such as an IAM policy document stored in JavaScript Object Notation (JSON) format.
DynamoDB can recognize and extract specific values nested within a document, allowing
you to retrieve only the data you’re interested in without having to retrieve the entire
document.


### Scaling Horizontally

DynamoDB uses the primary key to distribute items across multiple partitions. Distributing
the data horizontally in this fashion makes it possible for DynamoDB to consistently
achieve low-latency reads and writes regardless of how many items are in a table. The
number of partitions DynamoDB allocates to your table depends on the number of write
capacity units (WCU) and read capacity units (RCU) you allocate to your table. The higher
the transaction volume and the more data you’re reading or writing, the higher your RCU
or WCU values should be. Higher values cause DynamoDB to distribute your data across
more partitions, increasing performance and decreasing latency. As demand on your
DynamoDB tables changes, you can change the number of RCU and WCU accordingly.
Alternatively, you can configure DynamoDB Auto Scaling to dynamically adjust the number
of WCU and RCU based on demand. This automatic horizontal scaling ensures consistent
performance, even during times of peak load.

### Queries and Scans
Recall that nonrelational databases let you quickly retrieve items from a table based on the
value of the primary key. For example, if the primary key of a table is Username, you can
perform a query for the user named pdrake. If an item exists with that primary key value,
DynamoDB will return the item instantly.
Searching for a value in an attribute other than the primary key is possible, but slower.
To locate all items with a Username that starts with the letter p, you’d have to perform a
scan operation to list all items in the table. This is a read-intensive task that requires scanning
every item in every partition your table is stored in. Even if you know all the attributes of an item except for the primary key, you’d still have to perform a scan operation to
retrieve the item.

---

---
## AWS Lambda


---