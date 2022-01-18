---
title: Amazon Web Services (AWS)
has_children: true
nav_order: 2
permalink: docs/ui-component/aws
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

Amazon Route 53 is a Domain Name System (DNS), which allows you to route your custom domain names to your actual application on AWS. So, you configure Route 53 to send requests from the browser to your AWS application. The AWS DNS sets up your custom domain name.

---
## CloudWatch

Amazon CloudWatch is a key service that helps you plan, monitor, and fine-tune your AWS infrastructure and applications. It lets you collect, search, and visualize data from your applications and AWS resources in the form of logs, metrics, and events. 

Common CloudWatch use cases include the following:

**Infrastructure monitoring and troubleshooting** 
Visualize performance metrics to discover trends over time and spot outliers that might indicate a problem. Correlate metrics and logs across your application and infrastructure stacks to understand the root cause of failures and performance issues.

**Resource optimization** 
Save money and help with resource planning by identifying overused or underused resources. Ensure performance and availability by using AWS Auto Scaling to automatically provision new EC2 instances to meet demand.

**Application monitoring** 
Create CloudWatch alarms to alert you and take corrective action when a resource’s utilization, performance, or health falls outside of a threshold that you define.

**Log analytics** 
Search, visualize, and correlate logs from multiple sources to help with troubleshooting and identify areas for improvement.

---
### CloudWatch Metrics

CloudWatch Metrics is a feature that collects numeric performance metrics from both AWS and non-AWS resources such as on-premises servers. A metric is a variable that contains a timeordered set of data points. Each data point contains a timestamp, a value, and optionally a unit of measure. For example, a data point for the CPU Utilization metric for an EC2 instance may contain a timestamp of December 25, 2018 13:37, a value of 75, and Percent as the unit of measure. All AWS resources automatically send their metrics to CloudWatch. These metrics include things such as EC2 instance CPU utilization, S3 bucket sizes, and DynamoDB consumed read and write capacity units. CloudWatch stores metrics for up to 15 months. You can graph metrics to view trends and how they change over time.

**Figure:** Using CloudWatch to graph the CPU Utilization metric for an EC2 Instance

<img src="AWS/images/CloudWatch-Metrics.png" width="900"/>

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

<img src="AWS/images/CloudWatch dashboard.png" width="900"/>

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

<img src="AWS/images/Cost and usage.png" width="900"/>

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

<img src="AWS/images/Cost and usage report showing monthly costs grouped by service.png" width="900"/>

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

<img src="AWS/images/RI Utilization report.png" width="900"/>

### Reserved Instances Coverage

The Reserved Instances Coverage report tells you how many of your running instance hours are covered by instance reservations, how much you’ve spent for on-demand instances, and how much you could have saved by purchasing reserved instances. Figure 6.21 shows a graph of reservation coverage for the past 12 months, as well as the average coverage percentage and the total on-demand costs.

**Figure**:  RI Coverage report

<img src="AWS/images/RI Coverage report.png" width="900"/>

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