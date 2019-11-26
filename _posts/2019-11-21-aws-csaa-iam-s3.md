---
layout: post
title: AWS CSAA
---
## S3

 0 - 5TB file, unlimited storage
universal namspace

Objects as files

* Key, Value, Version ID, Metadata
* Access Control lists
* Torrent

### Data Consistency Model for S3

* Immediate(Read after Write) consistency for PUTS of new Objects
* Eventual Consistency for overwrite PUTS and DELETES

S3 Guaranteens

* Built for 4-9 availability
* Guarantee 3-9 availability
* 11-9 durability(lost risk)

Featured:

* Tiered Storage Available
* Lifecycle Management
* Versioning
* Encryption
* MFA Delete
* Secure data by using **access control lists** and **Bucket policies**

### S3 Storage Classes

* S3 Standard
  		+ designed to sustain the loss of 2 facilities
* S3 - IA
  		+ for data is accessed less frequently
  		+ charged a retrieval fee
* S3 One Zone - IA
  		+ lower-cost option for infrequently accessed data, no multi az resilience
* S3 - Intelligent Tiering
  		+ intellient move between S3 standard - s3 -ia
* S3 Glacier
  		+ super cheap
* S3 Glacier Deep Archive
  		+ retrieve after 12 hours

### Charging

* Storage
* Requests
* Storage Management Pricing
* Data Transfer Pricing
* Transfer Acceletation
* Cross Region Replication Pricing

### Encryption

Encryption In Transit

* SSL/TLS
  Encryption At Rest (Server Side)
* S3 Managed Keys  - SSE-S3
  		+ AWS managed
* AWS Key Management Service, Managed Keys - SSE-KMS
  		+ AWS and you together
* Server Side Encryption With Customer Provided - SSE-C
  	+ You manage the key
  	+ 
  Client Side Encryption

### Versioning

* once enabled, cannot be disabled
* Integrates Lifecycle
* MFa Delete capability
* Versioning will make size increse exponentially.
* Upload will make new object private
  		+ But the old ones still remain the same

### Lifecycle

* Auto move between different storage classes

### Cross-Region Replication

* Versioning must be enabled on both the source and destination buckets
* it will not replicate delete marker or delete version
* files in existing bucket are not replicated automatically.

### Transfer Acceleration

* use cloudfront edge network
* Faster than normal upload

### CloudFront

Content delivery network(CDN)

Edge Location

content to cached. not AWS region/AZ

### Origin

e.g. S3 Bucket, EC2 Instance, an ELB, or Route53

### Distribution

The game give to the cdn consisting of edge locations

* Web Distribution
  		+ Typically used for websites
* RTMP 
  		+ Used for media Streaming

Charge when clear the cashed data(invalidation).
Can restrict the client to use cloudfront url instead of origin url to be more secure
Can restrict the client to used signed url
Cached for the life of TTL

### Snowball

* What is snowball
* snowball can
  		+ import to S3
  		+ Export from S3

### Storage Gateway

What is Storage Gateway
As VM or hardware

Three Flavours:

* File Gateway (NFS & SMB)
  		+ Store Application server data to s3
* Volume Gateway(iSCSI)
  		+ Storing virtual hardisk drive in s3(like ebs snapshot)
  		+ Stored Volumes(flav 1)
  			+ have complete copy of data(on site) and asynchronous backed up to EBS snapshot(S3)
  		+ Cached Volumes(flav 2)
  			+ entire dataset is stored on s3 and the most frequently accessed data is cached on site
* Tape Gateway

## EC2

Pricing Models

* On demand
  		+ without up-front payment or long-term
* Reserved
  		+ steady state or predictable usage
  		+ require reserved capacity
  		+ Types
  			+ Standard
  				+ 75%
  			+ Convertible
  				+ 54%
  			+ Scheduled 
  				+ specific time windows
* Spot
  		+ Flexible start and end times
  		+ useful for applications that feasible at low compute prices
* Dedicated Hosts
  		+ regulatory requirements
  		+ Great for licensing not support multi-tenancy or cloud deployments
  		+ 70% off

### Mnemonic

F - FPGA
I - IOPS
G - Graphics
H - High Disk Throughput
T - Cheap General purpose (T2 Micro)
D - Density
R - Ram
M - Main choice for general purpose apps
C - Compute
P - Graphics
X - Extreme Memory
Z - Extreme Memory And CPU
A - Arm-based workloads
U - Bare Metal

Fight Dr MC PXZ AU

No need to pay partial hour chare if Amazon terminate your spot instance,

Termination Protection isturned off by default
EBS Root Volumes by default cannot be excrypted.
Addtional volumes can be encrypted

### Security Group

* Security group take effects immediately
* Inbound Block by default, no way to block
* Multiple EC2 can have multiple Security groups, and one ec2 can have multiple Security groups
* Outbound Allowed by default
* Outbound rule depend on the inbound rule
  		+ if inbound http, then outbound http
  		+  it's stateful while network access control list is stateless

## EBS

Elastic Block Store
5 types

* General Purpose (SSD)
  		+ most workloads
  		+ 16,000 MAX IOPS
* Provisioned IOPS(SSD)
  		+ 64,000 MAX IOPS
* Throughput Optimised Hard Disk Drive
  		+ Big Data
  		+ 500 GiB - 16 TiB
  		+ 500 MAX IOPS
* Cold Hard Disk Drive
  		+ Files Servers
  		+ 250 MAX IOPS
* Magnetic
  		+ 40-200 MAX IOPS

### Snapshot

Root EBS and EC2 are in the same availability ZOne
Snapshots exist on S3
Snapshots are incremental - delta are moved 
better to create a snapshot when the instance is stopped
EBS volume can be chaned on the fly

If want to change AZ, create a snapshot and image, then launch instance.
If want to move to another region, create a snapshot and image, move the image to another region. Finally launch instance in another region.

### AMI Types(EBS vs Instance Store)

Based on

* Region
* Operating systen
* Architecture
* Launch Permissions
* Storage 
  		+ for the Root Device, 
  		+ Instance STore, 
  		+ EBS Backed Volumes

Instance STore Volumes are sometimes called Ephemeral Storage

* if host fails, all data are lost

EBS can be stopped, data will not be lost.

### ENcrypted Root Device Volumes

snapshots of encrypted volumes are encrypted automatically

* volumes restored from encrypted snapshots are encrypted automatically
* You can share snapshots, but only if they are unencrypted

How to make the runing EC2 with EBS encrypted,

1. Create snapshot of the volumr
2. Copy the snapshot and encrypted it
3. Create AMI from the snapshot
4. Launch an ami with that AMI

### CloudWatch

Monitoring service , monitors performance

* Compute
  		+ EC2
  		+ Autoscaling
  		+ ELB
  		+ Route53 Heal Check
* Storage & Content Delivery
  		+ EBS Volumes
  		+ Storage Gateways
  		+ CloudFront

Host Level Metrics Consist of:

* CPU
* Network
* Disk 
* Status Check

Cloud Trail

* CCTV(auditing)
* manage API Calls, Console monitor

Can create CLoudWatch Alarms

* 

Standard Monitoring = 5 minutes
Detailed Monitoring = 1 Minute

Dashboards

* Creates awesome dashboards to see what is happening with the AWS environment
* Alarms - Allows you to set alarms that notify you when particular thresholds are hit
* Events - CloudWatch Events helps you to respond to state changes in your AWS resources 
* Logs - CludWatch Logs helps you to aggregate, monitor, and store logs

### AWS Command Line (CLI) Lab

* Roles are more secure and easier to manage
* Roles are universal

### Boot Strap Scripts

### EFS

Elastic FIle System
EBS can only mount to one instance
Pay for the storage used
Multiple AZ
Scale up to the petabytes
support thousands of concurrent NFS connections
Read After Write Consistency

### EC2 Placement Groups

* Clustered Placement Groups
  		+ Within a single availability zone
  		+ low network latency, high network throughput
* Spread Placement Group
  		+ On distinct underlying hardware.
  		+ protect from hardware failure
* Partitioned
  		+ Each Partition is on it set of rack
  		+ No two partitions share the same racks
  		+ isolate the hardware failure
  		+ Multiple EC2 Instances HDFS, Hbase, and Cassandra

Can only launch an instance to a placement group. Not mving existing one to the placement one.

## Databases

### Relational Database

* SQL Server
* Oracle
* MYSQL Server
* Postgre SQL
* Aurora 
* MariaDB

Two Key Features

* Multi-AZ
  		+ For Disaster Recovery
  		+ Automatic failover
  		+ Database's url not change
* Read Replicas
  		+ For Performance,scaling
  		+ can have 5 copies of read replica
  		+ Failover not automatic, need to update DNS by hand

### Non Relational Databases

* Collection = Table
* Document = Row
* Key Value = Field/Column
  		+ Nest

### Data Warehousing

* Business intelligence

#### OLTP vs OLAP

RDS (OLTP)

* select or choose

OLAP

* aggregate, calculation, analysis
* complex queries
  ### DynamoDB (No SQL)
  ### Redshift (OLAP)

### ElastiCache

* improve performance , in-memory cache instead of relying entirely on slower disk-based databases.
* cache most common reques
* Speed up performance of existing databases

Caching Engines:

* Memcached
* Redit

RDS runs on virtual machine
 Cannot log in
It's Amazon's responsibility to patching the RDS Operating System and DB
Not Serverless

Aurora Serverless is serverless

### Back Ups, Multi-AZ & Read Replicas

Back Ups

* Automated Backups
  		+ retention period 35 days
  			+ one snapshot and store transaction logs through out the day
  			+ slow when in back up window
* Database Snapshots

Restoring backup will use a new RDS Instance with a new DNS Endpoint

### Encryption At Rest

* Support MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora
* Via Key Management Service(KMS)
* Automated backups, read replicas, and snapshots are all encrypted.

What is Multi-AZ

* Exact copy of production database in another availabilty zone.
* AWS All handles replication
* Disaster Recovery Only, not for performance

What is a read replica

* read only copy of the production database.
* asynchronous replication from the primary rds instance to the read replica.
* primarily for very read-heavy database workloads
* Each replica have its own dns end point
* can have a read replica in a second region
* backup must be turned on
* can be promoted to master, this will break the read replica

### DynamoDB

* NoSQL
* consistent,  Single-digit millisecond latency at any scale.
* stored on ssd storage
* spread across 3 geographically distinct data centres
* eventual consistent reads(Default)
  		+ consistency across copies of data is usually reached within a seconds. Repeating a read after a short time should return the updated data.(Best Read Performance)
* strongly consistent reads
  		+ A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read

### Redshift

* different type of architecture both from a database perspective and infrastructure layer
* Single Node (160Gb)
* Multi-Node
  		+ Leader Node(Manages client connections and receives queries.)
  		+ Compute Node (store data and perform queries and computations). Up to 128 Compute Nodes,
* Advanced Compression
  		+ Compress columns
* Massively Parallel Processing (MPP):
  		+ automatically distrubutes data and query load across all nodes.
  		+ Makes it easy to add nodes to your data warehouse, fast query performance

Backup

* enabled by default 1 day retention period
* maximum retention period is 35 days.
* maintain at least three copies of your data(the original and replica on the compute nodes and a backup in Amazon S3)
* asynchronously replicate snapshots to S3 in another region for disaster recovery

charge for compute node hours, backup, and data transfer

Security

* encrypted in transit using ssl
* encrypted at rest using AES-256 encryption
* By default Redshift takes care of key management
  		+ Manage your own keys through HSM
  		+ AWS Key management Service

Availability

* only available in 1 AZ
* can restore snapshots to new AZs in the event of an outage

### Aurora

* MySQL compatible, relational database.
* five faster than MySql
* Start 10GB, scales in 10 GB increments to 64 TB
* compute resources can scale up to 32vCPUs and 244GB of Memory
* 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones. 6 copies of your data

Scaling

* transparently handle the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability.
* Self healing. Data blocks and disks are continuously scanned for errors and repaired automatically.

Two types of aurora replicas are available:

* aurora replicas (currently 15)
* mySQL read replicas (5)

Backups

* automated backups. Backup do not impace database performance
* can take snapshots with aurora. not impact on performance,
* can share aurora snapshots with other AWS Accounts

### Elastic Cache

* increase database and web application performance
* Memcached
  		+  Simple cache to offload DB
  		+ Ability to scale horizontally
  		+ multi-threaded performance
* Redis
  		+ Simple cache to offload DB
  		+ Ability to scale horizontally
  		+ Advanced data types
  		+ ranking/sorting data sets
  		+ pub/sub capabilities
  		+ persistence
  		+ Multi-AZ
  		+ Backup & Restore Capabilities

## DNS

N, viginia
3.84.248.118
Sydney
54.252.211.97
Tokyo
3.112.149.79

34.201.134.186
54.252.211.97
3.112.149.79

* Simple Routing
  		+ Random order, without health check
* Weighted Routing
  		+ Based on the weight
  		+ can enable healthcheck
  		+ If a record set fails, it will be removed from ROute 53 until it passes the health check
* Latency-based Routing
  		+ based on the lowest network latency for end user
* Failover Routing
  		+ want to create an active/passive set up.
  		+ minitor the health of your active site.
* Geolocation Routing
  		+ Based on geo location
* Geoproximity Routing
  		+ Traffic flow only mode
  		+ complex (out of scope)
* Multivalue Answer Routing
  		+ Simple with health check

## VPC

* launch instances into a subnet of your choosing
* assign custom IP address ranges in each subnet
* Configure route tables between subnets
* create internet gateway and attach it to your vpc
* Much better security control over your aws resources
* instance security groups
* subnet network access control lists(ACLs)

### Default VPC vs Custom VPC

* Default vpc is user friendly, allowing you to immediately deploy instances
* all subnets in default vpc have a route out to the internet
* each ec2 instance has both a public and private IP address

### VPC Peering

* allows you to connect one VPC with another via a direct network route using private IP addresses
* instances behave as if they were on the same private network
* you can peer vpc's with other AWS accounts as well as with other VPCs in the same account.
* Peering is in a star configuration: ie central vpc peers with 4 others. No transitive peering

### NAT Instances & NAT Gateways

* Nat Instances
  		+  disable source/Destination Check on the instance
  		+ must be in a public subnet
  		+ must be a route out of the private subnet
  		+ traffic the nat instances can support depends on the instance size. if bottlenecting, increase the instance size
  		+ create HA using autoscaling groups, multiple subnets in different AZs, and a script to automate failover.
* Nat gateways
  		+ redundant inside the availability zone
  		+ preferred by the enterprise
  		+ starts at 5Gbps and scales currently to 45Gbps
  		+ No need to patch
  		+ not associated with security groups
  		+ rautomatically assigned a public ip address
  		+ remember to update route tables
  		+ no need to disable source/destination checks

### Network Access ControlLists vs Security Groups

* by defalt, comes with a default acl, allowing all outbound and inbound traffic.
* by default, custom network acl denies all inbount and outbound rules.
* each subnet in vpc must be associated with a network acl. if not, by default, it will associate with the default network acl.
* block ip addresses using network acls not security groups
* one subnet can only associated with one network acl at a time
* network acls are stateless.

### custom vpcs and elbs

### VPC Flow Logs

3 levels

* VPC
* Subnet
* Network Interface Level
* Cannot enable flow logs for vpcs that are peered with your vpc unless the peer vpc is in your account
* once flow log is created, cannot change its configuration.

Not all ip traffic is monitored

* traffic generated by instances when they contact the amazon DNS Server
* traffic generated by a windows instance for amazon windows license activation
* traffic to and from 169.254.169.254 for instance metadata
* DHCP traffic
* traffic to the reserved IP address for the default vpc router
* 

### Bastion Hosts

### Direct Connect

* connects data center to AWS
* For high throughput workloads
* need a stable and reliable secure connection

### VPC Endpoints

Two Type Endpoints

* Interface Endpoints
* Gateway Endpoints
  		+ S3
  		+ DynamoDB

5 vpc allows in rach AWS region

## HA

### Elastic Load Balancer

* Application load Balancer
  		+ HTTP/HTTPS
  		+ Application-aware (layer 7)
  		+ intelligent
* Network Load Balancer
  		+ load balancing of TCP
  		+ Connection level(4), extreme performance
  		+ low latency
* Classic Load Balancer
  		+ cost effective	
  		+ sticky sessions

504 error the application is having issues.

X-Forwared-For Header

* store the user's ip address

### Advanced Load Balancer Theory

Sticky Sessions

* bind user session to a specific EC2 instance
* you can enable sticky sessions for application load balancers as well, but the traffic will be sent at the target group level

Cross zone load balancing
Path Patterns

* based on the url containing in the request

### HA Architecture

### Cloud Formation

* completely scripting  the cloud environment
* Quick Start includes a bunch of scriptes that amazon build for different scenerio

### Elastic BeanStalk

* A button (much easier to cloud formation)
* quickly deploy and manage applications, don't need to care about the infrastructure
* just upload the application

## Applications

### SQS

* distributed queue system
* to decouple the components of an application so they run independently
  Two types
* Standard Queue
  		+ might be out of order
  		+ message might be delievered more than once
* FIFO Queue
  		+ First in first out
  		+ order is ensured
  		+ once(no duplicate)
* Messages are 256KB in size
* can be kept in the queue from 1 minute to 14 days. default retention period is 4 days
* visibility time out is the ammount of time the message is invisible in the SQS.
* visibility timeout maximum is 12 hours
* long pooling wait unitil next message arrives
* Mesaage-oriented API

### Simple Work Flow Service

* coordinate work across distributed application components.
* tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.
* workflow executions can last up to 1 year
* task-oriented API
* ensures that a task is assigned only once is never duplicated.
* keeps track of all the tasks and events in an application

swf actors

* workflow starters
  		+ an application that can initiate(start) a workflow. could be website following the placement of an order
* Deciders
  		+ Control the flow of activity taks in a workflow execution. if something has finished(or failed) in a workflow, a Decider decides what to do next
* Activity Workers
  		+ Carry out the activity tasks

### Simple Notification Service(SNS)

* stored in muitiple availability zones
* push based
* easy integration with applications
* pay as you go

### Elastic Transcoder

* Media Transcoder in the cloud
* convert media files from different formats.
* pay by minutes and resolution

### API Gateway

* fully managed service that makes it easy for developers to publish, maintain, monitor and secure APIs at any scale
* Expose HTTPS enpoint to define a RESTful API
* serverlessly
* send each API endpoint ot a different target
* run efficiently with low cost
* scale effortlessly
* track and control usage by API key
* Throttle requests to prevent attacks
* connect to cloudwatch to log all requests for monitoring

API Gateway Caching
Same Origin Policy

* prevent cross-site scripting(XSS)

CORS

* one way the server at the other end can relax the same-origin policy
* Cross-origin resource sharing(cors) is a mechanism that allows restricted resources on a web page to be requested from anther domain outside the domain from whch the first reosurce was served.

### Kinesis

Three types

* Kinesis Streams
  		+ place to store the data
  		+ 24 hour - 7 days retention
  		+ containing in shard
  			+ shard, 5 transactions per second for reads, up to a maximum total data read rate of 2 MB per second, up to 1,00 records per second for writes, up to a maximum total data write rate of 1 MB per second
* Kinesis Firehose
  		+ optional to have analystics function and output to like S3 or to Redshift
  		+ no data persistence
* Kinesis Analytics
  		+ can analyze the data on the fly

### Web Indentity Federation & Cognito

* Sign-up and sign-in to your apps
* cognito brokerw between the app and Facebook or Goole to provide temporary credentials which map to an IAM role allowing access to the required resource.
* No need for the application to embed or store AWS credentials locally on the device and it gives users a seamless experience across all mobile devices

User Pools are user directories used to manage sign-up and sign-in functionality for mobile and web applications. Successful authentication generates a JSON Web token(JWTs).

IdentityPools enable provide temporary AWS credentials to access AWS services like S3 or DynamoDB. For authorization.

* User pool is user based. It handles things like user registration, authentication and account recovery.
* Identity pools authorise access to your AWS resouces

Cognito Synchronisation

## Serverless

### Lambda

* no os, patches
* as an event-driven compute service. triggers
* as a compute service
