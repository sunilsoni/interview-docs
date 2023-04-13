---
layout: default
title: CloudFormation
parent: AWS
resource: true
desc: "AWS CloudFormation interview questions and answers."
categories: [AWS CloudFormation]

---

# AWS CloudFormation
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



CloudFormation is an automation tool which automates the process of creating resources for your infrastructure in AWS. You can write YAML or JSON scripts (also called templates) where you specify details for each of your resources and their dependencies. Once the scripts get executed successfully all the resources mentioned in it will be created exactly as per provided configurations. It is important to note that In case of any failure, all the changes are rolled back.


---

## Concepts

Basic concepts are 

###  Templates

- A JSON or YAML formatted text file.
- CloudFormation uses these templates as blueprints for building your AWS resources.

###  Stacks

- Manage related resources as a single unit.
- All the resources in a stack are defined by the stack’s CloudFormation template.


###  Change Sets

- Before updating your stack and making changes to your resources, you can generate a change set, which is a summary of your proposed changes.
- Change sets allow you to see how your changes might impact your running resources, especially for critical resources, before implementing them.

<img src="images/cloudformation Stack.png" width="900"/>

- With AWS CloudFormation and AWS CodePipeline, you can use continuous delivery to automatically build and test changes to your CloudFormation templates before promoting them to production stacks.
- CloudFormation artifacts can include a stack template file, a template configuration file, or both. AWS CodePipeline uses these artifacts to work with CloudFormation stacks and change sets.

- **Stack Template File** – defines the resources that CloudFormation provisions and configures. You can use YAML or JSON-formatted templates.
- **Template Configuration File** – a JSON-formatted text file that can specify template parameter values, a stack policy, and tags. Use these configuration files to specify parameter values or a stack policy for a stack.

Through the AWS PrivateLink, you can use CloudFormation APIs inside of your Amazon VPC and route data between your VPC and CloudFormation entirely within the AWS network.

### Stacks


- If a resource cannot be created, CloudFormation rolls the stack back and automatically deletes any resources that were created. If a resource cannot be deleted, any remaining resources are retained until the stack can be successfully deleted.
- Stack update methods
  - Direct update
  - Creating and executing change sets
- Drift detection enables you to detect whether a stack’s actual configuration differs, or has drifted, from its expected configuration. Use CloudFormation to detect drift on an entire stack, or on individual resources within the stack.
  - A resource is considered to have drifted if any if its actual property values differ from the expected property values.
  - A stack is considered to have drifted if one or more of its resources have drifted.
- To share information between stacks, export a stack’s output values. Other stacks that are in the same AWS account and region can import the exported values.
- You can nest stacks.

### Templates

- Templates include several major sections. The Resources section is the only required section.
- CloudFormation Designer is a graphic tool for creating, viewing, and modifying CloudFormation templates. You can diagram your template resources using a drag-and-drop interface, and then edit their details using the integrated JSON and YAML editor.
- Custom resources enable you to write custom provisioning logic in templates that CloudFormation runs anytime you create, update (if you changed the custom resource), or delete stacks.
- Template macros enable you to perform custom processing on templates, from simple actions like find-and-replace operations to extensive transformations of entire templates.



### StackSets

- CloudFormation StackSets allow you to roll out CloudFormation stacks over multiple AWS accounts and in multiple Regions with just a couple of clicks. StackSets is commonly used together with AWS Organizations to centrally deploy and manage services in different accounts.
- Administrator and target accounts – An administrator account is the AWS account in which you create stack sets. A stack set is managed by signing in to the AWS administrator account in which it was created. A target account is the account into which you create, update, or delete one or more stacks in your stack set.
- In addition to the organization’s management account, you can delegate other administrator accounts in your AWS Organization that can create and manage stack sets with service-managed permissions for the organization.
- Stack sets – A stack set lets you create stacks in AWS accounts across regions by using a single CloudFormation template. All the resources included in each stack are defined by the stack set’s CloudFormation template. A stack set is a regional resource.
- Stack instances – A stack instance is a reference to a stack in a target account within a region. A stack instance can exist without a stack; for example, if the stack could not be created for some reason, the stack instance shows the reason for stack creation failure. A stack instance can be associated with only one stack set.
- Stack set operations – Create stack set, update stack set, delete stacks, and delete stack set.
- Tags – You can add tags during stack set creation and update operations by specifying key and value pairs.

### Monitoring

CloudFormation is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in CloudFormation. CloudTrail captures all API calls for CloudFormation as events, including calls from the CloudFormation console and from code calls to the CloudFormation APIs.


### Security

- You can use IAM with CloudFormation to control what users can do with AWS CloudFormation, such as whether they can view stack templates, create stacks, or delete stacks.
- A service role is an IAM role that allows CloudFormation to make calls to resources in a stack on your behalf. You can specify an IAM role that allows CloudFormation to create, update, or delete your stack resources.
- You can improve the security posture of your VPC by configuring CloudFormation to use an interface VPC endpoint.

### Pricing

No additional charge for CloudFormation. You pay for AWS resources created using CloudFormation in the same manner as if you created them manually.



---

## A Short Example

we will use a sample CloudFormation template and give you some details on how to configure it. The template will create two EC2 instances and RDS without any manual effort.

###  Prerequisites

You need to know the following:

- **Region ID**: ID of the region where you want the resources to be created.
- **VPC ID**: ID of the VPC inside which you want to create the resources.
- **EC2 Keypair**: Name of an already created EC2 key pair.

###  Writing the Template

You can use CloudFormation console for creating templates. Using the console, you can simply drag and drop a resource into a drawing panel and relevant code for that resource in YAML and JSON will be automatically generated for you. After this, you can modify it as per your needs. Alternately, you can always write your own script using any editor and upload it to CloudFormation. Following is a sample template in YAML.


```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: Creates two Subnets, a DBSubnetGroup, an EC2 instance and a RDS instance.
Parameters:
    KeyName:
        Description: "Name of an existing EC2 KeyPair to enable SSH access to the instance"
        Type: "AWS::EC2::KeyPair::KeyName"
        ConstraintDescription: "must be the name of an existing EC2 KeyPair"
Resources:
    mySubnet1:
        Type: "AWS::EC2::Subnet"
        Properties:
            AvailabilityZone: "us-east-1a"
            VpcId: "vpc-b93fd8c3"
            CidrBlock: "172.16.31.0/20"
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"
    mySubnet2:
        Type: "AWS::EC2::Subnet"
        Properties:
            AvailabilityZone: "us-east-1b"
            VpcId: "vpc-b93fd8c3"
            CidrBlock: "172.16.33.0/21"
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"              
    mydbsubnetgroup:
        Type: "AWS::RDS::DBSubnetGroup"
        Properties:
            DBSubnetGroupName: "dbsubnetgroup"
            DBSubnetGroupDescription: "description"
            SubnetIds:
                -   !Ref mySubnet1
                -   !Ref mySubnet2
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"  
    InstanceSecurityGroup:
        Type: "AWS::EC2::SecurityGroup"
        Properties:
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"
            VpcId: "vpc-b93fd8c3"
            GroupDescription: "Enable SSH access via port 22"
            SecurityGroupIngress:
                -
                    CidrIp: "0.0.0.0/0"
                    Description: "Allowed from anywhere"
                    FromPort: "22"
                    ToPort: "22"
                    IpProtocol: "tcp"
    EC2Instance:
        Type: "AWS::EC2::Instance"
        Properties:
            ImageId: "ami-04681a1dbd79675a5"
            InstanceType: "t2.micro"
            SecurityGroupIds:
                -
                    !GetAtt InstanceSecurityGroup.GroupId
            KeyName: !Ref KeyName
            SubnetId: !Ref mySubnet2
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"
    RDSInstance:
        Type: "AWS::RDS::DBInstance"
        Properties:
            AllocatedStorage: "100"
            DBInstanceClass: "db.t2.micro"
            Engine: "MySQL"
            Iops: "1000"
            MasterUsername: "admin"
            MasterUserPassword: "admin123"
            DBSubnetGroupName: "dbsubnetgroup"
            Tags:
                -
                    Key: "purpose"
                    Value: "CloudFormationTesting"
        DependsOn: "mydbsubnetgroup"
Outputs:
    FirstEC2InstanceId:
        Description: "Instance Id of first EC2 Instance"
        Value: !Ref EC2Instance
    RDSInstanceId:
        Description: "Instance Id of RDS Instance"
        Value: !Ref RDSInstance
```

There are four main sections in the above script.

- **Properties** — This is where you specify any external property to be used and referenced in your template. You can provide values to all of the included properties in the setup configuration of your CloudFormation job (called Stack)
- **Resources** — List of all resources that template will create
- **Output** — list of outputs to be displayed on CloudFormation console.
- **AWSTemplateFormatVersion** — CloudFormation is planning to support different versions of CloudFormation templates in future. For now, 2010-09-09 is the only version and hence the only acceptable value for this parameter.


###  Configuring CloudFormation Stack

1. Login to AWS and go to AWS CloudFormation console


<img src="images/CloudFormation Stack .png" width="900"/>


2. Select the option “Upload a template to Amazon S3” under “Choose a template”. Upload your template by selecting “Choose File”
3. Give an appropriate “Stack name” to your CloudFormation Stack and provide the name of EC2 Keypair.  Click “Next"
4. All of the input fields on this page are optional, however, you can specify a tag that will be added to all the resources your template is going to create. You can use the permissions assigned to your AWS account to be considered at the time of running of your template or alternatively you can create an IAM role and run your template using it. Either way, your account or IAM role should have the permissions to create the resources listed in your template. Also, you can create roll back alarms.  
5. Click “Next” and then click “Create.”

The execution of template will start and you can see the progress in the “Events” tab.



<img src="images/CloudFormation Events.png" width="900"/>



---

## Links
1. [An Introduction to AWS CloudFormation](https://dzone.com/articles/aws-cloudformation-getting-started-for-beginners)
2. [AWS CloudFormation](https://tutorialsdojo.com/aws-cloudformation/)