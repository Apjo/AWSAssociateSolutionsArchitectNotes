# AWS Associate Solutions Architect Notes
These are the notes I have prepared while doing the online course for `AWS Associate Solutions Architect` on Udemy(2015-2017) 

The course is taught by [Ryan Kroonenburg](https://www.udemy.com/user/ryankroonenburg/).

# What do I need for this course:
- AWS account Free tier
- Domain name(optional)
- A Laptop with internet connection

# History of AWS:
It all started with **Chris Pinkman** and **Benjamin Black** presenting a paper on Amazon’s internal infrastructure, 
and requested the CEO to sell it as a service, while preparing a business case

Following are the sequence of events:

    1.  2004, SQS launched
    2.  2006, AWS launched officially
    3.  2007, More than 180k dev moved or started using AWS
    4.  2010, All of Amazon moved to the AWS platform
    5.  2012, First re:invent
    6.  2013, Certifications
    7.  2014, Committed to aachieve 100%  renewable enery usage
    8.  2015, Revenue hits a new high of USD $6 billion per year
    9.  2016, Run rate of $13 billion

### AWS Solutions Architect-Introduction:
- forums: forums.acloud.guru
- Exam blueprint 
[Example exam blueprint](http://awstrainingandcertification.s3.Amazonaws.com/production/AWS_certified_solutions_architect_associate_blueprint.pdf)

<a name ="toc"></a>
### Table of Contents
* [Concepts and Components](#concepts_introduction)
* [IAM](#i_am)
* [S3](#s_3)
    * [S3 Versioning](#s_3_versioning)
    * [S3 Lifecycle Management](#s_3_lifecycle_mgmt)
    * [S3 Encryption](#s_3_encryption)
    * [S3 Security](#s_3_security)
    * [S3 Transfer Acceleration](#s3_ta)
    * [S3 Static website](#s3_static_website)
    * [S3 Exam Tips](#s3_exam_tips)
* [CloudFront](#cloudfront)
    * [CloudFront Exam Tips](#cloudfront_exam_tips)
* [Storage Gateway](#storage_gateway)
* [Snowball](#snowball)
* [Import/Export](#import_export)

<a name ="concepts_introduction"></a>
# Concepts and Components:

   1.   **AWS Global Infrastructure**:
   
        1. Regions: A place where AWS resources exists a geographical area, there are 15 regions (as of 2015).
            Each region consists of multiple availability zones, currently 49 in total(as of 2017).
            An Availability Zone(AZ) is simply a data center.
        
        2. Edge location: This is a CDN(Content-Delivery Network) endpoint. Edge locations are used by CloudFront 
            to cache files near the user where they access them.
        
        3. CDN: A content delivery network (CDN) is a system of distributed servers that deliver webpages,
            and other web content to a user based on the geographic locations of the user,
            the origin of the webpage and a content delivery server.
        
        There are many more edge locations than there are regions. Currently 52 edge locations around the world
        
   2.   **Networking**:

        1. Route 53: Amazon’s DNS service, basically allows you to host your domain name with Amazon. 
            53 is the DNS port. When you open up DNS world you do this on port 53
            
        2. Direct connect: Allows you to connect directly to where your Virtual Private Cloud(VPC) is located
            using connection links to Amazon data center into your VPC, and you don't need internet to access it
            
        3. Virtual Private Cloud: A virtual data center as a collection of AWS resources, such as EC2 instances, 
            EBS instances, and Load Balancers
            
        4. CloudFront: Part of the CDN, consisting of edge locations to cache your assets, like videos, large media
            files etc.
            
        5. Direct Connect: Connecting your office or physical data centers to AWS using a dedicated telephone line
            
   3.   **Compute Elements**:
   
        1. EC2: Known as Elastic Cloud Compute, allowing one to provision instances inside your VPC, these are
            just virtual machines in the cloud that run on AWS
            
        2. EC2 Container Service: highly scalable, high performance container management service, supporting Docker
            containers, allowing you to run applications on a managed cluster of EC2 instances, eliminating the need
            to install, operate and scale your own cluster management infrastructure
               
        3. Elastic Beanstalk: An easy to use service for developing and scaling web apps developed in 
            Java, Dot Net etc., we can simply upload the code and EB will automatically handle the deployment from 
            capacity provisioning, load balancing, autoscaling, app health and monitoring.
        
        4. Lambda: Is Serverless. Upload your code to respond to events.
        
        5. Lightsail: A completely brand new service introduced in 2016. Allows anyone who does not understand AWS 
            to deploy a site in a few seconds
                
   4.   **Storage**:
        1. S3(Simple Storage Service): S3 is a file-based storage or object based storage.
            Allows us to store files in the cloud of sizes ranging from 1 byte to 5 terabytes
               
        2. Glacier: Is an archiving service. Allows us to archive all our data in the Amazon cloud,
             not immediately accessible but take 3-5 hours to restore a file from Glacier,hence used for long-term storage
                   
        3. EFS(Elastic File service): File based storage and you can share it, you can install databases, applications.    
           
        4. Storage gateway: A service that connects on-premise software appliance with cloud based storage 
            to provide seamless and secure integration between organizations on premise IT equipment and AWS storage infrastructure.

   5.   **Databases**:
   
        1. RDS(Relational Database Services): Consists of elements such as SQLServer by MS, Oracle, PostgreSQL, MySQL, 
            and Amazon’s own database engine known as Aurora completely MySQL compatible db but designed to run specifically 
            on the AWS platform.
        
        2. DynamoDB: For NoSQL
        
        3. RedShift: A fast, fully-managed petabyte scaled datawarehousing solution,
            that makes it simple and cost-effective to efficiently analyze your data using your existing BI tools. 
            It is designed from the infrastructure layer upwards to maximize performance and minimize cost.
                 
        4.  Elastic Cache: Allows/offers an in-memory caching service for the AWS platform.
   
   6.   **Migration**
   
        1. Snowball: This is a data transport solution that uses secure appliances to transfer large amounts of data,
            into and out of AWS. It addresses common challenges with large-scale data transfers such as high network costs, 
            long transfer times, and security concerns.
            
        2. DMS(Database Migration services): This allows migration of on-premise databases to AWS cloud
        
        3. SMS(Server Migration Service): does same work as the DMS but targets virtual machines,
            to replicate vms to aws cloud
                    
   7.  **Analytics**:
   
        1. Athena: SQL queries on S3. 
            
        2. Kinesis: Is a fully-managed service for real-time processing of streaming data at massive scale. 
            Can continuously change and store terabytes of data per hour from several sources such as website clickstreams, 
            social media, location tracking event. With Kinesis client library ACL, we can build Amazon Kinesis apps, 
            and use streaming data to power real time dashboards, generate alerts, 
            implement dynamic pricing and advertising and more. We can emit data from Kinesis to other AWS services such as 
            S3, redShift, Elastic MapReduce, and lambda.
            
        3. ElasticMapReduce(EMR): A web service that makes it easy to quickly and cost-effectively process vast amounts of data. 
            Uses Hadoop, an open source framework to distribute your data and process across a resizeable cluster of 
            Amazon EC2 instances. It can also run other distributed framework such as Spark and Presto. 
            EMR is used in a variety of applications including log analysis, web-indexing, data warehousing, 
            machine learning, financial analysis, scientific simulation, and Bioinformatics, 
            customers launch millions of Amazon’s EMR clusters each year.
            
        4. Cloud Search / Elastic Search: Search engine for your website or your application, 
            Cloud search is fully managed service provided by AWS, Elastic search uses open source framework
            
        5. Data Pipeline: Allows to move data from one place to another
        
        6. Quick Sight: used for creating visualizations, dashboards for BI/Analytics
             
   8.   **Security and Identity**:
   
        1. IAM(Identity Access Management): Enables you to securely control access to AWS services and resources for your users
            We can create and manage AWS users and groups and use permissions to allow and deny their access to AWS resources
            
        2. Inspector: An agent to install on vms to inspect and does security reporting on whats going on
        
        3. Certificate Manager: Gives free SSL certificates for your domain names.
        
        4. Directory Service: A way of using active directory which you use with Microsoft with AWS.
        
        5. WAF(Web application Firewalls): Application level protection to your website .    
                       
   9.   **Application Services**:
   
        1. Step Functions: A way of visualizing what's going on inside your application.
        
        2. API Gateway: Acts as a door to create, publish, monitor, maintain, and secure API at scale using AWS.
        
        3. AppStream: Streaming desktop applications to your users.     
        
        4. SWF(Simple Work Flow Service): Helps developers to build, run, and scale background jobs that have parallel 
            or sequential steps.
        
        6. Elastic Transcoder: A media transcoding service in the cloud. Designed to be highly-scalable, easy to use in a 
            cost-effective way for developers and businesses to convert or transcode media files from their source formats 
            to version that will play on devices like smartphones, tablets etc.
    
   10.	**Deployment and Management**:

        1. CloudWatch: A monitoring service for AWS Cloud resources and the apps you run on AWS. 
            Used for collecting and tracking metrics, collect and monitor log files, and set alarms. 
            It can monitor AWS resources, such as EC2 instances, DynamoDB tables, and RDS DB instances, 
            as well as custom metrics generated by your apps and services, and log any files your app generates. 
            We can use it to gain system-wide visibility into resource utilization, app performance, 
            and operational health.
            
        2. CloudTrail: A logging, and auditing service, a web service that records API call for your account
            and deliver log files to you. We can get history of AWS API calls for your account, including calls made by 
            AWS management console, SDKs, Command line tools, and high level AWS services such as AWS cloud formation.
            
        3. Cloud Formation: Gives developers, and sys admins an easy way to create and manage a collection of related 
            AWS resources, provisioning and updating them in an orderly and predictable fashion.
            
        4. OpsWorks: Automating deployments using chef.
        
        5. Config Manager: proactively monitor changes to your environment.
        
        6. Service Catalog: Allows you as an enterprise to build out what it is that you authorize within your organization.
        
        7. Trusted Advisor: tips on cost optimization, performance optimization, security fixes etc.
    
   11.  **Developer Tools**:
        1. CodeCommit: GitHub's way of storing your code in the cloud.
        2. CodeBuild: way of compiling code.
        3. CodeDeploy: deploying code to your Ec2 instances.
        4. CodePipeline: keeping track of different versions of your code.
        
   12.  **Mobile Services**:
        1. Mobile Hub: Add, configure features for your mobile apps. It is its own console for mobile apps.
        2. Cognito: Makes easy for singup and sign into your apps.
        3. Device Farm: Improve quality of ios, aos, fireos, by quickly, and securely testing on 100 smartphones.
        4. Mobile analytics: allows to simply and cost effectively analyze app usage data.
        5. Pinpoint: Google analytics for your mobile apps.
   
   13.  **Business Productivity**:
        1. WorkDocs: Securely storing work documents in the cloud.
        2. WorkMail: Exchange for AWS, sending, receiving emails.
        
   14.  **Internet Of Things**:
        Keeping track of thousands, millions or billions of devices out there
   
   15.  **Desktop & AppStreaming**:
        1. WorkSpaces: Basically a VDI. Desktop in the cloud.
        2. AppStream 2.0: Streaming desktop apps to your users.
                                
   16.  **Artificial Intelligence**:
        1. Alexa: Voice service in the cloud. 
        2. Lex: No longer need echo to communicate. 
        3. Polly: Text to voice service.
        4. Machine Learning: 
        5. Rekognition
        
   17.  **Messaging**:
        1. SNS(Simple Notification Service): A fast, flexible, fully-managed push messaging service,
            makes it simple and cost-effective to push notifications to all mobile devices including Apple, Google, FireOS,
            and Windows devices, and Android devices as well.  
        2. SQS(Simple Queue Service): A fast reliable, scalable and fully-managed messaging queueing service. 
            SQS makes it simple and cost-effective to decouple the components of a cloud application. 
            We can use SQS to transmit any volume of data at any level of throughput, without losing messages or 
            other services to be available.
        3. SES(Simple Email Service): A cost-effective outbound only email sending service. 
            We can send transactional emails,marketing messages etc, and get to pay for what we use. 
            Along with high-deliverability SES provides, easy, real-time access to your sending statistics, 
            and built-in notifications for bounces, complaints, and deliveries to help you find tune your 
            cloud-based email sending strategy
                                 
   After AWS resources are deployed we can update or modify in a controlled manner,
   and predictable way in effect applying version control to your AWS infrastructure.
   
[Back to Table of Contents](#toc)

<a name ="i_am"></a>
#  IAM(Identity and Access Management)
Allows us to manage users and their level of access to the AWS console.

**Features of IAM**:
- Centralized control of your AWS account
- Integrated with existing active directory account and allows single sign on
- Has fine grained access to the AWS resource
- Access available on user/group/roles
- Allows Multifactor authentication
- Provides temporary access for users,and devices and services where necessary
- Allows us to set up password rotation policy
- Integrates with many other aws services
- supports compliance
- A universally available service, not restricted to a particular region

**High Level Concept**:
- User: An end user
- Group: A collection of users under one set of permissions
- Roles: Similar to a group, but you can assign both users and AWS resources(EC2).
- Policies: document defining 1 or more permissions

**Each Role has a policy template**.
- Administrator Access: Full access to AWS services and resources
- Power User Access:    Full access except for management of users and groups
- Read Only Access:     Read only access to the resources

More granular access depending on the resources required such as S3 access.

**Configure IAM**:
- root account gives you unlimited access to do things in the cloud
- Multifactor authentication: Is simply where you have a second means to verify yourself when signing in.
Since passwords can be compromised, with multi factor authentication is basically a second way of authenticating you.

**Creating a role**: 
A secure way to grant permissions to entities that you trust
Eg:
- IAM users in another account
- Application code running on EC2 instances needs access to other AWS services

**Summary**:
IAM consists of the following:
- Users
- Groups(group users and apply policies to them)
- Roles
- Policy documents
- Root account has complete admin access when you first set up your AWS account
- IAM does not apply to any region at this time
- New users have no permissions, they have AccessKeyId, and secret access keys when they are first created
- Access key ids and secret keys cannot be used as passwords to login to the console, we use them to access AWS via API or CLI
- Set up MFA on root account, always
- create and customize your own password rotation policies
- power user access allows access to all AWS resources except for mgmt of groups and users within IAM

[Back to Table of Contents](#toc)

# Active Directory Integration:
### How is it done?
Imagine a user is at home, and he wants to login to the AWS console, and they are working on their own home network
So they haven’t already signed-in into the work network.

What they(users) would do is to browse to a URL, for eg: /ADFS/LS/IDPInitiatedSignOn, 
and this is basically an ADFS server that sits inside a DMZ inside someone’s corporate network. 
You browse to that link and it would give you a user name and password depending on your browser,
but basically it prompts you to sign in using your active directory credentials. 
It is also known as Single-Sign On or SSO
 
- We type our SSO in there and sign into active directory environment. When we perform this step we receive a SAML assertion.
- SAML basically stands for **Security Assertion Mark-Up Language**.
  SAML assertions is in the form of an authentication response from the ADFS. 
- We receive a cookie that is stored inside our browser that says that you are signed on.
- Our browser then points to the SAML assertion to the AWS sign on endpoint for SAML. 
- Behind the scenes the sign-in users assume the role with SAML API to request temporary security credentials,
  and then constructs a sign-in URL for the AWS management console. 
- This will login to the AWS Web console. 

**Questions**:
Can you authenticate with Active Directory: Yes, using SAML authentication
A: Whether or not you are authenticating to active directory first and then given a security credential or,
if you get the temporary security credential first, which is then authenticated against the active directory?
A: You always authenticate against active directory first and then you would be assigned the temporary security credential

### AWS Object Storage and CDN - S3, Glacier and CloudFront
<a name ="s_3"></a>
**S3**:
S3(Simple Storage Service) provides developers and IT teams with highly scalable, durable, secure object storage. 
Amazon S3 is easy to use, with a simple web service interface to store and retrieve any amount of data from anywhere on the web.

**S3 Essentials**:

    1. S3 is object based i.e. it allows you to store, and upload files on the platform. Cannot install OS or databases on S3
    2. Files can be from 1 byte to 5tb in size
    3. There is unlimited storage 
    4. Files are stored in buckets(any directory like we have on Windows or Linux files system)
    5. Buckets have a unique namespace for each given region, that is, names must be uniqe globally
    6. S3 being object based, objects consists of the key(name of the object), and value(data, made of sequence of bytes), and 
        VersionId(versioning), metadata(data about data), subresources(ACLs), and torrent 
    7. Built for 99.99% availability on S3 platform. Amazon guarantees 99.9% availability or the S3 platform. 
    8. Amazon also guarantees 99.999999999% durability for S3 information.
        Durability is simply, if you think of storing a file on a disc set that’s a RAID 1 and you lose one of the discs,
        since we are in the RAID 1 configuration which is a mirror, all your information is stored across 2 disks, 
        so you can afford the loss of 1 disc. The way Amazon structures S3 is that if we store 10,000 files 
        that will guarantee that those 10,000 files will stay there with above guarantee %age of durability
    10. S3 allows you to do lifecycle management as well as tiered storage options
    11. S3 also allows you to encrypt your buckets

**Data Consistency model for for S3**:
- Read after write consistency for PUTS on new objects
- Eventual consistency for overwrite PUTS and DELETES, i.e. if you update an object or delete an object,
    it will take some time for that to be consistent across different facilities or inside S3 bucket.
     
**S3 storage tiers and classes**:
- _Standard S3 storage_: _**99.99% availability**_, and _**99.999999999% durability**_
- _S3 - IA(Infrequently accessed)_: data that is accessed less frequently, but requires rapid access when needed, lower fee
    than S3, but charged on retrieval
- _Reduced Redundancy Storage(RRS)_: still has _**99.99% availability**_ but only _**99.99% durability**_ over a given year 
    So, basically it is a little bit cheaper to Reduced Redundancy storage,
    but you only want to store files on them that are not important if you lose them.
    Only use Reduced Redundancy storage for replaceable data,so for example if you store 10,000 files so you could expect 
    to lose 100 files over a year as opposed to 0.0001 file with standard storage.
- _Glacier_: An extremely low-cost storage service for data archival. 
    Amazon Glacier stores data for as little as $0.01 per gigabyte per month,
    and is optimized for data that is infrequently accessed and for which retrieval times of 3-5 hours are suitable

**S3 Charges**:
- Storage: the more the storage you use, the cheaper it becomes
- Requests: # of requests
- Storage management pricing - add tags while storing data in S3, and allows you to control costs, charged on per tag basis
- Data Transfer pricing: Data coming in is free, data moving around, replication is charged
- Transfer acceleration: fast, easy, and secure transfer of files over long distances between your end users and an S3 bucket

<a name ="s_3_versioning"></a>    
**S3 Versioning**:
- Stores all the versions of an object(including all writes and even if you delete and object).
    For example you might have a word file that says “Hello,World”, and you have saved it to your S3 bucket,
    you might then go in and update that file with “hello”. Now, you have 2 versions of that file on your S3 bucket.
- Great backup tool, once enabled,versioning cannot be disabled but only suspended
- Integrates with Lifecycle rules
- Versioning’s MultiFactorAuthentication(MFA) Delete capability, which uses multi-factor authentication,
  can be used to provide an additional layer of security.
- Cross region Replication, requires versioning enabled on the source bucket

**S3 Versioning Exam Tips**:
- Stores all versions of the object(all writes and deletes)
- Great backup tool
- Once enabled, versioning cannot be disabled, only suspended
- Integrates with lifecycle rules
- Versioning's MFA delete capability, which uses multi-factor authentication, can be used to provide additional security
- cross region replication requires versioning enabled on the source bucket

<a name ="s_3_lifecycle_mgmt"></a>
**S3 Lifecycle management**:
- Can be used in conjunction with versioning
- Can be applied to current versions and previous versions.
- Following actions are allowed in conjunction with or without versioning:
    - archive to Glacier storage class(30 days after IA, if relevant)
    - permanent delete
    - archive and permanent delete
    - transition to the Standard: Infrequent Access Storage class(128kb and 30 days after the creation date)

**S3 Lifecycle management Exam tips**:    
- Can be used with versioning
- Can be applied to current and previous versions
- Following actions can  now be done
    - Transition to Standard-IA(128kb and 30 days after creation date)
    - Archive to glacier storage class(30 days after IA)
    - permanently delete

<a name ="s_3_encryption"></a>      
**S3 Encryption**:
- In Transit: 
    You can upload/download your data to S3 via SSL Encrypted end points and S3 can automatically encrypt your data at rest.
- At Rest:
    - Server side encryption(SSE)
     1) S3 managed keys- SSE-S3
     2) AWS Key Management service, managed keys SSE-KMS
     3) Server Side Encryption with Customer provided keys- SSE-C
    - Client Side Encryption: you encrypt data on client side

<a name ="s_3_security"></a>
**S3 Security**:
- All buckets are PRIVATE by default. That means, if you were to type in the buckets publicly accessible URL address,
  and it’s not a publicly available bucket, you wouldn’t be able to access object within that bucket.
  You would have actually go in and make that bucket public 
- Allows Access Control Lists (an individual user can only have access to 1 bucket and have read only access)
- Integrates with IAM using roles,for example allows EC2 users to have access to S3 buckets by roles
- All endpoints are encrypted by SSL
- S3 buckets can be configured to create access logs which log all the requests made to the S3 bucket.
  This can be done to another bucket

**S3 Functionality**:
- Static websites can be hosted on S3. No need for webservers, you can just upload a static `.html` file to an S3 bucket and
  take advantage of AWS S3’s durability and High Availability
- Integrates with Cloud Front CDN,which is Amazon’s own Content Delivery Network
- Multipart uploads, allows you to upload parts of a file concurrently
- Suggested for files over 100MB.It is required for any files over 5GB
- Allows us to resume a stopped file upload
- S3 is spread across multiple availability zones, and they guarantee Eventual consistency.
   All AZ’s will eventually be consistent. Put/Write/Delete requests will eventually be consistent across AZ’s

**S3 use Cases**:
- File shares for networks
- Backup/archiving
- Used as an origin for CloudFront’s Content Distribution Network 
- Hosting static files
- Hosting static websites

<a name ="s3_ta"></a>
# S3 transfer acceleration
- accelerates uploads to S3 using CloudFront edge networks
- makes use of a distinct url to upload to a edge location which will then transfer to S3
- costs extra, and has the greatest impact on people who are in far away location

# S3 static websites
- Use S3 to host static websites
- Serverless
- Very cheap, scales automatically
- STATIC only, cannot host dynamic sites

# Q. What is the correct format for a static website hosting?
Ans: [bucket_name].[s3-website-][valid-aws-region][.aws.amazon.com]

[Back to Table of Contents](#toc)

<a name ="s3_exam_tips"></a>
**S3-Exam tips**:
- *Object based*, only store files, not suitable to install an Operating System
- Files are stored in buckets
- Files can be 0 Bytes to 5TB
- Unlimited storage
- S3 bucket name always looks like https://s3-<valid-aws-region-name>.amazonaws.com/<buket-name>
- Unique namespace, i.e. names must be unique globally, and all lower case
- *Read after Write consistency for PUTS of new objects*
- *Eventual consistency overwrites for PUTS and DELETES*
- S3(durable, immediately available, frequently accessed)
- S3-IA(durable, immediately available, infrequently accessed)
- S3-Reduced Redundancy Storage(data that is easily reproducible)
- Glacier- archived data, wait for 3-5 hours before accessing
- Core fundamentals of S3 object:
   - key(name), names are lexographically stored in order
   - value(data)
   - version ID
   - metadata
   - Subresources
    - ACLs
    - Torrent  
- Successful uploads will generate a HTTP 200 status code
- You can load files to S3 much faster by enabling multipart upload
- **Read the S3 FAQ manual before taking the exam!!!**

**S3 Lab-Exam tips**:
- Buckets are a universal namespace
- Upload an object to S3 receive a HTTP 200 code
- 3 different types of storage S3, S3-IA, S3 reduced redundancy storage
- Encryption: 
  - Client side encryption
  - Server side encryption
     1) Server side encryption with Amazon S3 managed keys(SSE-S3)
     2) Server side encryption with KMS(SSE-KMS)
     3) Server side encryption with customer provided keys(SSE-C)
- Control access to buckets using either a bucket ACL or using bucket policies
- **by DEFAULT buckets are PRIVATE & ALL OBJECTS stored inside them are PRIVATE**

**Cross region replication for S3-Exam Tips**:
- Versioning must be enabled on both source and destination buckets
- Regions must be unique
- Files in an existing bucket are not replicated automatically.
  All subsequent updated files will be replicated automatically.
- You cannot replicate to multiple buckets or use daisy chaining(at this time)
- Delete markers are replicated
- Deleting individual versions or delete markers will not be replicated

[Back to Table of Contents](#toc)

<a name ="cloudfront"></a>
# CloudFront:
- A CDN is a system of distributed servers (network) that deliver webpages and other web content to a user
   based on the geographic location of the user, the origin of the webpage and a content delivery server. 
- CloudFront can be used to deliver your your entire website, including dynamic, static, streaming,
   and interactive content using a global network of edge locations. 
- Requests for your content are automatically routed to the nearest edge location,
   so content is delivered with the best possible performance. 
- Objects are cached for the life of the TTL(time to live). 
- You can clear cached objects, but you will be charged.
- Works well with S3, EC2, Route53, ELB, also works fine with non-aws origin server,
  which stores original, definitive version of your file.
  
**Terminologies**:

**Edge Location**: The location where the content will be cached, this is different from AWS Region/ AZ.
    Currently, 50 edge locations in the world.

**Origin**: This is the origin of all the files that the CDN will distribute.
    This can be either an S3 bucket, an EC2 instance, or an ELB or Route53.
    This may not be registered with AWS you can have your own custom origin servers.

**Distribution**: Name given to the CDN which consists of a collection of Edge Locations

**Web distribution**: Used for websites, RTMP: used for media streaming

<a name="cloudfront_exam_tips"></a>
**CloudFront-Exam Tips**:
- Edge location is where content will be cached. Edge location are not for READ only, you can write them too.
- Origin is the origin of all the files that the CDN will distribute, this can be an S3 bucket, an EC2 instance, an ELB or
  Route53
- Distribution is the name given to the CDN which consists of a collection of Edge locations
  - web distribution - typically used for websites
  - rtmp- used for media streaming
- objects are cached for the life of ttl(time to live)
- if you clear the cached objects, you will be charged

[Back to Table of Contents](#toc)

<a name ="storage_gateway"></a>  
# Storage Gateway:
- This is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and
  secure integration between the two. 
- The service enables you to securely store data to the AWS cloud for scalable and cost-effective storage.
- Available for download as a VM that you install as a host in your datacenter
- Once installed and associated with your AWS account through the activation process,
  you can use the AWS console to create the storage gateway option that is right for you, i.e. gateway-cached
  or gateway-stored volumes that can be mounted as iSCSI devices by your on-premise applications
- 4 pricing components: gateway usage(per gateway/month), snapshot storage(per GB/month), volume storage usage(per GB/month),
  data transfer out(per GB/month)
- 4 types:
    - **File gateway(NFS)**: store flat files directly on S3, and accessed via NFS. Ownership, permissions,and timestamps
       are durably stored in S3 in the user metadata of the object associated with the file.
       They can be managed as native S3 objects
    - **Volumes gateway(iSCSI)**: uses block based storage, would be able to run a OS
       - **Gateway Stored Volumes/Stored volumes**: store entire size of data sets on sites or on premise, are inexpensive and
         durable backup providers that you can recover locally or from Amazon EC2, low latency access to datasets.
         Data written to your stored volumes is stored on your on-premise hardware. This data is asynchronously backed up to S3
         in EBS snapshots 
       - **Gateway Cached Volumes/Cached volumes**: store only most recently accessed data on your own premise
         and rest is backed off in Amazon. Can create storage volumes upto 32TiB in size.
         Your gateway stores data that you write to these volumes in S3, and retains recently read data in your on-premises 
         storage gateway's cache and upload buffer storage. 1GB - 32TB in size for cached volumes
    - **Gateway Virtual Tape Library/Tape gateway(VTL)**: backup and archiving solution.
         Have a limitless collection of virtual tapes. Each virtual tape can be stored in a  Virtual Tape library backed by 
         Amazon S3 or a Virtual tape shelf backed by Amazon Glacier. 
         The VTL exposes an industry standard iSCSI interface which provides your backup application with online access 
         to the virtual tapes. 
         Each tape gateway is preconfigured with a media changer and tape drives, which are available to your existing client 
         backup applications as iSCSI devices.
         You add tape cartridges as you need to archive your data. Uses popular backup applications like NetBackup, Backup exec
         Veeam etc.

**Storage Gateway Exam Tips**:
- File gateway: for flat files, stored directly on S3
- Volume gateway
    Stored volumes: Entire dataset is stored on site and is asynchronously backed up to S3
    Cached volumes: entire data set is stored on S3 and the most frequently accessed data is cached on site
- Gateway Virtual Tape Library(VTL)
    Used for backup and popular backup applications like Netbackup, Backup Exec

[Back to Table of Contents](#toc)
    
<a name ="snowball"></a>
# Snowball:
- This is a petabyte scale data transport solution that uses secure appliances to transfer large amounts of data
  into and out of AWS. 
- It addresses common challenges with large-scale data transfers such as high network costs, long transfer times,
  and security concerns. 
- Transferring data with snowball is fast, simple, secure and can be as little as 1/5th the cost of high-speed internet. 
- Currently, only available in the US, and only works with S3 both with importing and exporting. 
- 80TB of snowball in all regions, you can get 50TB in the U.S.
- Snowball uses tamper resistant enclosures, 256-bit encryption, and industry-standard Trusted Platform Module(TPM)
  that is designed to ensure both security and full chain-of-custody or your data, as well as reduce management overhead
  involved with transferring data into or out of AWS.
- Once data transfer has been processed and verified, AWS performs a software erasure of the snowball appliance
- **Snowball Edge**:
   - A 100TB data transfer device with on-board storage & compute capabilities
   - used for moving large amounts of data into and out of AWS
   - as a temporary tier for large datasets or to support local workloads in remote/offline areas
   - cluster together to form a local storage tier and process your data on-premises, helping you ensure your application
     continue to run even when they are not able to access the cloud
- **Snowmobile**:     
   - An exabyte-scale data transfer service used to move large amounts of data to AWS
   - can transfer upto 100PB per snowmobile in a 45ft long container
   - makes it easy to move massive volumes of data to the cloud, including libraries, image repositories etc.
   - in this way data is safe, transferred fast, and cost effective
    
**Snowball Exam tips**:
- Understand snowball
- Understand import/export that is what was used before snowball
- Snowball can import to S3, and export from S3

[Back to Table of Contents](#toc)

<a name= "import_export"></a>     
# Import/Export:
- Import/Export Disk:
    - Used before snowball was introduced    
    - Accelerates moving large amount of data into and out of the AWS cloud using portable storage devices for transport.
    - Faster than the internet transfer and more cost effective than upgrading your connectivity
    - Allows to import to EBS, S3, Glacier, export from S3
    - you pay only for what you use. 
    - 3 pricing components: per device fee, a data load time charge, possible return shipping charges,
      or shipping to destinations not local to AWS

<a name ="ec2"></a>
# EC2(Elastic Compute Cloud)

Provides resizable compute capacity in the cloud. 
Reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as computing requirements change.

**EC2 options**:

- On demand: Allow you to pay a fixed rate by the hour with no commitment. 
   User that want low cost and flexibility without any upfront payment or long-term commitment. 
   Apps with spiky, short term, or unpredictable workloads that cannot be interrupted. Apps being developed or tested for the first time
               
- Reserved: 1 or 3 year terms, provide discounts on the hourly charge by providing a capacity reservation
   Apps with steady state or predictable usage. Apps that require reserved capacity. Users able to make upfront payments to reduce their total computing costs even further

- Spot: Enable you to bid whatever price you want for instance capacity, providing for even greater savings if your app has flexible start and end times 
        Apps that are feasible to very low compute prices. Users with urgent computing needs for large amounts of additional capacity
        If the spot instance is terminated by Amazon EC2, you will not be charged for the partial hour of usage, but if you terminate the instance yourself, you will be charged for any hour in which the instance ran

# EC2 Instance Types:

| Family |    Speciality               |  Use Cases
|------- |-----------------------------|----------------------------------------------------------|
| T2     |Lowest Cost, General Purpose | Web Servers/Small DBs                                    | 
| M4     |General Purpose              | Application Servers                                      |              
| M3     |General Purpose              | Application Servers                                      |
| C4     |Compute Optimized            | CPU Intensive Apps/DBs                                   |  
| C3     |Compute Optimized            | CPU Intensive Apps/DBs                                   |
| R3     |Memory Optimized             | Memory Intensive Apps/ DBs                               |
| G2     |Graphics/General Purpose GPU |Video Encoding, Machine Learning, 3D Application Streaming|
| I2     |High Speed Storage           | NoSQL DBs, Data Warehousing etc.                         |
| D2     |Dense storage                |File Servers/Data Warehousing/Hadoop                      |

# How to remember?
D for Density
I for IOPS
R for RAM
T for cheap general purpose(think of T2 Micro)
M - main choice for general purpose apps
C for Compute
G - Graphics

# Elastic Block Storage

Allows you to create storage volumes and attach them to Amazon EC2 instances. 
Once attached, you can create a file system on top of these volumes, run a database, or use them in any other way you would use a block device. 
Amazon EBS volumes are places in specific Availability Zone, where they are automatically replicated to protect you from the failure of a single component.

# EBS Volume Types:

- General Purpose SSD(GP2): 99.999% availability,ratio of 3 IOPS per GB with upto 10,000 IOPS and the ability to burst upto 3,000 IOPS for short periods for volumes < 1GB
- Provisioned IOPS SSD(I01): designed for I/O apps  such as large relational or NoSQL databases. Use if you need > 10,000 IOPS
- Magnetic(Standard): lowest cost per gigabyte of all EBS volume types. Magnetic volumes are ideal for workloads where data is accessed infrequently, and apps where the lowest storage cost is important.
    Termination protection is turned off by default, you must turn it on

On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated
**Root volumes** cannot be encrypted by default, you need a third party tool(bitlocker) to encrypt the root volume
Additional volumes can be encrypted

# Security Groups Lab

- Changes to security rule takes place immediately
- You cannot deny any http rule, you can only allow at any given time
- All inbound traffic is blocked
- All outbound traffic is allowed
- You can have any number of EC2 instances within a security group
- Security groups are STATEFUL -> if you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again

# Volume vs snapshots lab

**Volume**:

- exists on a EBS
- Is a virtual HD

**Snapshot**:

- Exists on S3
- You can take a snapshot of a volume, this will store that volume on S3 that will store the volume in S3
- They are point in time copies of volumes
- Snapshots are incremental, this means that only the blocks that have changed since your last snapshot are moved to S3
- It takes time to create the first snapshot

**Volume vs snapshots - security**:

- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically
- You can share snapshots, but only if they are unencrypted. These snapshots can be shared with other AWS accounts or made public

**Snapshots of Root Device Volumes**:

To create  snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking a snapshot

# RAID, Volumes and Snapshots:

**RAID**:

Redundant Array of Independent Disks

**Types**:

- RAID 0: Striped, No redundancy, good performance
- RAID 1: Mirrored, Redundancy
- RAID 5: good for reads, bad for writes, AWS does not recommend putting RAID 5 ever on EBS
- RAID 10: Striped and Mirrored, Good redundancy, good performance


**How do I take a snapshot of a RAID Array**:

**Problem**: 

Take a snapshot, the snapshot excludes data held in the cache by apps and the OS. This tends not to matter on a single volume, however using multiple volumes in a RAID array, this can be a problem due to interdependencies of the array.

**Solution**:
 
- take an application consistent snapshot
- Stop the app from writing to the disk
- Flush all the caches to the disk

**How can we do this?**
  
 1. Freeze the filesystem
 2. Unmount the RAID array
 3. Shutting down the associated EC2 instance


# Creating an Amazon Machine Image(AMI):

Provides the information required to launch a virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need. 

It consists of the following:

- A template for the root volume of the instance(for example an Operating System, an app server, and apps)
- Launch permissions that control which AWS accounts can use the AMI to launch the instance
- A block device mapping that specifies the volumes to attach to the instance when it’s launched

AMIs are regional, you can only launch an AMI from the region in which it is stored. 
However you can copy AMI’s to other regions using the console,command line or the Amazon EC2 API


# EBS Root volumes vs Instance Store

You can select an AMI from 

- Region
- OS
- Architecture(32-bit or 64-bit)
- Launch permissions
- Storage for the Root Device(Root Device Volume)
  - Instance Store(Ephemeral storage). These cannot be stopped. If the underlying host fails, you will lose your data. We can reboot and not lose data
  - EBS backed volumes. These instances can be stopped. You will not lose the data on this instance if it is stopped. We can reboot and not lose data

By default both ROOT volumes will be deleted on termination, however with EBS volumes, you can tell AWS to keep the root device volume.

- All AMIs are categorized as either backed by Amazon EBS or backed by instance store
- For EBS volumes: The root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot. If you need fast provisioning times we prefer EBS backed volumes.
- For Instance store volumes: The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3. It takes time to provision an instance store volume than a EBS volume

# Load Balancers and Health Checks

- They can be Inservice or out of service
- They provide Health Checks
- Have their own DNS name. You are never given an IP address

# CloudWatch:

- Standard monitoring = 5 minutes
- Detailed monitoring = 1 minute
- Creates awesome dashboards to see what is happening with your AWS environment
- Allows you to set Alarms that notify you when particular thresholds are hit
- Events help you to respond to state changes in your AWS resources
- Logs allow to aggregate, monitor, and store logs

# The AWS Command Line(CLI) and EC2
# Identity Access Management Roles Lab

- Roles are more secure than storing your access key and secret access key on individual EC2 instances
- Roles are easier to manage
- Roles can only be assigned when that EC2 instance is being provisioned
- Roles are universal, you can use them in any region

# Bash Scripting Lab
# Instance Metadata

- Metadata information location: curl http://169.254.169.254/latest/meta-data/

# AutoScaling 101
# Launch Configurations & Auto Scaling Groups

# EC2 Placement Groups

**What is a placement group?**:

- Is a logical grouping of instances within a single Availability zone. 
- Enables apps to participate in a low-latency , 10Gbps network
- Recommended for apps that benefit from low network latency, high network throughput, or both
- Cannot span multiple availability zones
- The name you specify a placement group must be unique within your AWS account
- Only certain types of instances can be launched in a placement group(Compute optimized, GPU, Memory Optimized, Storage Optimized)
- AWS recommends homogenous instances (instances of the same size, and same family)within placement groups
- Cannot merge placement groups
- Cannot move an existing instance into a placement group. You can create an AMI from your existing instance, and then launch a new instance from the AMI into a placement group


# EFS(Elastic File System):

- A file storage service for EC2 instances. A simple interface that allows you to create and quickly configure file systems
- Storage capacity is elastic, growing and shrinking automatically as you add and remove files, so your app has the storage it needs, when they need it
- Supports NFS version v4
- You only pay for the storage you use(no pre-provisioning required)
- Can scale upto petabytes
- Supports thousands of concurrent NFS connections
- Data is stored across multiple AZ’s within a region
- Read After Write consistency
- Is a BLOCK based storage

# Lambda Concepts

A compute service where you can upload your code and create a lambda function
Takes care of provisioning and managing the servers that you use to run the code
We need not worry about OS, patching, scaling etc.

### It can be used in the following ways:
As an event-driven compute service where AWS Lambda runs your code in response to events. These events could change be changes to data in an Amazon S3 bucket or an Amazon DynamoDB table
As a compute service to run your code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDKs.

# What is Lambda?

- Data centres
- Hardware
- Assembly code/Protocols
- High Level Languages
- Operating Systems
- Application Layer/AWS APIs
- AWS Lambda

# What Languages:

- Node.js
- Java
- Python

# How is Lambda priced:

- Number of requests: First 1 million requests are free. $0.20 per 1 million requests thereafter
- Duration: calculated from the time your code begins executing until it returns or otherwise terminates, rounded up to the nearest 100ms. The price depends on the amount of memory you allocate to your function. You are charged $0.00001667 for every GB-second used

# Why Lambda?

- No servers
- Continuously scaling
- Really cheap

# Exam Tips for EC2:

## Know the differences:

- On demand
- Spot
- Reserved
- Remember with spot instances
  - If you terminate the instance, you pay for the hour
  - If AWS terminates the spot instance, you get the hour t was terminated for free

# Exam Tips for EBS:

## EBS consists of:

- General purpose SSD - GP2 - (up to 10,000 IOPS)
- Provisioned IOPS SSD - IO1 - (more than 10,000 IOPS)
- Magnetic- cheap, infrequently accessed storage
- You cannot mount 1 EBS volume to multiple EC2 instances, instead use EFS
- Remember the different EC2 instance types
- Remember the acronyms for remembering the EC2 instance types D(Density).I(IOPS).R(RAM).T(cheap general purpose).M(main choice for general purpose apps).C(compute).G(graphics)
- Termination protection is turned off by default, you must turn it on. On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.
- Root volumes cannot be encrypted by default, you need a third party tool to encrypt the root volume

# Volumes vs Snapshots

- Volumes exist on EBS(Virtual Hard Disk)
- Snapshots exist on S3
- You can take a snapshot of a volume, this will store that volume on S3. These are point in time copies
- Snapshots are incremental, this means that only the blocks that have changed since your last snapshot are moved to S3. It will take time to create a first snapshot
- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically.
- We can share snapshots only if they are encrypted. These can be shared with other AWS accounts or you can make them public
- In order to take a snapshot for Amazon EBS Volumes that serve as root devices, you should stop the instance before taking the snapshot

# EBS vs Instance store:

- Instance store volumes are called Ephemeral storage
- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data
- EBS backed instances can be stopped, you will not lose the data on this instance if it is stopped
- You can reboot both, and you are not going to lose the data
- By default both ROOT volumes will be deleted on termination, however with EBS volumes, you can tell AWS to keep the root device volume

# How can I take a snapshot of a RAID array?

- Problem: take a snapshot, the snapshot excludes the data held in the cache by applications and the OS. This tends not to matter on a single volume, however using multiple volumes in a RAID array, this can be problem due to interdependencies of the array. Solution is to take an application consistent snapshot.

How to do it?

- Stop the application from writing to the disk
- Flush all caches to the disk

   **How can we do this?**
   
  1. Freeze the filesystem
  2. Unmount the RAID array
  3. Shutting down the associated EC2 instance

# Amazon Machine Images:

AMI’s are regional, you can only launch an AMI from the region in which it is stored. 
However you can copy AMI’s to other regions using the console, command line or the Amazon EC2 API

# Cloudwatch:

- Standard monitoring: 5 minutes
- Detailed monitoring = 1min
- CloudWatch is for performance monitoring
- CloudTrail is for auditing
- Create dashboards to see what is happening with your AWS environment.
- Allows you to set alarms that notify you when certain thresholds are hit
- CloudWatch events help you to respond to the state changes in your AWS resources
- CloudWatch Logs help you to aggregate, monitor, and store logs 

# Roles:

- Are more secure than storing your access key and secret access key on individual EC2 instances
- Are easier to manage
- Roles can only be assigned when the EC2 instance is being provisioned
- Are universal, you can use them in any region

# Instance Meta-data:

- Used to get information about an instance(such as public ip)
- Command: curl http://169.254.169.254/latest/meta-data
- No such thing as user data

# Elastic File System:
- Supports NFS version 4 protocol
- You only pay for the storage you use(no pre-provisioning required)
- Can scale up to the petabytes
- Can support thousands of concurrent NFS connections
- Data is stored across multiple AZ’s within a region
- Read After Write consistency

# What is Lambda?
  Please read the definition for `Lambda` above

# Building a Fault-Tolerant website

## Setting up environment:
1. IAM Role for S3Role for S3 Full access
2. VPC will contain 2 security groups one will be a WebDMZ, and the second one will be a RDS one
3. 2 S3 buckets, named `wordpresscode2016aniketacloudguru`, and `wordpressmedia2016aniketacloudguru` and CDN's were configured for both of them
4. 1 CDN for `wordpressmedia2016aniketacloudguru`
5. RDS instance, non-publicly accessible, and non-multiAZ , since I wanted this to be free
6. 1 ELB with the Web-DMZ security group
7. No Route 53 record(optional)
8. set up a EC2 instance, installed wordpress on it, uploaded the code to S3. Link to blog: [WordPress](http://54.187.100.238/index.php/2016/08/27/welcome-to-aws-learnings/)

## Automation and setting up AMI

# Advantages of Cloud
- Trade capital expense for variable expense
- benefit from massive economies of scale
- stop guessing about capacity
- increase speed and agility
- stop spending money running and maintaining data
- go global in minutes

# Overview of Security Processes
- *Shared responsibility model*: AWS is responsible for Global Infrastructure but you are responsible for anything you put on the cloud
- *IAAS*: Amazon EC2, S3, and Amazon VPC are under your control. 
- *Managed services*: AWS is responsible for patching, antivirus etc. But you are responsible for account management and user access. 
- *Storage decommissioning*: When a storage device has reached its end of useful life, Amazon will de-commission the resource to not expose consumer data
- *Network Security*: You can connect to any AWS access point via HTTP using SSL, amazon also offers VPC which provides a private subnet within the AWS cloud
- *Amazon Corporate segregation*: Logically, the AWS production network is segregated from the Amazon Corporate network by means of a complex set of network security/segregation device
- will not permit IPSpoofing must request a vulnerability scans
- *AWS Trusted Advisor*: Inspects your AWS environment and makes recommendations when opportunities may exist to save money, improve system performance, or close security gaps.
- *Instance Isolation*: Different instances running on the same physical machine are isolated from each other via Xen hypervisor, AWS firewall resides between the virtual interface and 
the physical network interface. The instances can be treated as if they are on separate physical hosts, and neighbors have no access to that instance other than any other host
on the internet.
- *Guest OS*: You have full root access over accounts, services, and applications, virtual instances controlled by you, AWS does not have access rights. As also provides 
the ability to encrypt EBS volumes and their snapshots with AES-256
- *Firewall*: Amazon EC2 provides a complete firewall solution; configured to be in a deny-all mode, customers must explicitly open the ports to allow inbound traffic
- *Elastic Load Balancing*: SSL termination supported, allows you to identify the IP addresses of a client connecting to your servers.
- *Direct Connect*: Bypass ISPs in your network path. 

# AWS Risk and Compliance
- AWS has a strategic business plan which includes risk identification and the implementation of controls to mitigate or manage risks
- customers can request permission to conduct scans of their cloud infrastructure as long as they are limited to the customer's instances and do not violate
 the AWS acceptable policy
 
# Architecting for the AWS Cloud: Benefits
- almost zero upfront infrastructure development
- just-in-time infrastructure
- more efficient resource utilization
- usage-based costing
- reduced time to market

## Technical benefits of Cloud
- automation - scriptable infrastructure
- auto-scaling
- proactive scaling
- more efficient development lifecycle
- improved testability
- disaster recovery and business continuity
- overflow traffic to the cloud

- Be a pessimist when designing architectures in the cloud; assume things will fail. In other words, always design, implement and deploy for automated recovery from 
failure

- Decouple your components: build components that do not have tight dependencies on each other, so that one component dies/sleeps/busy then other components in the system
 are built so as to continue to work as if no failure is happening. Loose coupling isolates the various layers and components of your application so that each component
 interacts asynchronously with the others

- Implement elasticity: can be implemented in 3 ways
   1. proactive cyclic scaling: periodic scaling that occurs at fixed interval
   2. proactive even scaling: scaling when you are expecting big surge of traffic requests due to a scheduled business event
   3. Auto-scaling based on demand: using monitoring service, your system can send triggers to take appropriate actions

- secure your application   

# Consolidated Billing
   We have a paying account, and this account is linked to separate AWS accounts such as test/dev, production and bank office accounts respectively.
   Paying account is independent. It cannot access resources of other accounts. All linked accounts are independent. 
   There is a limit of 20 linked accounts for consolidated billing

## Advantages:
- one bill per AWS account
- very easy to track charges and allocate costs
- volume pricing discount

# Resource Groups and Tagging

## Tags
- key value pairs attached to AWS resources
- metadata
- they can be inherited

## Resource Groups
- makes it easy to group your resources using the tags assigned to them. You can group resources that share one or more tags
- they contain information such as: region, name, HealthChecks

# VPC Peering
- a simple connection between 2 VPCs that enables us to route traffic between them using private IPs
