# AWS Associate Solutions Architect Exam Notes
These are the notes I have prepared while doing the online course for AWS Associate Solutions Architect on Udemy(between 2015-2016) by [Ryan Kroonenburg] (https://www.udemy.com/user/ryankroonenburg/).
I use these notes whenever I forget or want to revise any concept of AWS, I strongly suggest anyone wanting to know/study about AWS be sure to check out the courses offered by Ryan on Udemy by navigating to the above link.

### AWS Solutions Architect-Introduction:
- forums: forums.acloud.guru
- Exam blueprint [Example exam blueprint](http://awstrainingandcertification.s3.Amazonaws.com/production/AWS_certified_solutions_architect_associate_blueprint.pdf)

# Important white paper to read:
Overview of Security Processes

# What do I need for this course:
- AWS account Free tier
- Domain name(optional)

# History of AWS:
It all started with **Chris Pinkman** and **Benjamin Black** present a paper on Amazon’s internal infrastructure, and request the CEO to sell it as a service, while preparing a business case

Following are the sequence of events:

    1.  SQS launched in 2004
    2.  AWS launched in 2006
    3.  2007 more than 180k dev moved or started using AWS
    4.  2010 all of Amazon moved to the AWS platform
    5.  2012 first re:invent
    6.  2013 certifications

# Concepts and Components:

   1.   **AWS Global Infrastructure**:
-   Consists of 11 regions
-   Each region consists of multiple availability zones
-   Currently(as of 2015) there are 52 edge locations
-   Regions are described as places like central europe, east US, west US etc.

**Availability zones are data centers**:
Each region will contain at a minimum of 2 availability zones

**Edge locations are CDN endpoints**:
A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other Web content to a user based on the geographic locations of the user, the origin of the webpage and a content delivery server.

-   There are many more edge locations than there are regions
-   Currently 52 edge locations around the world
-   Edge locations are used by CloudFront to cache files near the user where they access them.

   2.	**Networking**:
     
        1.  Route 53: Amazon’s DNS service, basically allows you to host your domain name with Amazon
        
        2.  Direct connect: allows you to connect directly to where your Virtual Private Cloud(VPC) is located.
            Allows you to put dedicated connection links to Amazon data center into your VPC, hence you don't need to go over the internet to access it
            
        3.  Virtual Private Cloud: a virtual data center as a collection of AWS resources, inside of a VPC we have EC2 instances, EBS instances, also Load Balancers

   3.	**Compute Elements**:
   
        1.  EC2: Known as Elastic Cloud Compute, allowing one to provision instances inside your VPC, these can be anything from Linux, CentOs, etc, and we can also provision Windows instances, Amazon also provides a marketplace, wherein you can purchase pre built, or preconfigured instances from 3rd party
        
        2.  Autoscaling: Most famous aspect of AWS cloud. Allows you to provision more Virtual machines to handle load
            Autoscaling happens at a predefined stage we can set alarms to trigger autoscaling, so things like CPU utilization, or perhaps Disk I/O, also autoscaling happens at a predefined timeframe
            
        3.  Elastic Load Balancing:  Acts as Load Balancer to your Web Servers, or your application servers, route53 can be made to point to your load balancer, the load balancer will then distribute your traffic down to your EC2 instances
            ELBs also has a health check mechanism, so it can detect whether an EC2 instance is alive, and if it has died, it will remove it on its own, and users will not notice that you have an outage on a particular instance
            
        4.  Workspaces: Essentially a VDI platform allows you to do virtual desktops, so basically you can run Windows 7/Windows 8 instances in the cloud, and use thin clients to access them

   4.	**Storage**:

        1.  S3(Simple Storage Service): Been around since the conception of AWS, it is a file-based storage or object based storage. Allows us to store files in the cloud of sizes ranging from 1 byte to 5 terabytes
        
        2.  Glacier: Is an archiving service. Allows us to archive all our data in the Amazon cloud, not immediately accessible but take 3-5 hours to restore a file from Glacier, hence used for long-term storage
        
        3.  EBS(Elastic Block Storage): Allows us to have persistent storage in the cloud. It is block-level so it allows us to install different file-systems such as Windows partition or Linux partition stored on the EBS volume. 
            Most commonly used to mount to EC2 instances. Completely flexible we can choose from Magnetic storage, SSD storage etc
            
        4.  Storage gateway: A service that connects on-premise software appliance with cloud based storage to provide seamless and secure integration between organizations on premise IT equipment and AWS storage infrastructure. 
            This service allows us to securely store data in the AWS cloud for scalable and cost-efficient storage. It also supports industry standard protocol that work with existing applications. Effectively AWS storage gateway is used for backups to cloud or S3 or to Glacier
            
        5.  Import/Export: Accelerates moving large amounts of data in and out of the AWS cloud using portable storage devices for transport. 
            It transfers your data onto and off of storage devices using Amazon’s high speed internal networking and bypasses the internet. 
            It is often faster than internet transfers and more cost-effective than upgrading the connectivity

   5.   **Databases**:
   
        1.  RDS(Relational Database Services): Consists of elements such as SQLServer by MS, Oracle, PostgreSQL, MySQL, and Amazon’s own database engine known as Aurora completely MySQL compatible db but designed to run specifically on the AWS platform.
        2.  DynamoDB: For NoSQL 
        3.  Elastic Cache: Allows/offers an in-memory caching service for the AWS platform.

   6.  **Analytics**:
   
        a.  RedShift: A fast, fully-managed petabyte scaled datawarehousing solution that makes it simple and cost-effective to efficiently analyze your data using your existing BI tools. 
            It is designed from the infrastructure layer upwards to maximize performance and minimize cost.
        
        b.  Kinesis: Is a fully-managed service for real-time processing of streaming data at massive scale. 
            Can continuously change and store terabytes of data per hour from several sources such as website clickstreams, social media, location tracking event. 
            With Kinesis client library ACL, we can build Amazon Kinesis apps, and use streaming data to power real time dashboards, generate alerts, implement dynamic pricing and advertising and more. 
            We can emit data from Kinesis to other AWs services such as S3, redShift, Elastic MapReduce, and lambda.
            
        c.  ElasticMapReduce(EMR): A web service that makes it easy to quickly and cost-effectively process vast amounts of data. 
            Uses Hadoop, an open source framework to distribute your data and process across a resizeable cluster of Amazon EC2 instances. 
            It can also run other distributed framework such as Spark and Presto. 
            EMR is used in a variety of applications including log analysis, web-indexing, data warehousing, machine learning, financial analysis, scientific simulation, and Bioinformatics, customers launch millions of Amazon’s EMR clusters each year.

   7.   **Application Services**:
   
        1.  SQS(Simple Queue Service): A fast reliable, scalable and fully-managed messaging queueing service. 
            SQS makes it simple and cost-effective to decouple the components of a cloud application. 
            We can use SQS to transmit any volume of data at any level of throughput, without losing messages or other services to be available
        
        2.  SWF(Simple Work Flow Service): Helps developers to build, run, and scale background jobs that have parallel or sequential steps. 
            We can think of this as a fully-managed state-tracker and task coordinator in the cloud. Tasks can be carried out by application or human workers
        
        3.  SNS(Simple Notification Service): A fast, flexible, fully-managed push messaging service, makes it simple and cost-effective to push notifications to all mobile devices including Apple, Google, FireOS, and Windows devices, and Android devices as well. 
            We can use SNS push notifications for end-end smart connected devices or distributed systems. Besides pushing a cloud notification directly to mobile devices it can deliver messages by SMS or email to SQS queue or any Http endpoint. To prevent messages being lost all messages are published to SNS are stored redundantly across multiple availability zones
        
        4.  SES(Simple Email Service): A cost-effective outbound only email sending service. 
            We can send transactional emails,marketing messages etc, and get to pay for what we use. 
            Along with high-deliverability SES provides, easy, real-time access to your sending statistic, and built-in notifications for bounces, complaints, and deliveries to help you find tune your cloud-based email sending strategy
        
        5.  Elastic Transcoder: A media transcoding service in the cloud.Designed to be highly-scalable, easy to use in a cost-effective way for developers and businesses to convert or transcode media files from their source formats to version that will play on devices like smartphones, tablets etc. 
            Netflix, and Amazon Prime make heavy use of Elastic Transcoding service
        
        6.  Cloud Search: A managed service in the AWS cloud that makes it simple and cost-effective to setup,manage,and scale a custom search solution for website/app
  
   8.	**Deployment and Management**:
    
    __Opsworks__: An app management service that makes it easy to deploy and operate applications of all shapes and sizes 
    We can define the application’s architecture and specification around each component including package installation, s/w configuration resources, such as storage. 
    Start from templates for common technologies like app service and databases, or build your own to perform any task that can be scripted. 
    Includes automation to scale your application,based on time or load and dynamic configuration to orchestrate changes as your environment scales.
    
        1.  IAM(Identity Access Management): 
            Enables you to securely control access to AWS services and resources for your users
            We can create and manage AWS users and groups and use permissions to allow and deny their access to AWS resources
        
        2.  CloudWatch:
            A monitoring service for AWS Cloud resources and the apps you run on AWS
            Used for collecting and tracking metrics, collect and monitor log files, and set alarms
            It can monitor AWS resources,such as EC2 instances, DynamoDB tables,and RDS DB instances, as well as custom metrics generated by your apps and services, and log any files your app generates
            We can use it to gain system-wide visibility into resource utilization, app performance, and operational health
            
        3.  Elastic Beanstalk: An easy to use service for developing and scaling web apps developed in Java, Dot Net, PHP, Node.js, Python, Ruby, and Docker on familiar servers such as Apache, EngineX, passenger, and IIS
            We can simply upload the code and EB will automatically handle the deployment from capacity provisioning,load balancing, autoscaling, app health and monitoring 
            At the same we retain full control over the AWS resources powering your application, and can access the underlying resources at any time
            
        4.  CloudTrail: A logging, and auditing service, a web service that records API call for your account and deliver log files to you 
            We can get history of AWS API calls for your account, including calls made by AWS management console, SDKs, Command line tools, and high level AWS services such as AWS cloud formation
            The history of API calls created by CloudTrail enables security analysis, resource change tracking, and compliance auditing
            
        5.  Data Pipeline: A web service that helps to reliably process and move data between different AWS compute and storage services as well as on premise data sources at a specified interval 
            We can regularly access data,whether where it’s stored, transformed, and processed at it’s scale and efficiently transfer the results to AWS services such as Amazon S3, RDS, DynamoDB, EMR
            
        6.  Cloud Formation: Gives developers, and sys admins an easy way to create and manage a collection of related AWS resources, provisioning and updating them in an orderly and predictable fashion 
            We can use AWS Cloud Formation sample templates or create our own templates to describe the AWS resources and any associated dependencies, or runtime params our app requires to run
            We don’t need to figure out the order for provisioning AWS services or details of those making the dependencies work cloud formation takes care of that
    
    After AWS resources are deployed we can update or modify in a controlled manner and predictable way in effect applying version control to your AWS infrastructure.


#  IAM(Identity and Access Management)
Allows us to manage users and their level of access to the AWS console.

**Features of IAM**:

-  Centralized control of your AWS account
-  Integrated with existing active directory account and allows single sign on
-  Has fine grained access to the AWS resource
-  Access available on user/group/roles
-  Allows Multifactor authentication
-  Provides temporary access for users,and devices and services where necessary
-  Allows us to set up password rotation policy

**High Level Concept**:

- User:     An end user
- Group:    A collection of users under one set of permissions
- Roles:    Similar to a group, but you can assign both users and AWS resources(EC2).EC2 instances have credentials stored on them,however it is a security risk and difficult to manage.Roles solve this issue.For example, an EC2 instance can have a S3 role assigned to it,and the S3 role would allow any person or any object that is assigned to it to access S3.

**Each Role has a policy template**.

- Administrator Access: Full access to AWS services and resources
- Power User Access:    Full access except for management of users and groups
- Read Only Access:     Read only access to the resources

More granular access depending on the resources required such as S3 access.

**Configure IAM**:

-  Multifactor authentication: Is simply where you have a second means to verify yourself when signing in. Since passwords can be compromised, with multi factor authentication is basically a second way of authenticating you.

**Creating a role**: 
To allow our EC2 instances to access our S3 resources.

-  Role Name: S3_Access
-  Roles selected: Amazon Ec2: Allows EC2 instances to call AWS services on your behalf.
-  Given a full S3_Access role.
-  Role ARN arn:aws:iam::535754833757:role/S3_Access

**Trusted Entities**: The identity provider(s) ec2.amazonaws.com

-   Policies arn:aws:iam::aws:policy/AmazonS3FullAccess
-   ARN:Amazon Resource Name- unique name within the amazon to describe that role.


# Active Directory Integration:
### How is it done?
Imagine a user is at home, and he wants to login to the AWS console, and they are working on their own home network
So they haven’t already signed-in into the work network.

What they(users) would do is to browse to a URL, for eg: /ADFS/LS/IDPInitiatedSignOn, and this is basically an ADFS server that sits inside a DMZ inside someone’s corporate network. 
You browse to that link and it would give you a user name and password depending on your browser, but basically it prompts you to sign in using your active directory credentials. 
It is also known as Single-Sign On or SSO
 
-   We type our SSO in there and sign into active directory environment. When we perform this step we receive a SAML assertion.
-   SAML basically stands for **Security Assertion Mark-Up Language**. SAML assertions is in the form of an authentication response from the ADFS. 
-   We receive a cookie that is stored inside our browser that says that you are signed on.
-   Our browser then points to the SAML assertion to the AWS sign on endpoint for SAML. 
-   Behind the scenes the sign-in users assume the role with SAML API to request temporary security credentials and then constructs a sign-in URL for the AWS management console. 
-   This will login to the AWS Web console. 

**Questions**:
Can you authenticate with Active Directory: Yes, using SAML authentication
Whether or not you are authenticating to active directory first and then given a security credential or if you get the temporary security credential first, which is then authenticated against the active directory? you always authenticate against active directory first and then you would be assigned the temporary security credential

### IAM Summary:
-   IAM is the management console for managing access to AWS resources for an org
-   IAM consists of users, groups, and roles
-   A user is an individual, groups are collection of users with one set of permissions, roles can be applied to both users and AWS services (such as Lambda,EC2 etc)