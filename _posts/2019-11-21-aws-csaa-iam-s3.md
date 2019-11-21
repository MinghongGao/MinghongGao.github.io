---
layout: post
title: AWS CSAA IAM & S3
---
## S3
 0 - 5TB file, unlimited storage
universal namspace

Objects as files
+ Key, Value, Version ID, Metadata
+ Access Control lists
+ Torrent

### Data Consistency Model for S3
+ Immediate(Read after Write) consistency for PUTS of new Objects
+ Eventual Consistency for overwrite PUTS and DELETES

S3 Guaranteens
+ Built for 4-9 availability
+ Guarantee 3-9 availability
+ 11-9 durability(lost risk)

Featured:
+ Tiered Storage Available
+ Lifecycle Management
+ Versioning
+ Encryption
+ MFA Delete
+ Secure data by using **access control lists** and **Bucket policies**

### S3 Storage Classes
+ S3 Standard
	+ designed to sustain the loss of 2 facilities
+ S3 - IA
	+ for data is accessed less frequently
	+ charged a retrieval fee
+ S3 One Zone - IA
	+ lower-cost option for infrequently accessed data, no multi az resilience
+ S3 - Intelligent Tiering
	+ intellient move between S3 standard - s3 -ia
+ S3 Glacier
	+ super cheap
+ S3 Glacier Deep Archive
	+ retrieve after 12 hours

### Charging
+ Storage
+ Requests
+ Storage Management Pricing
+ Data Transfer Pricing
+ Transfer Acceletation
+ Cross Region Replication Pricing

### Encryption
Encryption In Transit
+ SSL/TLS
Encryption At Rest (Server Side)
+ S3 Managed Keys  - SSE-S3
	+ AWS managed
+ AWS Key Management Service, Managed Keys - SSE-KMS
	+ AWS and you together
+ Server Side Encryption With Customer Provided - SSE-C
	+ You manage the key
	+ 
Client Side Encryption

### Versioning
+ once enabled, cannot be disabled
+ Integrates Lifecycle
+ MFa Delete capability
+ Versioning will make size increse exponentially.
+ Upload will make new object private
	+ But the old ones still remain the same

## Lifecycle
+ Auto move between different storage classes

### Cross-Region Replication 
+  Versioning must be enabled on both the source and destination buckets
+ it will not replicate delete marker or delete version
+ files in existing bucket are not replicated automatically.

### Transfer Acceleration
+ use cloudfront edge network
+ Faster than normal upload


## CloudFront
Content delivery network(CDN)

### Edge Location
content to cached. not AWS region/AZ

### Origin
e.g. S3 Bucket, EC2 Instance, an ELB, or Route53

### Distribution
The game give to the cdn consisting of edge locations


+ Web Distribution
	+ Typically used for websites
+ RTMP 
	+ Used for media Streaming

Charge when clear the cashed data(invalidation).
Can restrict the client to use cloudfront url instead of origin url to be more secure
Can restrict the client to used signed url
Cached for the life of TTL

## Snowball
+ What is snowball
+ snowball can
	+ import to S3
	+ Export from S3

## Storage Gateway
What is Storage Gateway
As VM or hardware

Three Flavours:
+ File Gateway (NFS & SMB)
	+ Store Application server data to s3
+ Volume Gateway(iSCSI)
	+ Storing virtual hardisk drive in s3(like ebs snapshot)
	+ Stored Volumes(flav 1)
		+ have complete copy of data(on site) and asynchronous backed up to EBS snapshot(S3)
	+ Cached Volumes(flav 2)
		+ entire dataset is stored on s3 and the most frequently accessed data is cached on site
+ Tape Gateway


