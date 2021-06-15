# Simple Storage Service (S3)

## Introduction
S3 provides Object-based storage, which is a safe place to store your files. The data is spread across multiple devices and facilities.

The basics of S3 are as follows:

- S3 is Object-based, which allows you to upload files.
- Files can be from 0 bytes to 5 TB and there is unlimited storage.
- Files are stored in Buckets which must be unique globally since S3 is a universal namespace.
- S3 returns HTTP 200 Code when you upload a file.

S3 is Objected-based, in which Objects consist of the following:

- Key (Simply the name of the object)
- Value (Simply the data and is made up of a sequence of bytes)
- Version ID (Important for versioning)
- Metadata (Data about data you are storing)
- Subresources: Access Control Lists, Torrent.

How does data consistency work for S3?

- Read after Write consistency for PUTS of new Objects, which means that you will be able to view the data if you write a new file and read it immediately afterwards.
- Eventual Consistency for overwrite PUTS and DELETES, which means that you may either get the old version or the latest one if you update an existing file or delete a file. Basically changes to objects can take a little bit of time to propagate.

S3 has the following features:

- Tiered Storage Available
- Lifecycle Management
- Versioning
- Encryption
- MFA Delete
- Secure your data using Access Control Lists and Bucket Policies.

AWS charges for S3 in the following ways:

- Storage
- Requests
- Storage Management Pricing
- Data Transfer Pricing
- Transfer Acceleration

### S3 Storage Tiers

- S3 Standard: S3 guarantees 99.99% availability and much higher durability, stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.
- S3 Standard-IA (Infrequently Accessed): For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but are charged a retrieval fee.
- S3 One Zone-IA: For where you want a lower-cost option for infrequently accessed data, but don’t require the multiple Availability Zones data resilience.
- S3 Intelligent-Tiering: Designed to optimize costs by automatically moving data to the most cost-effective access tier, without performance impact for operational overhead.
- S3 Glacier: S3 Glacier is a secure, durable, and low-cost storage class for data archiving. REtrieval times configurable from minutes to hours.
- S3 Glacier Deep Archive: S3’s lowest-cost storage class where a retrieval time of 12 hours is acceptable.

### S3 Security and Encryption

By default, all newly created buckets are private. You may use Bucket Policies and Access Control Lists to manage access to your bucket. Each bucket can be configured to create access logs which will log all requests made to the S3 bucket. This can be sent to another bucket even if it is located in separate account.

Encryption in transit is achieved by SSL/TLS.

Encryption at rest (server side) is achieved by:

- SSE-S3: S3 Managed Keys
- SSE-KMS: AWS Key Management service
- SSE-C: Customer Provided Keys

Client Side Encryption (Simply encrypt objects before uploading them to S3.)

### S3 Versioning

S3 will stores all versions of an object, including all writes and even if you delete an object, which is an effective backup tool. Once enabled, versioning cannot be disabled, only suspended. It also integrates with Lifecycle rules. Versioning’s MFA delete capability can be used to provide an additional layer of security.

### Lifecycle rules

Lifecycle rules allow you to automatically move your objects between the different storage tiers, can be used in conjunction with versioning, and can be applied to current versions and previous versions.

### Cross Region Replication

Cross region replication allows you to sync files between buckets located in different regions, considering the following features:

- Versioning must be enabled on both the source and destination.
- Regions must be unique.
- Files in an existing bucket are not replicated automatically.
- All subsequent updated files will be replicated automatically.
- Delete markers, as well as deleting individual versions or delete markers themselves are not replicated.

### S3 Transfer Acceleration

S3 Transfer Acceleration utilizes the CloudFront Edge Network to accelerate your uploads to S3. Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an edge location which will then transfer that file to S3.

## CloudFront

CloudFront is a CDN that deliver webpages and other web content to a user based on the geolocations of the user, the origin of the webpage, and a content delivery server.

- Edge location: The location where content will be cached for the life of the TTL, which is separate to an AWS region/AZ. (They are not just READ only, which means that you can write to them.) You can clear cached objects, but you will be charged.
- Origin: The origin of all the files that the CDN will distribute. This can be an S3 bucket, and EC2 instance, an Elastic Load Balancer, or Route53.
- Distribution: The name given the CDN which consists of a collection of Edge locations.
- Web Distribution: Typically used for websites.
- RTMP Distribution: Typically used for Media Streaming.

## Snowball

Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of AWS with relatively low costs.

Typical Snowball comes in either a 50TB or a 80TB size; however, AWS Snowball Edge is a 100TB data transfer device with on-board storage and compute capabilities, such as Lambda functions.

Insanely, Snowmobile is an exabyte-scale data transfer service used to move extremely large amounts of data (100PB) to AWS.

## Storage Gateway

Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration between an organization’s on-premises IT environment and AWS’s storage infrastructure.

There are three different types of Storage Gateway:

- File Gateway (NFS and SMB)
- Volume Gateway (iSCSI) (Stored Volumes and Cached Volumes)
- Tape Gateway (VTL)

For File Gateway, files are stored as objects in your S3 buckets, accessed through an NFS mount point. Once transferred to S3, objects can be managed as native S3 objects and be applied to bucket policies such as versioning, lifecycle management, and cross region replication.

For Volume Gateway, data written to these volumes can be asynchronously backed up as point-in-time snapshots of your volumes, and stored in the cloud as Amazon EBS snapshots, which are incremental backups that capture only changed blocks and are compressed to minimize your storage charges.

Stored Volumes let you store your primary data locally, while asynchronously backing up that data to AWS, and allows you to access the entire datasets with low latency.

Cache Volumes let you use S3 as the primary data storage while retaining frequently accessed data locally in your storage gateway.

For Tape Gateway, you can archive your data in the AWS Cloud.
