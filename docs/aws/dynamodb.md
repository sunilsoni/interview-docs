
---
layout: default
title: DynamoDB
parent: Amazon Web Services (AWS)

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


| Create | Read | Update| Delete|
|--------|------|--------- |--------- |
| PutItem       | GetItem     | UpdateItem | DeleteItem|
| BatchWriteItem       |  BatchGetItem |   | BatchWriteItem|
|        |   Query   | | |
|        |   Scan   | | |

The stream operations control table streams. You can review the following stream tools −

ListStreams
DescribeStream
GetShardIterator
GetRecords


### Primary





### Primary




---

## More Details: 
1. [What is DynamoDB?](https://www.javatpoint.com/aws-dynamodb)