# AWSAssociateSolutionsArchitectNotes
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
   Consists of 3 different components, namely
     
        a.  route 53: Amazon’s DNS service, basically allows you to host your domain name with Amazon
        b.  Direct connect: allows you to connect directly to where your Virtual Private Cloud(VPC) is located. Allows you to put dedicated connection links to Amazon data center into your VPC, hence you don't need to go over the internet to access it
        c.  Virtual Private Cloud: a virtual data center as a collection of AWS resources, inside of a VPC we have EC2 instances, EBS instances, also Load Balancers

   3.	**Compute Elements**:
   Consists of 4 key services

        a.  EC2: Known as Elastic Cloud Compute, allowing one to provision instances inside your VPC, these can be anything from Linux, CentOs, etc, and we can also provision Windows instances, Amazon also provides a marketplace, wherein you can purchase pre built, or preconfigured instances from 3rd party.
        b.  Autoscaling: Most famous aspect of AWS cloud. Allows you to provision more Virtual machines to handle load. Autoscaling happens at a predefined stage we can set alarms to trigger autoscaling, so things like CPU utilization, or perhaps Disk I/O, also autoscaling happens at a predefined timeframe.
        c.  Elastic Load Balancing:  Acts as Load Balancer to your Web Servers, or your application servers, route53 can be made to point to your load balancer, the load balancer will then distribute your traffic down to your EC2 instances. ELBs also has a health check mechanism, so it can detect whether an EC2 instance is alive, and if it has died, it will remove it on its own, and users will not notice that you have an outage on a particular instance
        d.  Workspaces: Essentially a VDI platform allows you to do virtual desktops, so basically you can run Windows 7/Windows 8 instances in the cloud, and use thin clients to access them.

   4.	**Storage**:
    Consists of 5 elements

        a.  S3(Simple Storage Service): Been around since the conception of AWS, it is a file-based storage or object based storage. Allows us to store files in the cloud of sizes ranging from 1 byte to 5 terabytes
        b.  Glacier: Is an archiving service. Allows us to archive all our data in the Amazon cloud, not immediately accessible but take 3-5 hours to restore a file from Glacier, hence used for long-term storage
        c.  EBS(Elastic Block Storage): Allows us to have persistent storage in the cloud. It is block-level so it allows us to install different file-systems such as Windows partition or Linux partition stored on the EBS volume. Most commonly used to mount to EC2 instances. Completely flexible we can choose from Magnetic storage, SSD storage etc
        d.  Storage gateway: A service that connects on-premise software appliance with cloud based storage to provide seamless and secure integration between organizations on premise IT equipment and AWS storage infrastructure. This service allows us to securely store data in the AWS cloud for scalable and cost-efficient storage. It also supports industry standard protocol that work with existing applications. Effectively AWS storage gateway is used for backups to cloud or S3 or to Glacier
        e.  Import/Export: Accelerates moving large amounts of data in and out of the AWS cloud using portable storage devices for transport. It transfers your data onto and off of storage devices using Amazon’s high speed internal networking and bypasses the internet. It is often faster than internet transfers and more cost-effective than upgrading the connectivity

   5.   **Databases**:
   
        a.  RDS(Relational Database Services): Consists of elements such as SQLServer by MS, Oracle, PostgreSQL, MySQL, and Amazon’s own database engine known as Aurora completely MySQL compatible db but designed to run specifically on the AWS platform.
        b.  DynamoDB: For NoSQL 
        c.  Elastic Cache: Allows/offers an in-memory caching service for the AWS platform.

   6.  **Analytics**:
   
        a.  RedShift: A fast, fully-managed petabyte scaled datawarehousing solution that makes it simple and cost-effective to efficiently analyze your data using your existing BI tools. It is designed from the infrastructure layer upwards to maximize performance and minimize cost.
        b.  Kinesis: Is a fully-managed service for real-time processing of streaming data at massive scale. Can continuously change and store  terabytes of data per hour from several sources such as website clickstreams, social media, location tracking event. With Kinesis client library ACL, we can build Amazon Kinesis apps, and use streaming data to power real time dashboards, generate alerts, implement dynamic pricing and advertising and more. We can emit data from Kinesis to other AWs services such as S3, redShift, Elastic MapReduce, and lambda.
        c.  ElasticMapReduce(EMR): A web service that makes it easy to quickly and cost-effectively process vast amounts of data. Uses Hadoop, an open source framework to distribute your data and process across a resizeable cluster of Amazon EC2 instances. It can also run other distributed framework such as Spark and Presto. EMR is used in a variety of applications including log analysis, web-indexing, data warehousing, machine learning, financial analysis, scientific simulation, and Bioinformatics, customers launch millions of Amazon’s EMR clusters each year.

   7.   **Application Services**:
   
        a.  SQS(Simple Queue Service): a fast reliable, scalable and fully-managed messaging queueing service. SQS makes it simple and cost-effective to decouple the components of a cloud application. We can use SQS to transmit any volume of data at any level of throughput, without losing messages or other services to be available
        
        b.  SWF(Simple Work Flow Service): Helps developers to build, run, and scale background jobs that have parallel or sequential steps. We can think of this as a fully-managed state-tracker and task coordinator in the cloud. Tasks can be carried out by application or human workers
        
        c.  SNS(Simple Notification Service): A fast, flexible, fully-managed push messaging service, makes it simple and cost-effective to push notifications to all mobile devices including Apple, Google, FireOS, and Windows devices, and Android devices as well. We can use SNS push notifications for end-end smart connected devices or distributed systems. Besides pushing a cloud notification directly to mobile devices it can deliver messages by SMS or email to SQS queue or any Http endpoint. To prevent messages being lost all messages are published to SNS are stored redundantly across multiple availability zones
        
        d.  SES(Simple Email Service): a cost-effective outbound only email sending service.We can send transactional emails,marketing messages etc. and get to pay for what we use.Along with high-deliverability SES provides,easy,real-time access to your sending statistic,and built-in notifications for bounces,complaints,and deliveries to help you find tune your cloud-based email sending strategy
        
        e.  Elastic Transcoder: a media transcoding service in the cloud.Designed to be highly-scalable,easy to use in a cost-effective way for developers and businesses to convert or transcode media files from their source formats to version that will play on devices like smartphones,tablets etc.Netflix,and Amazon Prime make heavy use of Elastic Transcoding service
        
        f.  Cloud Search: A managed service in the AWS cloud that makes it simple and cost-effective to setup,manage,and scale a custom search solution for website/app
  
   8.	**Deployment and Management**:
    
    __Opsworks__: An app management service that makes it easy to deploy and operate applications of all shapes and sizes 
    We can define the application’s architecture and specification around each component including package installation, s/w configuration resources, such as storage. 
    Start from templates for common technologies like app service and databases, or build your own to perform any task that can be scripted. 
    Includes automation to scale your application,based on time or load and dynamic configuration to orchestrate changes as your environment scales.
    
        a.  IAM(Identity Access Management): Enables you to securely control access to AWS services and resources for your users. We can create and manage AWS users and groups and use permissions to allow and deny their access to AWS resources.
        b.  CloudWatch: A monitoring service for AWS Cloud resources and the apps you run on AWS. Used for collecting and tracking metrics, collect and monitor log files, and set alarms. It can monitor AWS resources,such as EC2 instances, DynamoDB tables,and RDS DB instances, as well as custom metrics generated by your apps and services, and log any files your app generates. We can use it to gain system-wide visibility into resource utilization, app performance, and operational health
        c.  Elastic Beanstalk: An easy to use service for developing and scaling web apps developed in Java, Dot Net, PHP, Node.js, Python, Ruby,and Docker on familiar servers such as Apache, EngineX, passenger, and IIS. We can simply upload the code and EB will automatically handle the deployment from capacity provisioning,load balancing,autoscaling,app health and monitoring. At the same we retain full control over the AWS resources powering your application, and can access the underlying resources at any time.
        d.  CloudTrail: A logging,and auditing service,a web service that records API call for your account and deliver log files to you.We can get history of AWS API calls for your account,including calls made by AWS management console,SDKs,Command line tools,and high level AWS services such as AWS cloud formation. The history of API calls created by CloudTrail enables security analysis, resource change tracking, and compliance auditing
        e.  Data Pipeline: A web service that helps to reliably process and move data between different AWS compute and storage services as well as on premise data sources at a specified interval.We can regularly access data,whether where it’s stored, transformed, and processed at it’s scale and efficiently transfer the results to AWS services such as Amazon S3, RDS, DynamoDB, EMR
        f.  Cloud Formation: Gives developers, and sys admins an easy way to create and manage a collection of related AWS resources, provisioning and updating them in an orderly and predictable fashion.We can use AWS Cloud Formation sample templates or create our own templates to describe the AWS resources and any associated dependencies,or runtime params our app requires to run.We don’t need to figure out the order for provisioning AWS services or details of those making the dependencies work cloud formation takes care of that. 
    
    After AWS resources are deployed we can update or modify in a controlled manner and predictable way in effect applying version control to your AWS infrastructure.

# Quiz1
    1.  Which section describes best the availability zones: distinct locations from within an AWS region that are engineered to be isolated from failures.
    2.  what does a AWS region consists of? an independent collection of AWS computing resources in a defined geography
    3.  AWS NoSQL product offering is known as dynamodb (Please Use One Word).
    3.  In what year did Amazon move Amazon.com to AWS? 2010
    4.  What is the difference between Elastic Beanstalk & CloudFormation? Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring based on the code you upload to it, whereas CloudFormation is an automated provisioning engine designed to deploy entire cloud environments via a JSON script.
    5.  What new compute service was recently announced at the AWS Re-Invent summit in 2014? Lambda
    6.  Amazon's highly scalable DNS service is known as: Route53

