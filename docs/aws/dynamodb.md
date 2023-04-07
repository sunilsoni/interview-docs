---
layout: default
title: DynamoDB
parent: Amazon Web Services (AWS)
resource: true
desc: " AWS DynamoDB interview questions and answers."
categories: [AWS DynamoDB]

---

# AWS DynamoDB
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

- Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that require consistent single-digit millisecond latency at any scale.
- It is a fully managed database that supports both document and key-value data models.
- Its flexible data model and performance makes it a great fit for mobile, web, gaming, ad-tech, IOT, and many other applications.
- It is stored in SSD storage.
- It is spread across three geographically data centres.

---

## Consistency models

Because of its availability in three geographically data centres, It consists of two different types of consistency models:

1. Eventual Consistent Reads
2. Strongly Consistent Reads

### Eventual Consistent Reads

It maintains consistency across all the copies of data which is usually reached within a second. If you read a data from DynamoDB table, then the response would not reflect the most recently completed write operation, and if you repeat to read the data after a short period, then the response would be the lattest update. This is the best model for Read performance.

### Strongly Consistent Reads

A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.


---


## Basic Concepts
Before using DynamoDB, you must familiarize yourself with its basic components and ecosystem. In the DynamoDB ecosystem, you work with tables, attributes, and items. A table holds sets of items, and items hold sets of attributes. An attribute is a fundamental element of data requiring no further decomposition, i.e., a field.

### Primary Key

The Primary Keys serve as the means of unique identification for table items, and secondary indexes provide query flexibility. DynamoDB streams record events by modifying the table data.

The Table Creation requires not only setting a name, but also the primary key; which identifies table items. No two items share a key. DynamoDB uses two types of primary keys −

- **Partition Key** − This simple primary key consists of a single attribute referred to as the “partition key.” Internally, DynamoDB uses the key value as input for a hash function to determine storage.
- **Partition Key and Sort Key** − This key, known as the “Composite Primary Key”, consists of two attributes.
  - The partition key and
  - The sort key.

  DynamoDB applies the first attribute to a hash function, and stores items with the same partition key together; with their order determined by the sort key. Items can share partition keys, but not sort keys.

The Primary Key attributes only allow scalar (single) values; and string, number, or binary data types. The non-key attributes do not have these constraints.


### Secondary Indexes
These indexes allow you to query table data with an alternate key. Though DynamoDB does not force their use, they optimize querying.

DynamoDB uses two types of secondary indexes −

- **Global Secondary Index** − This index possesses partition and sort keys, which can differ from table keys.

- **Local Secondary Index** − This index possesses a partition key identical to the table, however, its sort key differs.

### API 

The API operations offered by DynamoDB include those of the control plane, data plane (e.g., creation, reading, updating, and deleting), and streams. In control plane operations, you create and manage tables with the following tools −

- CreateTable
- DescribeTable
- ListTables
- UpdateTable
- DeleteTable


In the data plane, you perform CRUD operations with the following tools −


| Create | Read | Update     | Delete         |
|--------|------|------------|----------------|
| PutItem       | GetItem     | UpdateItem | DeleteItem     |
| BatchWriteItem   |  BatchGetItem |            | BatchWriteItem |
|        |   Query   |            |                |
|        |   Scan   |            |                |

The stream operations control table streams. You can review the following stream tools −

- ListStreams
- DescribeStream
- GetShardIterator
- GetRecords


### Provisioned Throughput

In table creation, you specify provisioned throughput, which reserves resources for reads and writes. You use capacity units to measure and set throughput.

When applications exceed the set throughput, requests fail. The DynamoDB GUI console allows monitoring of set and used throughput for better and dynamic provisioning.

### Read Consistency
DynamoDB uses eventually consistent and strongly consistent reads to support dynamic application needs. Eventually consistent reads do not always deliver current data.

The strongly consistent reads always deliver current data (with the exception of equipment failure or network problems). Eventually consistent reads serve as the default setting, requiring a setting of true in the ConsistentRead parameter to change it.


### Partitions
DynamoDB uses partitions for data storage. These storage allocations for tables have SSD backing and automatically replicate across zones. DynamoDB manages all the partition tasks, requiring no user involvement.

In table creation, the table enters the CREATING state, which allocates partitions. When it reaches ACTIVE state, you can perform operations. The system alters partitions when its capacity reaches maximum or when you change throughput.

---


## DynamoDB Simplified:
Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. It's a fully managed, multiregion, multimaster, durable non-SQL database. It comes with built-in security, backup and restore, and in-memory caching for internet-scale applications.

## DynamoDB Key Details:
- The main components of DynamoDB are:
  - a collection which serves as the foundational table
  - a document which is equivalent to a row in a SQL database
  - key-value pairs which are the fields within the document or row
- The convenience of non-relational DBs is that each row can look entirely different based on your use case. There doesn't need to be uniformity. For example, if you need a new column for a particular entry you don't also need to ensure that that column exists for the other entries.
- DynamoDB supports both document and key-value based models. It is a great fit for mobile, web, gaming, ad-tech, IoT, etc.
- DynamoDB is stored via SSD which is why it is so fast.
- It is spread across 3 geographically distinct data centers.
- The default consistency model is Eventually Consistent Reads, but there are also Strongly Consistent Reads.
- The difference between the two consistency models is the one second rule. With Eventual Consistent Reads, all copies of data are usually identical within one second after a write operation. A repeated read after a short period of time should return the updated data. However, if you need to read updated data within or less than a second and this needs to be a guarantee, then strongly consistent reads are your best bet.
- If you face a scenario that requires the schema, or the structure of your data, to change frequently, then you have to pick a database which provides a non-rigid and flexible way of adding or removing new types of data. This is a classic example of choosing between a relational database and non-relational (NoSQL) database. In this scenario, pick DynamoDB.
- A relational database system does not scale well for the following reasons:
  - It normalizes data and stores it on multiple tables that require multiple queries to write to disk.
  - It generally incurs the performance costs of an ACID-compliant transaction system.
  - It uses expensive joins to reassemble required views of query results.
- High cardinality is good for DynamoDB I/O performance. The more distinct your partition key values are, the better.  It makes it so that the requests sent will be spread across the partitioned space.
- DynamoDB makes use of parallel processing to achieve predictable performance. You can visualize each partition or node as an independent DB server of fixed size with each partition or node responsible for a defined block of data. In SQL terminology, this concept is known as sharding but of course DynamoDB is not a SQL-based DB. With DynamoDB, data is stored on Solid State Drives (SSD).

---

## DynamoDB Accelerator (DAX):
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second.
- With DAX, your applications remain fast and responsive, even when unprecedented request volumes come your way. There is no tuning required.
- DAX lets you scale on-demand out to a ten-node cluster, giving you millions of requests per second.
- DAX does more than just increase read performance by having write through cache. This improves write performance as well.
- Just like DynamoDB, DAX is fully managed. You no longer need to worry about management tasks such as hardware or software provisioning, setup and configuration, software patching, operating a reliable, distributed cache cluster, or replicating data over multiple instances as you scale.
- This means there is no need for developers to manage the caching logic. DAX is completely compatible with existing DynamoDB API calls.
- DAX enables you to provision one DAX cluster for multiple DynamoDB tables, multiple DAX clusters for a single DynamoDB table or somewhere in between giving you maximal flexibility.
- DAX is designed for HA so in the event of a failure of one AZ, it will fail over to one of its replicas in another AZ. This is also managed automatically.

---

## DynamoDB Streams:
- A DynamoDB stream is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table.
- Amazon DynamoDB is integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in DynamoDB Streams.
- Immediately after an item in the table is modified, a new record appears in the table's stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records. The Lambda function can perform any actions you specify, such as sending a notification or initiating a workflow.
- With triggers, you can build applications that react to data modifications in DynamoDB tables.
- Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a stream record with the primary key attribute(s) of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the "before" and "after" images of modified items.

---

## DynamoDB Global Tables
- Global Tables is a multi-region, multi-master replication solution for fast local performance of globally distributed apps.
- Global Tables replicates your Amazon DynamoDB tables automatically across your choice of AWS regions.
- It is based on DynamoDB streams and is multi-region redundant for data recovery or high availability purposes. Application failover is as simple as redirecting your application’s DynamoDB calls to another AWS region.
- Global Tables eliminates the difficult work of replicating data between regions and resolving update conflicts, enabling you to focus on your application’s business logic. You do not need to rewrite your applications to make use of Global Tables.
- Replication latency with Global Tables is typically under one second.



---

## More Details: 
1. [What is DynamoDB?](https://www.javatpoint.com/aws-dynamodb)
2. [DynamoDB](https://www.tutorialspoint.com/dynamodb/dynamodb_basic_concepts.htm)