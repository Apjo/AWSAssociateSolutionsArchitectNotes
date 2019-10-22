# AWS Associate Solutions Architect Notes

Notes prepared while doing the online course on AWS Associate Solutions Architect.
 
These notes are a mixture of notes from a course taught by [Ryan Kroonenburg](https://www.udemy.com/user/ryankroonenburg/),
and one taught by [Eissa](https://www.udemy.com/aws-certified-solutions-architect-associate-exam/) 

### AWS Solutions Architect-Introduction:
- [Example exam blueprint](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS%20Certified%20Solutions%20Architect%20-%20Associate%20Exam%20Guide_v1.1_2019_08_27_FINAL.pdf)
- [March 2020 Updated version](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS%20Certified%20Solutions%20Architect%20-%20Associate%20Exam%20Guide_v1.1_2019_08_27_FINAL.pdf)

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
* [Elastic Cloud Compute EC2](#ec2)
    * [EC2 instance types](#ec2_instance_types)
    * [EC2 Exam Tips](#ec2_exam_tips)
    * [Elastic Block Storage EBS](#ebs)  
        * [EBS volume types](#ebs_volume_types)
        * [EBS volumes vs Snapshots Lab](#volume_vs_snapshot_lab)
        * [EBS Volumes and snapshots security](#volumes_snapshots_security)
        * [EBS vs Instance Store Exam Tips](#ebs_instance_exam_tips)
    * [Security group basics](#security_grp_basics)
    * [RAID](#raid)      
        * [How do I take a snapshot of a RAID Array](#raid_snapshot)
        * [Encrypted Root device volume & Snapshots lab](#encrypted_root_vol_snapshot_lab)
        * [Creating an ami](#ami_create)
        * [AMI Types](#ami_types)
    * [Load Balancer and HealthCheck Labs](#loadbalancer_healthcheck_lab)
    * [CloudWatch EC2](#cloudwatch)
    * [IAM Roles with EC2](#iam_with_ec2)
    * [EC2 Instance Metadata](#ec2-meta-data)
    * [Autoscaling](#autoscaling)
    * [EC2 Placement groups](#ec2_placement_groups)
    * [Elastic File System](#efs)
    * [AWS Lambda](#aws_lambda)
        * [AWS Lambda Exam Tips](#aws_lambda_exam_tips)
* [DNS](#dns)
    * [Route53 Routing policies](#route53_routing_policies)  
    * [DNS Exam Tips](#dns_exam_tips)  
* [Databses 101](#databases)
    * [RDS](#rds)
    * [RDS Backup](#rds_backups_multiaz)
    * [DynamoDB](#dynamodb)
    * [Redshift](#redshift)
    * [Elasticache](#elasticache)
    * [Aurora](#aurora)
* [Virtual Private Cloud](#vpc)
    * [VPC Components](#vpc_compo)
    * [IP V6](#ip_v6)
    * [NAT](#nat_instances)
        * [NAT Gateway](#nat_gateway)
        * [Network Access Control Lists and Security Groups](#nacl_sg)
        * [Application Load Balancers](#alb)
        * [VPC Flow Logs](#vpc-flow-logs)
        * [NAT vs Bastion](#nat-vs-bastion)
* [Application Services](#application-services)
    * [Simple Queue Service(SQS)](#sqs)
    * [Simple Workflow Service(SWF)](#swf)
    * [Simple Notification Service(SNS)](#sns)
    * [Elastic Transcoder](#elastic_transcoder_svc)
    * [API Gateway](#api_gateway)
    * [Kinesis](#kinesis)
* [Overview of Security Processes](#overview_security_process)
* [Addtional Exam Tips](#exam_tips)
    * [Consolidated Billing](#consolidated_billing)
    * [Cross Account Access](#cross_account_access)   
    * [Tagging](#tags)
    * [Resource Groups](#resource_groups)
    * [VPC Peering](#vpc_peering)
    * [Direct Connect](#direct_connect)
    * [Security Token Service](#sts)
    * [Workspaces](#workspaces)
    * [Elastic Container Service](#ecs)
* [Other Helpful Resources- A must read!!](#helpful)

<a name ="concepts_introduction"></a>
# Concepts and Components:

   1.   **AWS Global Infrastructure**:
        1. Availability zone: Each AWS region consists of multiple AZs
            Each region consists of multiple availability zones, currently 69 in total(as of 2019)
            An Availability Zone(AZ) is simply a data center
            Each AZ can contain multiple data centers
                        
        2. Regions: A place where AWS resources exists a geographical area, there are 22 regions (as of 2019)
        
        3. Edge location: This is a CDN(Content-Delivery Network) endpoint. Edge locations are used by CloudFront 
            to cache files near the user where they access them.
        
        4. CDN: A content delivery network (CDN) is a system of distributed servers that deliver webpages,
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
            
        2. Kinesis: 
            - Is a fully-managed service for real-time processing of streaming data at massive scale. 
            - Can continuously change and store terabytes of data per hour from several sources such as
                website clickstreams, social media, location tracking event. 
            - With Kinesis client library ACL, we can build Amazon Kinesis apps,
                and use streaming data to power real time dashboards, generate alerts, implement dynamic pricing and
                advertising or more
            - We can emit data from Kinesis to other AWS services such as S3, redShift, Elastic MapReduce, and lambda
            
        3. ElasticMapReduce(EMR): 
            - A web service that makes it easy to quickly and cost-effectively process vast amounts of data. 
            - Uses Hadoop, an open source framework to distribute your data and process across a resizeable cluster of 
                Amazon EC2 instances.
            - It can also run other distributed framework such as Spark and Presto. 
            - EMR is used in a variety of applications including log analysis, web-indexing, data warehousing, 
                machine learning, financial analysis, scientific simulation, and Bioinformatics, 
                customers launch millions of Amazon’s EMR clusters each year
            - Allows you root access(i.e. login via SSH)
            
        4. Cloud Search / Elastic Search: 
            - Search engine for your website or your application, 
            - Cloud search is fully managed service provided by AWS, Elastic search uses open source framework
            
        5. Data Pipeline: Allows to move data from one place to another
        
        6. Quick Sight: used for creating visualizations, dashboards for BI/Analytics
             
   8.   **Security and Identity**:
   
        1. IAM(Identity Access Management): 
            - Enables you to securely control access to AWS services and resources for your users
            - We can create and manage AWS users and groups and use permissions to allow and
                deny their access to AWS resources
            
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
        
        6. Elastic Transcoder: 
            - A media transcoding service in the cloud. 
            - Designed to be highly-scalable, easy to use in a cost-effective way for developers and businesses to
                convert or transcode media files from their source formats to version that will play on devices like
                smartphones, tablets etc.
    
   10.	**Deployment and Management or Monitoring & Logging**:

        1. CloudWatch: 
            - A monitoring service for AWS Cloud resources and the apps you run on AWS
            - Used for collecting and tracking metrics, collect and monitor log files, and set alarms
            - It can monitor AWS resources, such as EC2 instances, DynamoDB tables, and RDS DB instances,
                as well as custom metrics generated by your apps and services, and log any files your app generates 
            - We can use it to gain system-wide visibility into resource utilization, app performance,
                and operational health.
            
        2. CloudTrail: 
            - A logging, and auditing service, a web service that records API call for your account 
                and deliver log files to you.
            - We can get history of AWS API calls for your account, including calls made by AWS management console,
                SDKs, Command line tools, and high level AWS services such as AWS cloud formation
            
        3. Cloud Formation: 
            - Gives developers, and sys admins an easy way to create and manage a collection of related AWS resources,
                provisioning and updating them in an orderly and predictable fashion.
            
        4. OpsWorks: Automating deployments using chef.
        
        5. Config Manager: proactively monitor changes to your environment.
        
        6. Service Catalog: 
            - Allows you as an enterprise to build out what it is that you authorize within your organization.
        
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
        1. SNS(Simple Notification Service): 
            - A fast, flexible, fully-managed push messaging service, makes it simple and cost-effective to push
                notifications to all mobile devices including Apple, Google, FireOS, and Windows devices,
                and Android devices as well  
        2. SQS(Simple Queue Service): 
            - A fast reliable, scalable and fully-managed messaging queueing service. 
            - SQS makes it simple and cost-effective to decouple the components of a cloud application. 
            - We can use SQS to transmit any volume of data at any level of throughput, without losing messages or 
                other services to be available.
        3. SES(Simple Email Service): 
            - A cost-effective outbound only email sending service. 
            - We can send transactional emails,marketing messages etc, and get to pay for what we use. 
            - Along with high-deliverability SES provides, easy, real-time access to your sending statistics, 
                and built-in notifications for bounces, complaints, and deliveries to help you find tune your 
                cloud-based email sending strategy
   
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

**IAM Elements**:
- Principal: who is going to do the action, admin IAM is your first principal
- Request: eg: create user, create EC2 instance, start or stop an EC2 instance
- Authentication 
- Authorization
- Actions
- Resources: entity that exists within a service

**High Level Concept**:
- Access IAM via AWS Console or through SDKs, HTTPS API, and CLI(require Access Key and Secret)
- User: An end user
- Group: A collection of users under one set of permissions, makes it easier to manage permissions for users. 300 groups
    can be created at any given time, nesting of groups is not allowed. A user can be a member of upto 10 groups
- Roles: Similar to a group, but you can assign both users and AWS resources(EC2). No password or access key is assigned
    It is an identity with permission policies that determine what the identity can and cannot do in AWS. An IAM user
    can assume a role to temporarily take on different permissions. An IAM Role can be assigned to a Federated user who
    signs by using an external identity
- Policies: document defining 1 or more permissions

**Each Role has a policy template**.
- Administrator Access: Full access to AWS services and resources
- Power User Access:    Full access except for management of users and groups
- Read Only Access:     Read only access to the resources

More granular access depending on the resources required such as S3 access.

**Configure IAM**:
- root account gives you unlimited access to do things in the cloud
- AWS provides a number of authentication mechanisms including a console, account Ids and secret keys,
    X.509 certificates, and MFA devices
- Console authentication is the most appropriate for administrative or manual activities
- Account IDs and secret keys for accessing REST-based interfaces or tools
- X.509 certificates for SOAP-based interfaces and tools
- Multifactor authentication: Is simply where you have a second means to verify yourself when signing in.
Since passwords can be compromised, with multi factor authentication is basically a second way of authenticating you.

**Creating a role**: 
A secure way to grant permissions to entities that you trust
Eg:
- IAM users in another account
- Application code running on EC2 instances needs access to other AWS services

**Identity Federation**:
- If your account users already have a way to be authenticated, such as through your corporate network
    - you can federate those user identities in AWS
    - A user logged in to the corporate network using their corporate identity 
        - corporate can replace their existing identity with a temporary identity in your AWS account
        - this user can work in the AWS console
        - similarly the application the user is working on can make programmatic requests using permissions that you
          define
- When to use identity federation
    1. Your users already have identities in a corporate directory
        - If your corporate directory is SAML 2.0 compatible, you can configure your corporate directory to provide
            Single-Sign on(SSO) to access teh AWS management console
        - If your corporate directory is not compatible with SAML 2.0, you can create an identity broker application, to
            provide SSO access to the AWS management console
        - If your corporate directory is Microsoft Active directory, you can use AWS directory service to establish
            trust between your corporate directory and AWS account
    2. Your users already have internet identities
        - If your mobile app or web-based app can let users identify themselves through an identity provider like
            Amazon, Facebook, or Google, or any **OpenID Connect(OIDC)** compatible identity provider, the app can use
            **web federation** to access AWS
        - AWS recommends using AWS Cognito                        

**IAM users and Single Sign-on(SSO)**:
- IAM users in your account have access only to the AWS resources that you specify in the policy that is attached to the
    user or to an IAM group that the user belongs to, for working in the console users must have permissions to perform
    the actions that the console performs, such as listing and creating AWS resources

**IAM-Access Management**:
- Helps you to define what a user or other entity is allowed to do in account, called as authorization
- Permissions are granted through policies that are created and then attached to users, groups, or roles
- By default a user cannot access anything
- Users or groups can have multiple policies attached to them that grant different permissions
- You can assign a role to a federated user
- _Resource based policy_:
    - You can assign a policy to a resource(eg: S3) in addition to attaching to a user or group, this is called as
    resource-based policy, you specify what actions are permitted and hat resource is affected
    - include the principal who is granted the permission

**IAM Users**:
- When you first create an AWS account, you first create an account(root user) which you use to sign in to AWS
- You have complete unrestricted access to all the resources in your AWS account
- Not possible to restrict the permissions that are granted to the AWS account
- Create an IAM user for yourself and then assign yourself admin permissions for your account
- IAM user with admin permissions is not the same thing as the AWS account root user
- An IAM user is an entity that you create in AWS
- IAM users are global entities, no region is required to be specified when you define user permissions
- Each IAM user is associated with one and only one AWS account
- A brand new IAM user has no permissions to do anything
- You can grant user permissions by attaching IAM policies to them directly, or making them members of IAM groups
- IAM user for a service that needs credentials to make requests to AWS is known as "service account"
- You can have **5000** users, for more users make use of STS
- When you create a user, you can identify them by either their names or ARN(arn:aws:iam::account-id-without-hyphens:user/Bob)
- Create credentials or the user, depending on the type of access the user requires, i.e. programmatic or management console
- When you create access key, IAM returns the access key ID and secret access key
- You can give permissions to users to list, rotate and manage their own keys using an IAM policy

**IAM Roles**:
- a set of permissions that grants access to actions and resources in AWS
- does not have a long term credentials associated with it
- roles can be assumed by any one of the following:
    - IAM user in the same account
    - IAM user in a different account
    - web service offered by AWS such as EC2
    - federated user
- **_Resource based policies_**
    - specifies who can access the resource
    - cross-account access with a resource-based policy has an advantage over a role, i.e. a user continues to have
        access in the trusted account, and does not need to give their permissions in place of the role
    - not all services support resource-based policies
- **_IAM Service Roles_**
    - A role that service assumes to perform actions on your behalf
    - Must define a role for the service to assume
    - Vary from service to service, but many allow you to choose your permissions
    - Create, modify, and delete a service role from within IAM
- **_IAM Role for EC2 instance_**
    - when you launch an EC2 instance you can specify a role as a launch parameter
    - IAM automatically provides temporary security credentials that are attached to the role, and then makes them
        available for the EC2 instance to use on behalf of its applications
    - the temporary security credentials are available on the instance and are rotated 5 minutes before the expiration
    - for cases other than EC2 roles you need to request temporary credentials first
    - Instance profile is required to assign an AWS role and its associated permissions to an EC2 instance, it contains
        the role and can provide temporary credentials to an app that runs on the instance
    - **only 1 role can be assigned to an EC2 instance**, and all the app on that instance share the same role and 
        permissions
    - ** Although a role is usually assigned to an EC2 instance when you launch it, a role can also be attached to an
        EC2 instance that is already running**         
- **_IAM Role Delegation_**
    - is granting of permission to someone to allow access to resources that you control
    - this involves setting up trust between the account that owns the resource(trusting account), and the account that
        contains the users that need to access the resource(the trusted account)
    - the accounts can be either be the same account, 2 accounts under the same org, 2 accounts owned by different orgs   
    - to delegate  permission to access a resource, you can create an IAM role that has 2 policies attached
        - **_Permission policy_** 
            - Where the actions and resources the role can use are defined
            - It grants the user of the role the needed permissions to carry out the intended tasks on the resource
        - **_Trust policy_** 
            - Specifies which trusted accounts are allowed to grant its users permissions to assume the role,
            - The trusted entity is included in the policy as principal element in the document
            - You cannot specify a wildcard(*) as a principal
            - The trust policy on the role in the trusting account is 1 half of the permissions, the other half is a
                permissions policy attached to the user in the trusted account that allows the user to switch to, or
                assume the role           
- **_IAM Role for Cross-Account Access_**
    - To grant users access to resources from 1 account to another do not share credentials, access keys, instead use
        IAM roles
    - You can define a role in trusting account, that specifies what permissions the IAM users in the other accounts are
        allowed
    - In some web services you can attach a policy directly to a resource called as resource-based policies
    - A user in 1 account can switch to a role in the same or different account
        - While using the role the user can perform only the actions and access only the resources permitted by the
            role; their original user permissions are suspended
        - When the user exists the role, the original user permissions are restored
        - Services that support resource-based policies are S3, SNS, SQS, Glacier vaults      
    - When to use IAM users vs IAM Roles
        - Use IAM user when:
            - You created an AWS account and you are the only person who works in your account
            - Other people in your group need to work in your AWS account, and your group is using no other identity
                mechanism
            - You want to use the AWS CLI
        - Use IAM Role when:
            - You are creating an app that runs on EC2 instances and that app makes requests to AWS
            - You are creating an app that runs on a mobile phone and that makes requests to AWS
            - Users in your company are authenticated in your corporate network and want to be able to use AWS without
                having to sign in again      
                       
- **_Logging sign-in details in CloudTrail_**
    - If you enable CloudTrail to log sign-in events to your log, you need to be aware of how CloudTrail chooses where
        to log the events
    - Users are redirected to either global or a regional sign-in endpoint, based on whether the selected service
        console supports regions
    - You can manually request a certain regional sign-in endpoint by signing in to the region-enabled main console home
        page using a URL syntax like: https://alias.signin.aws.amazon.com/console?region=ap-southeast-1, AWS redirects
        you to ap-southeast-1 regional sign-in endpoint         

- **_IAM Best practices_**
    1. Lock away your AWS account Root user access keys
    2. Create individual IAM users
    3. Use AWS defined policies to assign permissions whenever possible
    4. Use groups to assign permissions to IAM users
    5. Grant least privilege
    6. Use access levels to review IAM permissions(AWS categorizes each service action into one of four access levels
        based on what each action does: List, Read, Write, or Permissions management)
    7. Configure a strong password policy
    8. Enable MFA for privileged users
    9. Use roles for applications that run on AWS EC2 instances
    10. Delegate by using roles instead of sharing credentials
    11. Rotate credentials  regularly
    12. Remove unnecessary credentials
    13. Use policy conditions for Extra security
    14. Monitor Activity in your AWS account    
    
**Summary**:

IAM consists of the following:
- Users
- Groups(group users and apply policies to them)
- Roles
- Policy documents
- Root account has complete admin access when you first set up your AWS account
- AWS strongly recommends that you do not use root user for your everyday tasks, even administrative ones 
- IAM does not apply to any region at this time
- **New users have no permissions, they have AccessKeyId, and secret access keys when they are first created**
- Access key ids and secret keys cannot be used as passwords to login to the console, we use them to access AWS via API or CLI
- Set up MFA on root account, always
- Create and customize your own password rotation policies
- Power user access allows access to all AWS resources except for mgmt of groups and users within IAM
- Secure access to AWS resources for applications that run on EC2
- Identity federation - users already having passwords get temporary access to your AWS account
- Identity information for assurance - AWS CloudTrail provides information about who made requests for your resources
- Payment Card Industry(PCI) Data Security Standard(DSS) compliance
- Eventually consistent - achieves high availability by replicating data across multiple servers, but a change
    committed must be replicated across IAM might take some time to be reflected
    eg: creating or updating users, groups, roles or policies
- Free to use, you will be only charged for the use of other AWS resources by your IAM users
- Checks each policy that matches your context of request
- By default it is an implicit deny(all requests are denied), explicit deny overrule any allows,
    explicit allows overrides this default
- Identity-based policies is not the way to provide cross-account access   

[Back to Table of Contents](#toc)

# Active Directory Integration:
### How is it done?
Imagine a user is at home, and he wants to login to the AWS console, and they are working on their own home network
So they haven’t already signed-in into the work network.

What they(users) would do is to browse to a URL, for eg: /adfs/ls/IdpInitiatedSignOn, 
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
1. Can you authenticate with Active Directory: Yes, using SAML(Secure Assertive Markup Language) authentication
A: Whether or not you are authenticating to active directory first and then given a security credential or,
2. if you get the temporary security credential first, which is then authenticated against the active directory?
A: You always authenticate against active directory first and then you would be assigned the temporary security credential

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

<a name ="s_3_lifecycle_mgmt"></a>
**S3 Lifecycle management**:
- Can be used in conjunction with versioning
- Can be applied to current versions and previous versions.
- Following actions are allowed in conjunction with or without versioning:
    - archive to Glacier storage class(30 days after IA, if relevant)
    - permanent delete
    - archive and permanent delete
    - transition to the Standard: Infrequent Access Storage class(128kb and 30 days after the creation date)

[Back to Table of Contents](#toc)

**S3 Lifecycle management Exam tips**:    
- Can be used with versioning
- Can be applied to current and previous versions
- Following actions can  now be done
    - Transition to Standard-IA(128kb and 30 days after creation date)
    - Archive to glacier storage class(30 days after IA)
    - permanently delete

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

<a name ="s3_ta"></a>
# S3 transfer acceleration
- accelerates uploads to S3 using CloudFront edge networks
- makes use of a distinct url to upload to a edge location which will then transfer to S3
- costs extra, and has the greatest impact on people who are in far away location

[Back to Table of Contents](#toc)

# S3 static websites
- Use S3 to host static websites
- Serverless
- Very cheap, scales automatically
- STATIC only, cannot host dynamic sites

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

<a name ="ec2"></a>
# EC2(Elastic Compute Cloud)

- Provides resizable compute capacity in the cloud. 
- You have root access to the EC2 instances, be able to restart, terminate, reboot.
    You need to have a key & key pair to access the instance
- Reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity,
  both up and down, as computing requirements change.
- only pay for the capacity you actually use
- provides developers the tools to build failure resilient apps and isolate from common failure scenarios
- 20 instances soft limit per account
- 2 types of block store devices namely `Elastic Block store` which are persistent and Network attached virtual drives,
    these are not directly connected to the host where the instance is but are attached to the network, where as
    `Instance-store` are not persistent(ephemeral), basically a virtual hard drive on the host allocated to this EC2 instance
- So, EBS-backed EC2 instance has a EBS root volume, and Instance-store backed EC2 instance has instance-store root volume

<a name ="ec2_options"></a>
**EC2 options**:
- **_On demand_**: 
    - Allow you to pay a fixed rate by the hour(or by the second) with no commitment. 
    - User that want low cost and flexibility without any upfront payment or long-term commitment. 
    - Apps with spiky, short term, or unpredictable workloads that cannot be interrupted.
    - Apps being developed or tested for the first time
               
- **_Reserved_**: 
    - 1 or 3 year terms, provide discounts on the hourly charge by providing a capacity reservation
    - Apps with steady state or predictable usage. Apps that require reserved capacity.
    - Users able to make upfront payments to reduce their total computing costs even further

- **_Spot_**: 
    - Applications that have flexible start and end times.
    - Enable you to bid whatever price you want for instance capacity, providing for even greater savings.
    - Users with urgent computing needs for large amounts of additional capacity.
    - If the spot instance is terminated by Amazon EC2, you will not be charged for the partial hour of usage,
    but if you terminate the instance yourself, you will be charged for any hour in which the instance ran

- **_Dedicated hosts_**:
    - Useful for regulatory requirements that may not support multi-tenant virtualization
    - Reduces costs by allowing you to use your own existing server-bound software licenses
    - Can be purchased on-demand
    - Can be purchased as a Reservation for up to 70% off the on-demand price 
    - Useful for physical EC2 server dedicated for your use.

[Back to Table of Contents](#toc)

<a name ="ec2_instance_types"></a>
# EC2 Instance Types:

| Family |    Speciality                |  Use Cases
|------- |------------------------------|-----------------------------------------------------------|
| T2     | Lowest Cost, General Purpose | Web Servers/Small DBs                                     | 
| M4     | General Purpose              | Application Servers                                       |              
| C4     | Compute Optimized            | CPU Intensive Apps/DBs                                    |  
| R4     | Memory Optimized             | Memory Intensive Apps/ DBs                                |
| G2     | Graphics/General Purpose GPU | Video Encoding, Machine Learning, 3D Application Streaming|
| I2     | High Speed Storage           | NoSQL DBs, Data Warehousing etc.                          |
| F1     | Field programmable gate array| hardware acceleration for your code                       |
| D2     | Dense storage                | File Servers/Data Warehousing/Hadoop                      |
| P2     | Graphics/General Purpose GPU | Machine Learning bitcoin mining etc.                      |
| X1     | Memory Optimized             | SAP HANA/Apache Spark etc.                                |


# How to remember?
D - for Density

I - for IOPS

R - for RAM

T - for cheap general purpose(think of T2 Micro)

M - main choice for general purpose apps

C - for Compute

G - Graphics

F - FPGA 

P - Graphics(think pics)

X - Extreme memory

Finally we are down to the term `DR MC GIFT PX` 

[Back to Table of Contents](#toc)

<a name ="ebs"></a>
# Elastic Block Storage(EBS)
- Allows you to create storage volumes and attach them to Amazon EC2 instances. 
- Once attached, you can create a file system on top of these volumes, run a database,
    or use them in any other way you would use a block device. 
- Amazon EBS volumes are places in specific Availability Zone,
    where they are automatically replicated to protect you from the failure of a single component.

<a name ="ebs_volume_types"></a>
# EBS Volume Types:
- **_General Purpose SSD(GP2)_**:
    - General purpose, balances both price and performance.
    - Ratio of 3 IOPS per GB with upto 10,000 IOPS and the ability to burst upto 3,000 IOPS for short periods 
    for volumes < 334Gib and above
- **_Provisioned IOPS SSD(I01)_**: 
    - Designed for I/O apps  such as large relational or NoSQL databases.
    - Use if you need > 10,000 IOPS
    - Can provision up to 20,000 IOPS per volume
- **_Throughput Optimized HDD(ST1)_**:
    - Used for big data, data warehouses, and log processing etc.
    - Where data is written in sequence
    - They cannot be boot volumes
- **_Cold HDD(SC1)_**:
    - Lowest cost storage for infrequently accessed workloads
    - File server
    - Cannot be a boot volume
- **_Magnetic(Standard)_**: 
    - Lowest cost per gigabyte of all EBS volume types.
    - Ideal for workloads where data is accessed infrequently, and apps where the lowest storage cost is important
    - Termination protection is turned off by default, you must turn it on

[Back to Table of Contents](#toc)
<a name ="volume_vs_snapshot_lab"></a>
# EBS Volumes vs Snapshot Lab
- **EBS volume and EC2 instance will always be in the same AZ**
- In order to move 1 EBS volume from 1 AZ to other you need to create a snapshot first and then from that snapshot
    you can create a new volume in a new AZ
- In order to move one instance in a region to another region, first you need to do is create a snapshot, and then you copy 
    the snapshot to the new region, once it is in the new region you essentially create an **image of that snapshot**,
    and then will be able to boot from EC2
- Snapshots are used for backups, and images are used to boot ec2 instances from volumes
- **_Volumes exists on EBS_**, think of them as virtual hard disk
- **_Snapshots exists on S3_**
- Snapshots are point in time copies of volumes
- You can take a snapshot of volume, this will store that volume on S3
- **_Snapshots are incremental_** this means that only the blocks that have changed since your last snapshot are moved to s3
- **_Creating the first snapshot takes a lot of time_**
- To create  snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking a snapshot
    However you can take a snap when the instance is running
- You can create ami's from volumes and snapshots
- You can change EBS volume sizes on the fly, including changing the size and storage type
- **You must deregister the AMI before being able to delete the root device.**
    
[Back to Table of Contents](#toc)

<a name ="ec2_exam_tips"></a>
**EC2 Exam tips**:
- Know the differences between
    - on demand
    - spot
    - reserved
    - dedicated hosts
- Remember with spot instances
    - if you terminate the instance, you pay for the hour
    - if AWS terminates it, you get the hour in which it was terminated for free
- EBS consists of:
    - SSD, General purpose-GP2-(up to 10,000 IOPS)
    - SSD, Provisioned IOPS-IO-1-(more than 10,000 IOPS)
    - HDD, Throughput optimized-ST1-frequently accessed workloads
    - HDD, Cold-SC1-less frequently accessed data
    - HDD, magnetic-standard-cheap, infrequently accessed storage
- **You cannot mount or attach 1 EBS volume to multiple EC2 instances, use instead EFS**
- Different ec2 types `DR MC GIFT PX`    

[Back to Table of Contents](#toc)

**EC2 Lab summary**:
- **_Termination protection_** is turned **off** by default, you must turn it on
- On an **_EBS backed instance_**, the default action is for the **_root EBS volume_** 
    to be deleted when the instance is terminated
- Root volumes cannot be encrypted. You can also use a third party tool to encrypt the root volume,
    or this can be done when creating ami's in the aws console or using the api
- Additional volumes can be encrypted

[Back to Table of Contents](#toc)

<a name ="security_grp_basics"></a>
# Security Groups Basics
- A virtual firewall
- One Ec2 instance can have multiple security groups
- One security group can be attached to multiple Ec2 instances
- Are stateful, if you create an inbound rule allowing traffic in, traffic will be allowed back out again
- All inbound traffic is blocked by default
- All outbound traffic is allowed by default
- Changes to security groups take place immediately
- You cannot block specific Ip addresses you need to use network access control lists
- You can specify allow rules, but not deny rules

<a name ="volumes_snapshots_security"></a>
**Volume vs snapshots - security**:
- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically
- You can share snapshots, but only if they are unencrypted. These snapshots can be shared with other AWS accounts or
    made public

[Back to Table of Contents](#toc)

<a name ="raid"></a>
# RAID, Volumes and Snapshots:
**RAID**:
- Redundant Array of Independent Disks
- RAID 0: Striped, No redundancy, good performance
- RAID 1: Mirrored, Redundancy
- RAID 5: Good for reads, bad for writes, AWS does not recommend putting RAID 5 ever on EBS
- RAID 10: Striped and Mirrored, Good redundancy, good performance
- You will use RAID arrays on AWS when you are not getting the disc I/O when required. Add multiple volumes and create
    a RAID array to give you the disc I/O you require, typically you will end up using RAID0 or RAID10

<a name ="raid_snapshot"></a>
**How do I take a snapshot of a RAID Array**:

**Problem**: 
Take a snapshot, the snapshot excludes data held in the cache by apps and the OS. This tends not to matter on a single
    volume, however using multiple volumes in a RAID array, this can be a problem due to interdependencies of the array.

**Solution**: 
- Take an application consistent snapshot
- Stop the app from writing to the disk
- Flush all the caches to the disk  
     1. Freeze the filesystem
     2. Unmount the RAID array
     3. Shutting down the associated EC2 instance

[Back to Table of Contents](#toc)

<a name ="encrypted_root_vol_snapshot_lab"></a>
# Encrypted Root device Volumes & Snapshots - Lab
- To create a snapshot for an EBS volume that serve as root devices, you should stop the instance before taking the
    snapshot
- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically
- You can share share snapshots only if they are unencrypted, these snapshots can be shared with other AWS accounts,
    or made public

[Back to Table of Contents](#toc)

<a name ="ami_create"></a>
# Creating an Amazon Machine Image(AMI):
- Provides the information required to launch a virtual server in the cloud.
- You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need.
- You can also launch instances from as many different AMIs as you need. 
- It consists of the following:
    - A template for the root volume of the instance(for example an Operating System, an app server, and apps)
    - Launch permissions that control which AWS accounts can use the AMI to launch the instance
    - A block device mapping that specifies the volumes to attach to the instance when it’s launched
- **AMIs are regional**, you can only launch an AMI from the region in which it is stored. 
- However you can copy AMI’s to other regions using the console,command line or the Amazon EC2 API

[Back to Table of Contents](#toc)

<a name ="ami_types"></a>
# AMI types(EBS vs Instance Store)
- You can select an AMI from:
    - Region
    - Operating System
    - Architecture(32-bit or 64-bit)
    - Launch permissions
    - Storage for the Root Device(Root Device Volume)
      - **_Instance Store(Ephemeral storage)_**:
            - These cannot be stopped.
            - If the underlying host fails, you will lose your data.
            - We can reboot and not lose data
      - **_EBS backed volumes_**:
            - These instances can be stopped.
            - You will not lose the data on this instance if it is stopped.
            - We can reboot and not lose data
- By default both ROOT volumes will be deleted on termination, however with EBS volumes,
    you can tell AWS to keep the root device volume.
- All AMIs are categorized as either backed by Amazon EBS or backed by instance store
- **_For EBS volumes_**: The root device for an instance launched from the AMI is an Amazon EBS volume created from an 
    Amazon EBS snapshot. If you need fast provisioning times we prefer EBS backed volumes.
- **_For Instance store volumes_**: The root device for an instance launched from the AMI is an instance store volume
    created from a template stored in Amazon S3. It takes time to provision an instance store volume than a EBS volume.
    This might take some time to provision.

[Back to Table of Contents](#toc)

<a name ="ebs_instance_exam_tips"></a>
# EBS vs Instance Store - Exam Tips
- Instance store volumes are sometimes called ephemeral storage
- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data
- EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped
- You can reboot both, you will not lose your data
- By default, both ROOT volumes will be deleted on termination, however with EBS volumes, you can tell AWS to keep the
    root device volume

[Back to Table of Contents](#toc)

<a name ="loadbalancer_healthcheck_lab"></a>
# Load Balancers and Health Checks
- Instances monitored by ELB can be reported as `InService`, or `OutOfService`
- They provide Health Checks by simply talking to it
- Have their own DNS name. You are never given an IP address. Amazon handles it on their own.
- Read the ELB FAQ for Classic Load Balancers

[Back to Table of Contents](#toc)

<a name ="cloudwatch"></a>
# CloudWatch EC2:
- CloudWatch is for performance monitoring
- CloudTrail is for auditing
- Default metrics available for EC2 instance: CPU related, Disk related, Network related, and Status check
- Standard monitoring = 5 minutes
- Detailed monitoring = 1 minute
- Creates awesome dashboards to see what is happening with your AWS environment
- Allows you to set Alarms that notify you when particular thresholds are hit
- Events help you to respond to state changes in your AWS resources
- Logs allow to aggregate, monitor, and store logs

[Back to Table of Contents](#toc)

<a name ="iam_with_ec2"></a>
# Using IAM roles with EC2 Lab
- Roles are more secure than storing your access key and secret access key on individual EC2 instances
- Roles are easier to manage
- Roles can be assigned to an EC2 instance AFTER it has been provisioned using both the command line & the AWS console
- **Roles are universal, you can use them in any region**

[Back to Table of Contents](#toc)

<a name ="ec2-meta-data"></a>
# EC2 Instance Metadata
- Metadata information location: **curl http://169.254.169.254/latest/meta-data/**
- public ip curl http://169.254.169.254/latest/meta-data/public-ipv4

[Back to Table of Contents](#toc)

<a name ="autoscaling"></a>
# AutoScaling 101
## Launch Configurations & Auto Scaling Groups
- Before you create auto scaling group you need to create a launch configuration

[Back to Table of Contents](#toc)

<a name ="ec2_placement_groups"></a>
# EC2 Placement Groups
- Is a logical grouping of instances within a **_single Availability zone_**. 
- Enables apps to participate in a low-latency , 10Gbps network
- Recommended for apps that benefit from **_low network latency, high network throughput, or both_**
- **_Cannot span multiple availability zones_**
- The name you specify a placement group must be unique within your AWS account
- Only certain types of instances can be launched in a placement group(Compute optimized, GPU, Memory Optimized,
    Storage Optimized)
- AWS recommends homogenous instances (instances of the same size, and same family)within placement groups
- Cannot merge placement groups
- Cannot move an existing instance into a placement group. You can create an AMI from your existing instance,
    and then launch a new instance from the AMI into a placement group

[Back to Table of Contents](#toc)

<a name ="efs"></a>
# EFS(Elastic File System):
- A file storage service for EC2 instances. A simple interface that allows you to create and quickly configure
    file systems
- Storage capacity is elastic, growing and shrinking automatically as you add and remove files,
    so your app has the storage it needs, when they need it
- **_Supports NFS version v4_**
- **_You only pay for the storage you use(no pre-provisioning required), not like EBS,
    we can just start putting files on it_**
- **_Can scale up to petabytes_**
- **_Supports thousands of concurrent NFS connections_**
- **_Data is stored across multiple AZ’s within a region_**.
    We do not get any durability rating from Amazon since it is quite new
- **_Read After Write consistency_**
- EFS is a **_BLOCK based storage_**, we can share files with other EC2 instances.
- make sure EC2 instances are in the same security group as the EFS
- We make use of EFS essentially as a file server, making it as a centralized repository
- We can apply user level and/or directory level permissions, make directories restricted

[Back to Table of Contents](#toc)

<a name ="aws_lambda"></a>
# Lambda Concepts
- A compute service where you can upload your code and create a lambda function
- Takes care of provisioning and managing the servers that you use to run the code
- We need not worry about OS, patching, scaling etc.
- A lambda basically is encapsulating data centres, hardware, assembly code/protocols, high level languages, OS,
    application layer etc.
- We can use Lambda as an event-driven compute service where AWS Lambda runs your code in response to events.
    These events could change be changes to data in an Amazon S3 bucket or an Amazon DynamoDB table
- We can also use it as a compute service to run your code in response to HTTP requests using Amazon API Gateway or
    API calls made using AWS SDKs.
- 1 request will invoke 1 lambda function, it scales out easily.
- Languages supported are Node.js, Java, Python, C#
- Lambda pricing:
    - _**Number of requests**_: First 1 million requests are free. $0.20 per 1 million requests thereafter
    - _**Duration**_: Calculated from the time your code begins executing until it returns or otherwise terminates,
        rounded up to the nearest 100ms. The price depends on the amount of memory you allocate to your function.
        You are charged $0.00001667 for every GB-second used
- Why Lambda?
    - No servers
    - Continuously scaling
    - Really cheap

[Back to Table of Contents](#toc)

<a name ="aws_lambda_exam_tips"></a>
**AWS Lambda-Exam tips**:
- Scales out(not up) automatically
- Lambda functions are independent 1 event = 1 function
- Lambda is serverless
- Know what services are serverless: eg: S3, API Gateway, Lambda, DynamoDB
- 1 Lambda function can trigger other lambda functions, 1 event = x functions if functions trigger other functions
- Architecture can get extremely complicated, `AWS X-Ray` allows for debugging
- Lambda can do things globally
- **Know your triggers, esp in the us-east-1 region**

[Back to Table of Contents](#toc)

<a name ="dns"></a>
# Route53
#DNS 101
- Convert human friendly domain names into an Internet Protocol(IP) address
- Last word represents top level domain
- Top domain names are controlled by IANA(Internet Assigned Numbers Authority) in  a root zone db
- **Domain Registrars**
    - An authority that can assign domain names directly under 1 or more top-level domains.
- **Start of Authority records**
    - Stores information about name of the server, admin of the server, current version of data file, default no.of seconds 
        for the ttl file on resource records, etc. 
- **Name Server(NS) records**: 
    - Used by top level domain servers to direct traffic to the content DNS containing authoritative records
- **A records**: 
    - Fundamental type of DNS record, and stands for "Address". A record is used by a computer to translate the name of the 
        domain to IP address.
- **TTL(Time to Live)**: 
    - The length that a DNS record is cached on either the Resolving server or the users own  local PC is equal 
        to the value of the TTL, the lower the ttl, the faster the changes to DNS records take to 
        propagate throughout the internet
- **CName(Canonical Name)**: Used to resolve one domain name from other
- **Alias Records**:
    - Used to map resource record sets in your hosted zone to elbs, cloudfront distributions,
        or S3 buckets configured as websites
    - Works like a CName,mapping one DNS to another, but a CNAME cannot be used for naked domain names(zone apex record),
        eg: you cannot have a CNAME for http://acloud.guru, it must be either an A record or Alias.
- **ELB's do not have a predefined IPv4 addresses, you resolve to them using a DNS name**
- Difference between Alias record and CNAME, when you are making a request to Route53 for a DNS record you will be
    charged if using a CNAME, else if using an alias record you won't be charged
- Always chose Alias record over a CNAME
- You always need SOA(start of authority) record for any hosted zone in Route53

[Back to Table of Contents](#toc)

<a name ="route53_routing_policies"></a>
# Route53 routing policies
- **_Simple_**
    - Default routing policy when you create a new record set
    - Commonly used when you have a single resource that performs a given function for your domain,
        eg: having 1 server serving all the content
        
- **_Weighted_**
    - Split your traffic based on different weights assigned, eg: 10% traffic to us-east-1, and 90% to eu-west-1
    
- **_Latency_**
    - Route traffic based on lowest latency for your end user
    - To use latency-based routing you create a latency resource record set for the Amazon EC2 in each region.
        When Route53 receives a query, it will select latency resource record set for the region with the lowest latency

- **_Failover_**
    - Used when you want to create an active/passive set up
    - Route53 will monitor the health of your primary site using a health check

- **_Geolocation_**
    - Route traffic as per geographical location of the user(location from which DNS queries originate)
    - eg: requests from europe goto eu-east-2, and requests from us goto us-east-1

[Back to Table of Contents](#toc)

<a name ="dns_exam_tips"></a>
**DNS-Exam Tips**
- ELB's do not have a IPv4 addresses, you resolve to them using a DNS name
- Understand difference between an Alias record and a CNAME
- Given a choice, always choose Alias record over CNAME
- Different routing policies 
- Route53 support MX records
- There is 50 domain names available by default, however it is a soft limit and can be raised by contacting AWS support.

[Back to Table of Contents](#toc)

<a name ="databases"></a>
# Databases
- **_RDS_**
    - OLTP(Online Transaction Processing) purposes
    - SQL, MySQL, PostgreSQL, Oracle, Aurora, MariaDB
    - DynamoDB - NoSQL
- **_RedShift_**: OLAP(Online Analytics Processing)
- **_DMS_**: Database Migration service
- **_ElasticCache_**
    - Deploy, operate, and scale an in-memory cache in the cloud
    - Improves performance of apps by allowing to retrieve information from fast, managed, in-memory caches,
      instead of relying entirely on slower disk-based databases
    - Supports 2 open-source in-memory caching engines: Redis, Memcached     

[Back to Table of Contents](#toc)

<a name ="rds"></a>
# Launching an RDS Instance - Lab
- 2 separate security groups
- To create a publicly accessible RDS instance, you should be opening up your RDS security group(port 3306)
  to allow and trust any web server security group to be able to connect to it

[Back to Table of Contents](#toc)

<a name ="rds_backups_multiaz"></a>
# RDS - Backups, Multi-AZ & Read replicas
- 2 types of backups, automated and database snapshots
- **_Automated backups_**
    - Allow you to recover your database to any point in time within a "retention period"
    - Retention period can be between 1 and 35 days
    - Take full daily snapshots and will restore transaction logs
    - When recovery is done, AWS will first choose the most recent daily backup, and then apply transaction logs
        relevant to that day
    - Backups enabled by default, and are taken within  a defined window, due to which storage I/O may be suspended,
        and you will observe increased latency  
    - Data stored in S3, get free storage space equal to the size of your database
- **_Snapshots_**
    - User initiated
    - Stored even after you delete rds instance
    -  I/O operations are suspended while you take a database snapshot
- In RDS when using multiple availability zones, you cannot use the secondary database as an independent read node    
- Absolutely free of charge when replicating data from your primary RDS instance to your secondary RDS instance 
- When you add a rule to an RDS security group you do not need to specify a port number or protocol
- If you are using Amazon RDS Provisioned IOPS storage with MySQL and Oracle database engines 6TB is the maximum size
  RDS volume you can have by default
- You can restore a full snapshot or a point in time
- You can take snapshot and then decide to scale up by changing the storage type of the instance    
- Whenever you restore a backup, or a snapshot, the restored version of the db will be a new rds instance with a new
    endpoint
- **_Encryption_**
    - Encryption at rest supported for MySQL, oracle, SQL Server, PostgreSQL & MariaDB
    - Done using AWS Key Management Service(KMS)
    - Once encrypted, data stored at rest in the underlying storage is encrypted, along with automated backups,
        snapshots, read replicas
    - Encrypting an existing db instance is not possible unless you create a new instance with encryption,
        and migrate the data
- **_Multi AZ_**
    - Used for recovery purposes only, not used for improving performance
    - Allows you to have exact copy of your production db in another AZ
    - AWS handles replication for you, writes to db are synchronized to your standby db
    - In the event of planned maintenance, db instance failure, or an AZ failure, Amazon RDS will automatically
        failover to the standby so that database operation resume quickly without administrative intervention         
- **_Read Replicas_**
    - Used for scaling and not disaster recovery!!!
    - Must have automatic backups turn on
    - 5 read replica copies of any database
    - Can have read replicas of read replicas
    - Each read replica has its own DNS endpoint
    - Cannot have read replicas that have multi-az
    - Can create read replica's of multi-az source db however
    - can be promoted to be their own db
    - cannot write to a read replica, READ only!!!
- To have a push-button scaling or scaling on the fly, always choose dynamodb, usually you will need to have a bigger
  instance size    
- By default, the maximum provisioned IOPS capacity on an Oracle and MySQL RDS instance (using provisioned IOPS) is
    30,000 IOPS.

[Back to Table of Contents](#toc)

<a name ="dynamodb"></a>
# DynamoDB
- Fast, flexible NoSQL database service for application requiring single digit millisecond latency at any scale
- Fully managed db, supporting both document and key-value data models
- Stored on SSD
- Spread across 3 geographically distinct data centres
- **_Eventual Consistent Reads(Default)_**
    - consistency across all copies of data is usually reached within a second
    - repeating a read after a short time should return the updated data
- **_Strongly Consistent Reads_**
    - returns a result that reflects all writes that received a successful response prior to the read
- **_Provisioned throughput capacity_**
    - write throughput capacity $0.0065 per hour for every 10 units
    - read throughput capacity $0.0065 per hour for every 50 units
- Storage costs of $0.25Gb/month

[Back to Table of Contents](#toc)

<a name ="redshift"></a>
# Redshift
- Fast, powerful, fully-manged, petabyte-scale data warehouse service in the cloud
- Start small with $0.25 per hour, with no upfront costs, and scale to a petabyte or more for $1000/TB/year
- **_Configuration_**
    - single node(160Gb)
    - multi-node
        - Leader node managing client connection and receives queries
        - Compute node up to 128 nodes, store data, perform queries & computation
- **_Columnar Storage_**
    - Data stored in the form of columns instead of rows
    - Ideal for data warehousing and analytics
    - Columnar data being stored sequentially on the storage media, and since only columns involved in the queries
        are processed, column based systems require fewer I/Os
    - Data can be compressed due to data being similar in a column
    - Doesn't require indexes, or materialized views, hence uses less space
    - Automatically selects the compression scheme by sampling your data        
- **_Massively Parallel Processing_**
    - Automatically distributes data & query load across all nodes
    - easy to add nodes to your warehouse, and enable fast query performance
- **_Pricing_**
    - Compute Node hours, billed per unit, per node per hour, eg: 3 node warehouse running persistently for a month
        would be 2160 instance hours, only compute nodes will incur charges
    - Backup
    - Data transfer
- **_Security_**
    - Encrypted in transit using SSL
    - Encrypted at rest using AES-256
    - By default takes care of key management
- **_Availability_**
    - 1 AZ
    - can restore snapshots to new AZ's in the event of an outage    

[Back to Table of Contents](#toc)

<a name ="elasticache"></a>
# Elasticache
- Deploy, operate, and scale an in-memory cache in the cloud
- Improves performance of web apps by retrieving information from fast, managed, in-memory caches instead of slower
    disk-based databases
- Types
    - **_Memcached_**
        - Memory object caching system
        - Elasticache is protocol compliant with memcached
    - **_Redis_**
        - open-source, in-memory key-value store supporting data structures such as sets and lists
        - supports Master/Slave replication and multi-AZ which can be used to achieve cross AZ redundancy
- Elasticache is a good choice if your database is particularly read heavy and not prone to frequent changing
- RedShift is a good answer if the reason your db is feeling stress is because mgmt. kept on running OLAP transactions

[Back to Table of Contents](#toc)

<a name ="aurora"></a>
# Aurora
- MySQL-compatible, relational db engine that combines speed and high-availability of high-end commercial databases
- Provides 5 times better performance than MySQL
- **_Scaling_**
    - Start with 10Gb, scales in 10Gb increments to 64Gb
    - Compute resources can scale upto 32vCPUs and 244Gb of memory
    - 2 copies of data in each AZ, with minimum of 3 AZ, ideally 6 copies
    - Transparently handle loss of 2 copies data without affecting database write availability & up to 3 copies without
        affecting read availability
    - data blocks & disks are continuously scanned for errors
- **_Replicas_**
    - Aurora replicas - can have 15 of them, if you loose primary aurora db for whatever reason, failover will
        automatically appear to your aurora replica 
    - MySQL Read Replicas - 5 of them

[Back to Table of Contents](#toc)

<a name ="vpc"></a>
# Virtual Private Cloud(VPC)
- Virtual data centre in the cloud, similar to having your own data center, and **logically isolated from other VPCs on AWS**
- You can launch AWS resources in a virtual network you define
- You have complete control over your virtual networking environment, including selection of your own IP address range,
    creation of subnets, network access control lists, configuring route tables, and network gateways
- **1 VPC in 1 region, or to simply put a vpc is always region specific**
- **1 subnet = 1 AZ, or simply put a subnet cannot span multiple AZs**
- A VPC can span multiple subnets
- AWS client has full control over resources and virtual compute instances
- You can have 1 or more IP addresses subnets in a VPC
- Security groups are stateful, network access control lists are stateless, i.e. with nacls we will need to open both
    inbound and outbound ports for eg for port 80, but not with security groups    
- Subnets and ACLs provide much better security over your AWS resources
- Instances security groups, they span multiple AZs and hence can span multiple VPCs
- Subnet acls
- Default vs custom vpc
    - Default allows you to deploy immediately, user friendly
    - All subnets have a route to the internet, do not get private subnets in default vpc
    - Each ec2 instance will has private and public IP address, in a custom vpc with a private subnet we won't get a 
        public ip address we only get a private address
- VPC peering
    - Allows you to connect 1 vpc to another via direct connect route using private ip
    - Instances behave as if they were on the same private network
    - Peering possible with vpcs in the same aws account or in different aws accounts
    - Always a star configuration, 1 central VPC peers with 4 others. No transitive peering! 
- Whenever you create a new VPC AWS creates a default ACL, a default security group, and a route, but it won't create a
    subnet, you will need to create one yourself
- Always going to loose 5 ip addresses when you create a subnet, since those 5 are reserved by Amazon
- You can have 1 NAT gateway for 1 custom vpc
- Allowed to have 5 VPCs in a region

[Back to Table of Contents](#toc)

## VPC Types
- A Default VPC
    - created in each AWS region when an AWS account is created
    - has default CIDR, Security group, N ACL, and route table settings
    - has an internet gateway by default
- A Custom VPC
    - is a VPC created by the owner of the AWS account
    - AWS user creating the custom VPC can decide the CIDR
    - has its own default security group, N ACL, and route tables
    - does not have an internet gateway by default, one needs to be created if needed

[Back to Table of Contents](#toc)

<a name ="vpc_compo"></a>
## Components of a VPC
- **_Classless Inter Domain Router(CIDR) and IP address subnets_** eg. 10.0.0.0, 172.16.0.0/16, 192.168.0.0/16
- **_Implied router_**
    - No need to specify any configuration, AWS handles it all!
    - Is the central VPC routing function, does all the subnet to subnet routing within a VPC
    - Connects the different AZ's together and connects the VPC to the Internet Gateway
    - Each subnet will have a route table the router uses to forward traffic withing the VPC
    - The route tables will also have entries to external destinations  
- **_Route tables_**
    - You can have up to 200 route tables per VPC
    - In each route table you can have up to 50 routes entries
    - **Each subnet MUST be associated with only 1 route table** at any given time. 
        **1 route table can be assigned to multiple subnets**, but
        **1 subnet cannot be attached to more than 1 route table**
    - If you do not specify a subnet-to-route-table association, the subnet will be associated with the default(main)
        VPC route table
    - **Main route table is created by default** for your VPC by AWS
    - You can also edit the main(default) route table, but you cannot delete the main(default) route table, however you
        can make a custom route table manually become the main route table, then you can delete the former main, as it
        is no longer a main route table
    - **Every route table in a VPC comes with a default rule that allows all VPC subnets to communicate with one another**,
        you cannot modify or delete this rule
- **_Internet gateway_**
    - Is the gateway through which your VPC communicates with the internet, and with other AWS services
    - **Only 1 internet gateway per vpc**
    - A horizontally scaled, redundant, and highly available VPC component
    - Performs NAT(static one-to-one) between your private and public(or elastic) IPv4 addresses
    - Supports both IPv4 and IPv6
- **_Security groups_** 
    - Virtual firewalls - **works at the `Elastic Network Interface(ENI)` level**
    - Controls traffic at the EC2 level, specifically at the ENI level
    - Up to 5 security groups per EC2 instances interface   be applied
    - **Stateful**, return traffic, of allowed inbound traffic, is allowed, even if there are no rules to allow it
    - **Can only** have permit rules, **can NOT** have deny rules
    - Implicitly deny rule at the end
    - Security groups are associated with EC2 instances network interfaces
    - All rules are evaluated to find a permit rule
    - Any virtual server instance(EC2) created without specifying a security group for it(during its creation), will be
        assigned the VPC default security group
    - Each VPC created will have a default security group created for it, you can NOT delete a default security group
    - Changes to security groups take effect immediately
    - **Default or Custom Security groups - default settings**
        - Default security group in a default or custom VPC, will have:
            - Inbound rules allowing instances assigned the same security group to talk to one another
            - All outbound traffic is allowed
        - Custom(Non-default) security groups in a VPC will always have:
            - No inbound rule - basically all inbound traffic is denied by default
            - All outbound traffic is allowed by default
    - **Security group configurations**
        - You can use security group names as the source or destination in other security group rules
        - You can use the security group name as the source in its own inbound security group rules
        - Security groups are directional and can use allow rules only
        - A security group set of rules ends with an implicit deny any
        - To allow the EC2 instances assigned to a security group to communicate with one another,
            - Create a security group, apply it to all these instances, and configure a rule that allows any traffic,
                on any protocol/ports, the source of which is the security group itself
            - Be cautious that the security group is a VPC resource, which means member EC2 instances can be from
                different subnets and AZs too
        - To allow all EC2 instances on a subnet to communicate with each other,
            - Create a security group and apply it to those instances, and configure a rule that allows communication on
                all protocols/ports, the source of which is the subnet CIDR block                          
- **_Network Access Control Lists(N. ACLs)_** 
    - **N.ACL works at the subnet level**
    - A function performed on the implied router(implied VPC hosts the Network ACL function)
    - N.ACL are Stateless. Outbound traffic for an allowed inbound traffic, must be "explicitly" allowed too
    - N.ACL can have "permit" and "deny" rules
    - N.ACL is a set of rules, each has a number
    - N.ACL rules are checked for "permit" from lower numbered rules until either a permit is found, or an
        explicit/implicit deny is reached
    - You can insert rules(based on the configured rule number spacing) between existing rules, hence, it is recommended
        to leave a number range between any 2 rules ot allow for edits later
    - N.ACLs end with an **explicit deny** any, which you can NOT delete
    - A subnet must be associated with a N.ACL, if you do not specify the N.ACL, the subnet will get associated with the
        default N.ACL automatically
    - You can create your own custom NACL, you do not have to use the default one
    - A default N.ACL allows all traffic inbound and outbound
    - A custom(non-default) N.ACL blocks/denies all traffic inbound and outbound by default
    - **Things to remember!!!**
        - If an instance in a VPC is unable to communicate over a certain protocol/port with another instance in the
            same VPC, then the problem is the security settings of:
                - Security group or NACL of the source instance, and/or
                - Security group or NACL of the destination instance
                    - The problem will never be routing table configuration, due to the default route entry
        - Remember that N.ACLs are stateless, to allow certain traffic though it, it needs to be allowed(and return traffic)
            in the inbound and outbound rules of the ACL
        - Remember,
            - Inbound in ACL means coming from outside the subnet destined to the subnet. Outbound means going out of the
                subnet
            - Inbound for security group means inbound from outside the instance destined to the instance. Outbound means
                going out of the instance's ENI                                 
- **_Virtual Private gateway_**
    - Imagine if you want to connect your VPC to your company HQ, so that my employees can connect to the servers hosted
        in the VPC, you have to have a virtual private gateway created and attached to your VPC.
        Like Internet gateway which will take the traffic to the outside world through the internet, the VPG will take
        the traffic to your Hq, or premises or branches through either VPN or a direct connection 
    

[Back to Table of Contents](#toc)
<a name = "ip_v6"></a>
## VPC IP Addressing
- All IPv6 addresses are Public
- Hence, AWS allocates the IPv6 address range if you require that
- Once the VPC is created, **you can NOT change its CIDR block range**  
- Always think about the future when you are deciding the CIDR block
- The CIDR block range can be /28 or /16, in ipv4 addresses which is 32 bit long, for /28, the first 28 bits will be reserved
    for subnets and last 4 bits will be for ec2 instances, i.e. you can have upto 16(2^4) ip addresses assigned
    Thus the minimum size of a CIDR block you can have in a VPC on AWS is /28. The 16 bits is too big, it gives you 2 ^16
- If you need a different CIDR size, create a new VPC
- The different subnets within a VPC can NOT overlap, you can however, expand your VPC CIDR by adding new/extra IP addreses
    ranges

[Back to Table of Contents](#toc)

## AWS Reserved IP's in each subnet
- First 4 IP addresses in each subnet and the last one are reserved by AWS
    - for example: if the subnet is 10.0.0.0/24, the ip addresses you cannot use are
    - 10.0.0.0 is the base network
    - 10.0.0.1 VPC router
    - 10.0.0.2 DNS related
    - 10.0.0.3 Reserved for future use
    - 10.0.0.255 last IP
    
[Back to Table of Contents](#toc)

<a name ="nat_instances"></a>
# NAT Instances - Security Group configuration
- NAT instance must be in a public subnet
- NAT instances need to be assigned a security group
- NAT instance is there to enable the private subnet EC2 instances to get to the internet
- No traffic initiated from the internet can access the private subnet
- Only admin SSH traffic can be allowed to the NAT instance(or RDP for Windows)
- Private subnet EC2 instances need to access websites on the internet(HTTP or HTTPS)
- NAT instance's security group must allow:
    - traffic inbound from the private subnet or the private subnet's security group as a source on port 80(HTTP) and
        443(HTTPS)
    - traffic outbound to 0.0.0.0/0(Internet) on Ports 80 and 443
    - traffic inbound from the customer's own network on port 22(SSH) to administer the NAT instance
- When creating a NAT instance, disable source/destination check on the instance
- We can change the source/destination check when an instance is running or stopped
- There must be a route out of the private subnet to the NAT instance, in order for this to work
- The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking increase 
    the instance size
- You can create high availability using ASGs, multiple subnets in different AZs, and a script to automate failover


[Back to Table of Contents](#toc)

<a name ="nat_gateway"></a>
# NAT Gateways 
- is an AWS managed service
- No need to patch, AWS is responsible
- Can Not be assigned a security group
- Works only with elastic Ip, cannot not use a public ip to do its function
- Remember to update your route tables, when you provision a NAT gateway
- 1 NAT gateway in 1 AZ is not good enough, you want them in multiple AZ to have some form of redundancy in case of a 
    failure
- No need to disable source/destination checks
- You can have up to 5 NAT gateways per AZ

[Back to Table of Contents](#toc)

<a name ="nacl_sg"></a>
# Network Access Control Lists vs Security Groups 
- Your vpc comes with a default network ACL, and by default allows all inbound and outbound traffic
- When you first create a new network acl or a custom network acl, there will be no inbound and outbound traffic
- Each subnet must be associated with a network acl, if you don't explicitly associate a subnet with a network acl, the 
    subnet is automatically associated with the default network acl
- You can associate a network ACL  with multiple subnets, however, a subnet can be associated with only 1 network ACL at
    a time. When you associate a netowrk ACL with a subnet, the previous association is removed    
- A network acl can be bound to only 1 vpc, it cannot span across multiple vpcs
- Network ACls contain a numbered list of rules that is evaluated in order, starting with lowest numbered rule.
    Rule 100 for IPv4,and rule 101 for IPv6
- A subnet can be associated with 1 network access control list, but a network acl can be associated with multiple 
    subnets, when you associate a network acl with a subnet the previous association is removed
- Can be used to block specific ip addresses or ip ranges
- A network ACL have separate inbound and outbound rules, each rule can either allow or deny traffic
- Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic and
    vice versa
- N.ACL is the subnet guard and the first line of defense
- Security group is the instance guard and the second line of defense(defense in depth)
- They both work together to secure your hosted environment
- It is also highly recommended to use your own application security means(firewalling) to add a deeper layer to
    your application security
- Changes made to NACLs(or Security groups) take effect immediately, so they are both quick to activate/defend as
    needed
- NACLs can help you block certain ranges of IP address from a large pool(Internet addresses for instance),
    because they do have deny rules. Security groups can NOT block a certain range of IP addresses from Internet
    from getting to your EC2 fleet of instances  

[Back to Table of Contents](#toc)

<a name ="alb"></a>
# Application Load Balancer
You will need atleast 2 public subnets to deploy ALB's 

[Back to Table of Contents](#toc)

<a name="vpc_wizard"></a>
# VPC Wizard
- If a VPC is created with a VPC wizard with private and public subnet options, you get
    - By default, a public subnet associated with a custom route table
    - By default, a private subnet associated with a main route table
    - An IGW created and attached to the VPC
    - By default the wizard will prefer to create a NAT gateway for your VPC, but you have the option to choose a NAT
        instance instead
    - If you choose to launch the NAT instance, the wizard will not allow you to go for less than a M1 small instance
    - Main(default) VPC route table is assigned to the private subnet, it has the VPC local subnets routing entry, and
        an entry 0.0.0.0/0 pointing at the NAT instance/gateway
    - Custom route table will have an entry 0.0.0.0/0 pointing to IGW as a target
    - Note that, creating a VPC creates route tables and not routing instances
- Deleting a VPC with NAT instances
    - A VPC with instances created within,can NOT be deleted unless the user manually terminates those instances
    - In case of a VPC Wizard created VPC with public and private subnets, either a NAT gateway or a NAT instances must 
        be created by the wizard(default is NAT gateway but the user can change that) If NAT instance is created, it has
        to be terminated before you can delete the VPC     
- **_VPC Wizard - Public and VPN only subnet_**
    - Wizard created VPC with public and VPN-only subnets does NOT have a NAT instance or NAT gateway
    - Wizard created VPC will have:
        - Main(default) VPC route table associated with the VPN-only subnet
        - Custom route table associated with the public subnet and pointing at the VPC IGW
        - An IGW created for the VPC
        - VGW with a VPN connection
        - Route propagation enabled for the Main route table for exchanging routes with the VGW dynamically
- **_Routing to On-premise network_**
    - A public and VPN-only subnets created by the VPC Wizard refers to the fact no NAT instance(or gateway) will be
        created as part of the wizard configuration. VPN only means a subnet that does not require access to the
        internet
    - VPC's **main route table** is **associated with the VPN-only subnet(private subnet)**
    - VPC's **custom route table** is **associated with the public subnet**
    - VGW is the gateway the main table refers to for access to customer premise/data center
- **_VPC Wizard - VPN only and HW VPN_**
    - No public subnet
    - No NAT instance/gateway
    - It will create a Virtual Private Gateway(VGW) but without an elastic ip
    - It will create a VPN connection 
    
[Back to Table of Contents](#toc)

<a name ="vpc_flow_logs"></a>
# VPC Flow Logs
- A feature that enables you to capture information about the IP traffic going to and from network interfaces in your
    VPC
- Flow log data is stored using Amazon CloudWatch logs. After you have created a flow log, you can view & retrieve its
    data in Amazon CloudWatch Logs
- A Flow log can be created at either the VPC, Subnet or Network Interface level
- You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account
- you cannot tag a flow
- After you have created a flow log you cannot change its configuration; eg. you cannot associate a different IAM role
    with the flow log
- Not all IP traffic is monitored
    - Traffic generated by instances when they contact the Amazon DNS server. 
    - Traffic generated from a windows instance for Amazon windows license activation
    - Traffic to and from 169.254.169.254 for instance metadata
    - DHCP traffic
    - Traffic to the reserved IP addresses for the default VPC router      
 
[Back to Table of Contents](#toc)

<a name ="vpc_peering"></a>
# VPC Peering
- A networking connection between 2 VPCs that enable you to route traffic between them using private IPv4 addresses or 
    IPv6 addresses
- Instances in either VPC can communicate with each other as if they are within the same network
- Can create a VPC peering connection between your own VPCs, or with a VPC in another AWS account within a single region
- AWS uses existing infrastructure of a VPC to create VPC peering connection, no gateway, no VPN, and does not rely on
    separate piece of physical hardware
- No single point of failure for communication or a bandwidth bottleneck
- To establish a VPC peering connection, you do the following:
    - The owner of the requester VPC(or local VPC) sends a request to the owner of the peer VPC to create the VPC
        peering connection. The peer VPC can be owned by you, or another AWS account, and cannot have a CIDR block that
        overlaps with the requester VPC's CIDR block
    - The owner of the peer VPC accepts the VPC peering connection request to activate the VPC peering connection
    - To enable the flow of traffic between the peer VPCs using private IP addresses, add a route to one or more of your
        VPC's route table that points to the IP address range of the peer VPC. The owner of the peer VPC adds a route to
        one of their VPC route tables that points to the IP address range of your VPC
    - If required, update the security group rules that are associated with your instances to ensure that traffic to and 
        from the peer VPC is not restricted
    - A VPC peering connection is a one-to-one relationship between 2 VPCs. You can create multiple VPC peering
        connections for each VPC that you own
    - Transitive peering relationships are not supported: you do not have any peering relationship with VPCs that your
        VPC is not directly peered with
- **_ Direct Connect & VPC peering edge to edge routing_**
    - VPC peering does not support edge-to-edge routing
- **_Limitations of VPC peering_**
    - You cannot create a VPC peering connection between VPCs that have matching or overlapping IPv4 or IPv6 CIDR blocks
    - You have a limit on the number of active(50) and pending(25) VPC peering connections that you can have per VPC
    - VPC peering does not support transitive peering relationships
    - You cannot have more than 1 VPC peering connection between the same 2 VPCs at the same time
    - A placement group can span peered VPCs
    - Unicast reverse path forwarding in VPC peering connections is not supported
    

<a name ="nat_vs_bastion"></a>
# NAT vs Bastion
- A NAT is used to provide internet traffic to EC2 instances in private subnets
- A Bastion is used to securely administer EC2 instances in private subnets

[Back to Table of Contents](#toc)

# Application Services
<a name ="sqs"></a>
# Simple Queue Service(SQS)
- A web service that gives you access to a message queue that can store messages while waiting for a computer to
    process them
- A distributed queue system that enables web service apps to quickly and reliably queue messages that one component in
    the application generates to be consumed by another component
- Acts as a temporary repository for messages that are awaiting to be processed
- You can decouple the components of an application so they run independently, with SQS easing message management 
    between components
- Any component of a distributed application can store messages in a fail-safe queue
- Messages can contain up to 256KB of text in any format, any component can later retrieve the message
    programmatically using SQS API
- Acts as a buffer between the component producing and saving data, and the component receiving the data for 
    processing, this helps resolving issues where producer produces work faster than the consumer can consume, or 
    producer and consumer are only intermittently connected
- Queue types
    - **_Standard_**
        - Default queue type
        - Nearly-unlimited no.of transactions/sec
        - Guarantees that a message is delivered atleast once
        - Due to high throughput and distributed architecture, more than 1 copy of the message might be delivered out of
            order
        - Provides best-effort ordering of messages, meaning ensuring that messages are generally delivered in the same
            order as they are sent
    - **_FIFO_**
        - First-in-first-out delivery and exactly once processing
        - Order in which messages are sent and received is strictly preserved and a message is delivered once and 
            remains available until a consumer processes and deletes it
        - No duplicates introduced in the queue
        - Supports message groups that allow multiple ordered message groups within a single queue
        - limited to 300 transaction/sec, but have all capabilities of standard queues 
- SQS is pull-based not push-based
- Messages can be kept from 1 min-14days
- Default is 4 days
- Visibility timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that
    message. Provided the job is processed before the visibility timeout expires, the message will then be deleted from
    the queue. If the job is not processed within that time, the message will become visible again & another reader
    will process it, meaning same message being delivered twice
- Visibility timeout is max 12 hours and default is 30secs
- SQS guarantees that your messages will be processed at least once
- SQS long polling is  a way to retrieve messages from your queue. Short polling returns immediately, even if the
    message queue being polled is empty, long polling doesn't return a response until a message arrives in the 
    message queue, or the long poll times out

[Back to Table of Contents](#toc)

<a name ="swf"></a>
# Simple Workflow Service(SWF)
- A web service to coordinate work across distributed application components
- Several use cases such as media processing, web apps backends, business process workflows, and analytics pipelines,
    to be designed as a coordination of tasks
- Tasks represent invocations of various processing steps in an app which can be performed by executable code, web
    service calls, human actions, and scripts
- SQS has a retention period of 14 days, SWF up to 1 yr for workflow executions
- SWF is task oriented, and SQS is message oriented
- SWF ensures task is assigned  only once and never duplicates, but SQS you not only need to handle duplicate messages,
    but also need to ensure that the message is processed only once
- SWF keeps track of all the tasks and events in your application. With SQS you need to implement your own application-
    level tracking, esp. if your app uses multiple queues
- SWF Actors
    - **_Workflow starters_**
        - An application that can initiate a workflow
    - **_Deciders_**
        - Control the flow of activity tasks in a workflow execution, if something has finished in a workflow(or fails)
            a Decider decides what to do next
    - **_Activity workers_**
        - Carry out the activity tasks

[Back to Table of Contents](#toc)

<a name ="sns"></a>
# Simple Notification Service(SNS)                                   
- A web service to send notifications from the cloud
- Allows one to publish messages from one application and immediately deliver them to subscribers or other applications
- Can deliver notifications by SMS text messages or email, to SQS or any HTTP endpoint
- SNS notifications can also trigger lambda functions
- Allows you to group multiple recipients using topics. A topic is an "access point" for allowing recipients to
    dynamically subscribe for identical copies of the same notification
- One topic can support deliveries to multiple endpoint types      
- After publishing a topic, SNS deliver appropriately formatted copies of your message to each subscriber
- To prevent loss of message, all messages published to SNS are stored redundantly across multiple AZs
- This is a pub/sub model, no polling
- Inexpensive model, pay-as-you-go with no upfront costs
- simple apis and easy integration with applications
- pay $0.50 per 1 million amazon sns requests, then $0.06 per 100,000 notification deliveries over HTTP, $0.75 per 100
    notification deliveries over SMS, and $2.00 per 100,00 deliveries over email

[Back to Table of Contents](#toc)

<a name ="elastic_transcoder_svc"></a>
# Elastic Transcoder
- media based transcoder in the cloud
- convert media files from their original source format into a different formats that will play on smartphones, tablets,
    PC's etc.
- Provides transcoding presets for popular output formats, which means that you don't need to guess about which settings
    works best on particular devices 
- Pay based on the minutes that you transcode and the resolution at which you transcode

[Back to Table of Contents](#toc)

<a name ="api_gateway"></a>
# API Gateway
- A fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale
- Create API for apps to access data, business logic, or functionality from your back-end services, such as apps
    running on EC2, code running on AWS Lambda, or any web app
- Once **_API Caching_** is enabled it allows us to cache endpoint's response,
    reduce the number of calls to your endpoint,and
    help improve the latency of the requests
- When you enable caching for a stage, API gateway will cache response for a specified time-to-live(ttl) period, in secs.
    API gateway then responds to the request by looking up the endpoint response from the cache instead of making a
    request to your endpoint
- Low cost and efficient
- Scales effortlessly
- Throttle requests to prevent attacks
- connect to cloudwatch to log all requests
- **_Cross-Origin Resource Sharing_**
    - CORS is one way the server at other end can relax the same-origin policy
    - CORS is a mechanism that allows restricted resources(e.g. fonts) on a web page to be requested from another
        domain outside the domain from which the first resource was served

[Back to Table of Contents](#toc)

<a name ="kinesis"></a>
# Kinesis
- Streaming data
    - data generated continuously by thousands of data sources, which typically send in data records simultaneously, and
        in small sizes 
- Kinesis is a platform on AWS to send your streaming data too. Kinesis makes it easy to load and analyze streaming data,
    and also providing the ability for you to build your own custom applications for your business needs
    - **_Kinesis streams_**
        - consists of shards
        - data capacity for your streams is a function of the number of shards that you specify for the stream. The
            total capacity of the stream is the sum of the capacities of its shards
        - data retained for 24hrs to 1 week
    - **_Kinesis Firehose_**
        - analyze data automatically using lambda without having to worry about consumers
    - **_Kinesis Analytics_**

[Back to Table of Contents](#toc)

<a name ="overview_security_process"></a>
# Overview of Security Processes
- **_Shared responsibility model_**: 
    - AWS is responsible for Global Infrastructure but you are responsible for anything you put on the cloud
- **_IAAS_**: 
    - Amazon EC2, S3, and Amazon VPC are under your control 
- **_Managed services_**: 
    - AWS is responsible for patching, antivirus etc. But you are responsible for account management and user access 
- **_Storage decommissioning_**:
    - When a storage device has reached its end of useful life, Amazon will de-commission the resource to not expose
        consumer data
- **_Network Security_**:
    - You can connect to any AWS access point via HTTP using SSL, Amazon also offers VPC which provides a private subnet
        within the AWS cloud
- **_Amazon Corporate segregation_**:
    - Logically, the AWS production network is segregated from the Amazon Corporate network by means of a complex set
        of network security/segregation device
    - Will not permit IPSpoofing must request a vulnerability scans
- **_AWS Trusted Advisor_**:
    - Inspects your AWS environment and makes recommendations when opportunities may exist to save money,
        improve system performance, or close security gaps
- **_Instance Isolation_**:
    - Different instances running on the same physical machine are isolated from each other via Xen hypervisor,
        AWS firewall resides between the virtual interface and the physical network interface
    - The instances can be treated as if they are on separate physical hosts, and neighbors have no access to that
        instance other than any other host on the internet
- **_Guest OS_**: 
    - You have full root access over accounts, services, and applications, virtual instances controlled by you,
    - AWS does not have access rights.
    - Provides the ability to encrypt EBS volumes and their snapshots with AES-256
- **_Firewall_**:
    - Amazon EC2 provides a complete firewall solution; configured to be in a deny-all mode,
    - customers must explicitly open the ports to allow inbound traffic
- **_Elastic Load Balancing_**: 
    - SSL termination supported, allows you to identify the IP addresses of a client connecting to your servers.
- **_Direct Connect_**: Bypass ISPs in your network path. 

<a name ="exam_tips"></a>
# Additional Exam Tips

[Back to Table of Contents](#toc)

<a name ="consolidated_billing"></a>
# Consolidated Billing
- AWS Organizations
    - An account management service that enables you to consolidate multiple AWS accounts into an organization that you
        create and centrally manage
    - Available in 2 sets
        - **_Consolidated Billing_**
            - We have a paying account, and this account is linked to separate AWS accounts for example test/dev, 
                production and bank office accounts respectively.
            - Paying account is independent. It cannot access resources of other accounts. 
            - All linked accounts are independent. There is a limit of 20 linked accounts for consolidated billing
            - One bill per AWS account
            - Very easy to track charges and allocate costs
            - volume pricing discount
            - Always enable multi-factor authentication on root account
            - Always use a strong and complex password on root account
            - Paying account should be used for billing purposes only. Do not deploy resources in to paying accounts
            - Allows you to get volume discounts on all your accounts 
        - All Features

[Back to Table of Contents](#toc)

<a name ="cross_account_access"></a>
# Cross Account Access
- Makes it easy for you to work within a multi-account AWS environment by making it easy for you to switch roles within
    the AWS management console
- you can sign in to the console with username/pwd and without having to reenter login information switch the console to
    manage another AWS account

[Back to Table of Contents](#toc)
    
# Resource Groups and Tagging

<a name ="tags"></a>
## Tags
- Key value pairs attached to AWS resources
- Metadata
- Tags can be inherited

[Back to Table of Contents](#toc)

<a name ="resource_groups"></a>
## Resource Groups
- Makes it easy to group your resources using the tags assigned to them.
    You can group resources that share one or more tags
- Contain information such as: region, name, HealthChecks
- Also contain specific information for eg. for EC2 - public and private ip addresses, for ELB - port configurations 

[Back to Table of Contents](#toc)
    
<a name ="direct_connect"></a>
# Direct Connect
- Makes it easy to establish a dedicated network connection from your premises to AWS
- Makes it easy for establishing a private connection between AWS and your datacenter, office, or colocation
    environment, which in many cases an reduce your network costs, increase bandwidth throughput, and provide a more
    consistent network experience than Internet-based connections
- Reduce costs
- Increase reliability
- Increase bandwidth
- A VPN connection can be configured in minutes and are good solution for immediate need, and have low to modest
    bandwidth requirements, and can tolerate the inherent variability in internet-based connectivity
- AWS direct connect does not involve the Internet; instead it uses dedicated, private network connections between
    your intranet and Amazon VPC
- Uses Ethernet VLAN trunking(802.1Q)    
- If you don't want your traffic to traverse the internet and increase reliability, lower costs etc. then you might want 
    to use direct connect (available in 10 Gbps, 1Gbps, Sub 1 Gbps can be purchased from AWS direct connect partners),
    but if you have an immediate need for a connection between your corporate headquarters and Amazon, and you need it 
    encrypted, your best choice will be a VPN        

[Back to Table of Contents](#toc)

<a name ="sts"></a>
# Security Token Service(STS)
- Grants trusted users limited and temporary access to AWS resources
- To request temporary security credentials, use the AWS STS API actions
- Available as a global service, all requests goto https://sts.amazonaws.com
- You can optionally send your AWS STS requests to endpoints in any of the AWS regions
- Temporary security credentials are supported in all regions
- You cannot restrict the temporary security credentials to a particular region or subset of regions, except the
    temporary security credentials from AWS GovCloud(US) and China(Beijing)
- No matter which region your credentials come from they work globally
- AWS STS endpoints are active by default in all regions and you can start using them without any further actions
- When you activate a region for an account, you enable the STS endpoints in that region to issue temporary credentials
    for users and roles in that account when a request is made to an endpoint in the region
- When the credentials are created, they are associated with an IAM access control policy
- Permissions assigned to temporary security credentials are evaluated each time a request is made that uses the
    credentials
- Users can come from 3 different resources
    - Federation
        - Uses SAML(Security Assertion Markup Language)
        - Grants temporary access based off the users Active directory credentials, does not need to be a user in IAM
        - SSO allows users to log in to AWS console without assigning IAM credentials
    - Federation with mobile apps
        - Use facebook/google/Amazon or other openId providers to login
    - Cross account access
        - Lets users from one AWS account access resources in another
- Key terms
    - **_Federation_**
        - Combining or joining a list of users in one domain (such as IAM) with a list of users in another domain(such 
            as Active directory, Facebook etc.)
    - **_Identity broker_**
        - A service that allows you to take an identity from point A to point B
    - **_Identity Store_**
        - Services like Active directory, Facebook etc.
    - **_Identities_**
        - A user service like Facebook etc.

- **_STS Access_**
    - Access it via the STS API
    - Can also use SDKs containing libraries and sample code
    - Can use the AWS CLI or the Microsoft Powershell
    - Cannot generate it through AWS Console
     
- **_EC2 Roles and STS_**
    - A special type of service role that a service assumes to launch and Amazon EC2 instance that runs your app
    - Automatically provides temporary security credentials that are attached to the role and then makes them
        available for the EC2 instance
    - For cases other than AWS EC2 roles, you need to request the temporary credentials first

- **_STS API Actions_**
    - AssumeRole
        - Who can call? IAM user or user with existing temporary security credentials
    - AssumeRoleWithSAML
        - Who can call? Any user passing the SAML authentication response
    - AssumeRoleWithWebIdentity
        - Who can call? any user; caller must web identification token that indicates authentication from a known
            identity provider
    - GetSessionToken
        - Who can call? IAM user or AWS account root user
    - GetFederationToken
        - Who can call? IAM user or AWS account root user
    - Passed policy support
        - Pass the IAM policy as a parameter to most of the AWS STS APIs to be used in conjunction with other policies
            affecting the user to determine what the user is allowed to do with temporary credentials that result from
            the API call, not supported by GetSessionToken
    - MFA support
        - Include info about MFA in AssumeRole and GetSessionToken APIs
    - Default expiration of 1 hour for AssumeRole, AssumeRoleWithSAML, and AssumeRoleWithWebIdentity, and 12 hours for
        GetSessionToken, and GetFederationToken, you can send the requested duration of the token, and this can be from
        15 minutes to all the way to few hours 36 hours      

- **_Assumed Role with Web Identity API_**
    - Permission policy of the role that is being assumed determines the permissions for the temporary security
        credentials returned by and AssumeRoleWithWebIdentity
    - You can optionally pass in a separate policy to scope down the permissions assigned to the temporary security
        credentials, cannot use the polciy to grant permissions that are in excess of those allowed by the permission
        policy of the role
     
- **_Assumed Role with SAML 2.0 - AWS API_**
    - SAML is a open standard for exchanging authentication and authorization data between security domains
    - SAML 2.0 is an XML-based protocol that used security tokens containing assertions to pass information about a
        principal
    - SAML 2.0 enables web-based, cross-domain single-sign-on(SSO)
    - Using SAML AWS enables federated single sign-on, which lets users sign into the AWS management console or make
        programmatic calls to AWS API by using assertions from a SAML compliant identity provider(IdP) like ADFS
    - Enterprise federation to AWS is possible using Windows Active Directory(AD), Active Directory Federation Services
        (ADFS) 2.0, and SAML 2.0
    - You need to configure trust on AWS side, you need:
        - Create an IdP which is an XML metadata document from the IDP, that describes IdP and lists its capabilities
        - Create an IAM role which will be assumed via AssumeRoleWithSAML, or you can also redirect all requests to SAML
            sign in URL https://signin.aws.amazon.com/saml
        - On the ADFS side you need to configure trust on AWS
        -      
                          
 - Scenario 
    1. Users Login
    2. Application calls identity broker that captures the username and password
    3. Identity broker uses organization's LDAP directory to validate the employee's identity FIRST
    4. The Identity broker calls GetFederationToken using IAM creds, call includes an IAM policy and a
        duration(1-36 hours), alongwith the policy that specifies permissions granted to the temporary security credentials
    5. STS confirms the policy of the IAM user making the call gives permissions to create new token, and returns
        (access key, secret access key, a token and a duration)
    6. Broker returns the temporary security creds to the reporting application
    7. The data storage application uses the temporary security credentials(including the token) to make requests to S3
    8. S3 uses IAM to verify that the credentials allow the requested operation on the given S3 bucket and key
    9. IAM provides S3 with the go-ahead to perform the requested operation

[Back to Table of Contents](#toc)

<a name ="workspaces"></a>
# Workspaces
- A VDI, a cloud-based replacement for traditional desktop
- Available as a bundle of compute resources, storage space, and storage application access that allow a user to
    perform day-to-day tasks just like using a traditional desktop
- A user cann connect to Workspace via any supported device, using a free Amazon WorkSpaces client application and creds
    set up by the admin or their existing active directory creds
- Windows 7 experience provided by Windows Server 2008 R2
- By default users can personalize their workspaces with their favorite settings. This can be locked down by an admin
- By default you will be given a local admin access, so you can install your own applications
- Workspaces are persistent
- All data on D:\ is backed up every 12 hours
- You don't need a AWS account to login into Workspace
                                 
[Back to Table of Contents](#toc)

<a name ="ecs"></a>
# Elastic Container Service
- **_Docker_**
    - is a software platform to build, test and deploy apps quickly
    - highly reliable; quickly deploy and scale apps into any environment and know your code will run
    - infinitely scalable: running docker on AWS is a great way to run distributed applications at any scale
    - docker packages software into standardized unit called containers, containers allow you to easily package an 
        apps code, configs, and dependencies into easy to use building blocks that deliver environmental consistency,
        developer productivity, and version control
- **_Containerisation benefits_**
    - escape from dependency hell
    - consistent progression from dev -> test -> qa -> prod
    - isolation , eg: performance issues in app A, will not affect app B
    - much better resource management
    - extreme code portability
- **_Docker components_**
    - **_Docker image_**
        - A read-only template with instructions for creating a docker container
        - Contains an ordered collection of root filesystem changes and the corresponding execution parameters for use
            within a container runtime
        - An image is created from a dockerfile, a plain text file that specifies the components that are to be included
            in the container
        - Images are stored in a registry, such as DockerHub, or AWS ECR    
    - **_Docker container_**
        - are a method of operating system virtualization that allow you to run an app and its dependencies in resource-
            isolated processes
        - Holds have everything that is needed for a software to run - including libraries, system tools, code, and
            runtime
        - created from a read-only template called an image    
    - **_Layers/union file system_** 
        - Docker images are read-only templates from which docker containers are launched, and
            each image consists of a series of a layer, uses union file system to combine these layers into a
            single image 
    - **_Dockerfile_** 
        - Images built from these images using simple set of instructions, each instruction creates a new layer
            in our image, and these instructions are present in a docker file, docker reads this docker file when you
            request a build in an image and then executes instructions and returns a final image
    - **_Docker daemon / engine_** 
        - Runs on linux in order to create a operating environment for your distributed application
            the in-host daemon communicates with the docker client to execute commands to build ship and run containers
    - **_Docker client_**
        - interface between you and the dicker engine, allowing the creation, manipulation and deletion of docker
            containers, and control of the docker daemon
    - Docker registries: public/private stores of docker images
- **_ECS_**
    - A highly scalable, fast, container management service that makes it easy to run, stop, and manage docker containers
        on a cluster of EC2 instances
    - ECS lets you launch and stop container-based applications with simple API calls, allows you to get the state of
        your cluster from a centralized service, and gives you access to many familiar EC2 features
    - A regional service that you can use in 1 or more AZs across a new, or existing, VPC to schedule the placement
        of containers across your cluster based on your needs
    - Eliminates the needs for you to operate and manage your own cluster management and configuration management
        systems, or scaling of your management infrastructure
    - Can be used to create a consistent deployment and build experience, manage and scale batch and ETL workloads,
        and build sophisticated app architectures on a microservices model
    - A task definition is required to run docker containers in ECS
    - task definitions are text files in JSON format that describe 1 or more containers that form your application
    - ECS service allows you to run and maintain a specified number of instances of a task definition
        simultaneously in an ECS cluster, think of services like auto-scaling group for ECS
    - **_ECS cluster_**
        - Logical grouping of container instances that you can place tasks on, a default cluster is created  when you 
            first use ECS
        - Clusters are region-specific
        - May contain multiple different container instance types
        - Container instances can only be a part of one cluster at a time
        - Can create IAM policies for your clusters to allow or restrict users' access to specific cluster
    - **_ECS Scheduler_**
        - Services scheduler
            - ensures that specified number of tasks are constantly running and reschedules tasks when a task fails
            - ensure tasks are registered against an ELB
        - Custom scheduler
            - you can create your own schedulers that meet your business needs
            - leverage 3rd party schedulers, such as Blox
        - leverage the same cluster state information provided by the Amazon ECS API to make appropriate placement
            decisions                    
    - **_ECS Container Agent_**
        - allows container instances to connect to your cluster, it is included in the ECS-optimized ami, but you can
            install it on any EC2 instance that supports the ECS specification, only supported on EC2 instances,
            not work with windows
    - **_ECS Security_**
        - EC2 instances use an IAM role to access ECS
        - EC2 tasks use an IAM role to access services and resources
        - Security group attach at the instance-level
        - access and configure the OS of the EC2 instance in your ECS cluster

[Back to Table of Contents](#toc)
                                                     
<a name ="helpful"></a>
# Other Helpful resources to study from:
- A great talk by Rick Houlihan from Amazon, for [DynamoDb](https://www.youtube.com/watch?v=FNFRTnp9Qh4&lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3Bj8oarHCeQOCnUV5R8ajrlg%3D%3D)
- Dan-Claudiu Dragos shared his experience [here](https://www.linkedin.com/pulse/how-get-all-aws-certifications-asia-wong-chun-yin-cyrus-%E9%BB%83%E4%BF%8A%E5%BD%A5-/) 
   on how he prepared for the AWS Solutions Architect Certifications in 7 days and succesfully passed it.
-  [A curated list of AWS resources to prepare for the AWS Certifications](https://gist.github.com/leonardofed/bbf6459ad154ad5215d354f3825435dc)
- [Open Guide for AWS](https://github.com/open-guides/og-aws)
