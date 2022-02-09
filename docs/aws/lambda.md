---
layout: default
title: Lambda
parent: Amazon Web Services (AWS)
resource: true
desc: "AWS Lambda interview questions and answers."
categories: [AWS Lambda]
---

# AWS Lambda
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

Lambda is a simple compute service that runs your code in response to certain events.
These events can be anything, from an upload operation of an object to an S3 bucket, a
record insertion in a DynamoDB table, or even some form of event triggered from your
mobile app. The idea here is simple--you simply provide your code to AWS Lambda.
Lambda will internally take care of provisioning and managing the underlying
infrastructure resources, making sure your code gets deployed successfully; even things like
your code's scalability and high availability are taken care of by Lambda itself!

---

## Key benefits of serverless computing

###  No ware to manage: 

Perhaps one of the biggest reasons for the hype about
serverless computing is the fact there is absolutely no hardware or software to
manage. The management of the serverless computing environment all the way
from the underlying hardware to the OS, to even the application's platform layer,
is managed by the cloud provider itself.

###  Faster execution time: 
Unlike your standard cloud instances, which generally
take a good minute or two to boot up, functions, on the other hand, spin up very
quickly, mostly in a matter of seconds. This could be due to the fact that the
functions are made to run on top of a containerized platform.

###  Really low costs: 
Since there is virtually no opex involved with serverless
computing, it is fairly cheap, even when compared to hosting and managing
instances in the cloud. Also, the pricing model for serverless computing is a little
different from that of your traditional cloud pricing model. Here, you are
generally billed on the duration of your function's execution and the amount of
memory it consumed during its execution period. The duration is calculated from
the time your code begins executing until it returns or otherwise terminates and
is rounded up to the nearest 100 ms.

###  Support of popular programming languages: 
Most cloud providers that provide
serverless computing frameworks today, support a variety of programming
languages, such as Java, Node.js, Python, and even C#. Azure functions allows
the use of F#, PHP, Bash, Batch and PowerShell scripts in addition to the few
mentioned.

###  Microservices compatible: 
Since serverless computing functions are small,
independent chunks of code that are designed to perform a very specific set of
roles or activities, they can be used as a delivery medium for microservices as
well. This comes as a huge advantage as compared to hosting your monolithic
applications on the cloud, which do not scale that effectively.

###  Event-driven applications: 
Serverless functions are an ideal choice for designing
and running event-driven applications that react to certain events and take some
action against them. For example, an image upload operation to a cloud storage
triggers a function that creates associated thumbnail images for the same.

There are a few cons to serverless computing as well that you should be aware of before we proceed further:

---

## Cons or Disadvantage  of serverless computing

###  Execution duration: 
Serverless functions are designed to run for short durations
of time, ideally somewhere under 300 seconds only. This is a hard limit set by
most cloud providers, however, there are a few workarounds to this as well.
Stateless: Serverless functions are purely stateless, which means that once the
function completes its execution or is terminated for some reason, it won't store
any data locally on its disk.

###  Complexity: 
The smaller you make things, the more complex it's going to
become. Although writing functions that perform very particular tasks is a good
idea, it can cause complexity issues when you view your application as a whole
system. A simple example can break one large application into some ten different
functions such that each perform a specific task. Now you need to manage ten
different entities rather than just one. Imagine if you had a thousand functions
instead.

###  Lack of tools: 
Although serverless computing is all at its hype, it still doesn't
provide a lot of out-of-the-box tools for management, deployment, and even
monitoring. Most of your monitoring tools that you use today were designed for
long-running, complex applications; not for simple functions that execute in a
mere seconds.

###  Vendor lock-in: 
With each cloud provider providing its own unique tool sets and
services around serverless computing, you often tend to get tied down to a
particular vendor. This means that you cannot change your cloud provider
without making some changes to your functions as well.

---


##  Lambda function

 <img src="images/lambda.png" width="1000" />

Reference : https://aws.amazon.com/lambda/

AWS supports Java, Python, Node.js, and even C# as programming languages for your functions.
Each function can be invoked either on demand or invoked dynamically based on certain types of supported events. 

A few event examples are listed out as follows:

**Amazon S3**: Lambda functions can be triggered when an object is created, updated, or deleted in an S3 bucket

**Amazon DynamoDB**: Lambda functions are triggered when any updates are made to a particular DynamoDB table, such as row insertion, deletion, and so on

**Amazon Simple Notification Service (SNS)**: Trigger a Lambda function when a message is published on a, SNS topic

**Amazon CloudWatch Logs**: Use Lambda functions to process CloudWatch Logs as feeds

**Scheduled events**: Run Lambda functions as scheduled events, just like a cron job

**AWS CodeCommit**: Execute Lambda functions whenever new code is pushed to an existing branch, and so on


---


## The Lambda programming model

So far we have seen that certain applications can be broken down into one or more simple
nuggets of code called as functions and uploaded to AWS Lambda for execution. Lambda
then takes care of provisioning the necessary resources to run your function along with
other management activities such as auto-scaling of your functions, their availability, and so
on. So what exactly are we supposed to do in all this? A developer basically has three tasks
to perform when it comes to working with Lambda--writing the code, packaging it for
deployment, and finally monitoring its execution and fine-tuning.

Currently, AWS officially supports Node.js, Java, Python, and C# as
the programming languages for writing Lambda functions, with each language following a
generic programming pattern that comprises of the following concepts.

### AWS SAM CLI Installation

AWS SAM provides you with a command line tool, the AWS SAM CLI, that makes it easy for you to create and manage serverless applications. You need to install and configure a few things in order to use the AWS SAM CLI.

Follow these steps to install and configure the prerequisites for using the AWS SAM command line interface (CLI) on your macOS host:

- Create an AWS account.
- Configure AWS Identity and Access Management (IAM) permissions and AWS credentials.
- Install Docker. Note: Docker is a prerequisite only for testing your application locally or using the --use-container option
- Install Homebrew.

Install the AWS SAM CLI.

https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html


### Creating Your First Java Lambda Project

First, go to a terminal and run the following command:

> $ sam init --location gh:symphoniacloud/sam-init-HelloWorldLambdaJava

This will ask you for a project_name value, and for now just hit Enter to use the  default.

The command will then generate a project directory. Change into that directory, and take a look. You’ll see the following files:

**README.md**
Some instructions on how to build and deploy the project

**pom.xml**
A Maven project file

**template.yaml**
A SAM template file—used for deploying the project to AWS

**src/main/java/book/HelloWorld.java**
    The source code for a Lambda function

If you’re using Jetbrains IntelliJ IDEA, you can do that by running the following:

> $ idea pom.xml

Within the pom.xml file itself, change the <groupId> to be more appropriate for yourself,
if you’d like.

```java
package book;
public class HelloWorld {
    public String handler(String s) {
        return "Hello, " + s;
    }
}
```

This class represents an entire Java Lambda function. Small, isn’t it? Don’t worry too
much about the whats and whys; we’ll get to them before too long. For now, let’s build
our Lambda deployment artifact.

### Building Hello World

run mvn package

This
should complete successfully with the following lines near the end:

```log
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

It should also create our uberjar. Run jar tf target/lambda.jar to list the contents
of the JAR file. The output should include book/HelloWorld.class, which is our
application code, embedded within the artifact.

---

## Core Concepts: Runtime Model, Invocation

 <img src="images/The%20Lambda%20execution%20environment.png" width="1000" />

### The Lambda Execution Environment

A function is executed, or invoked, whenever the invoke command of the AWS Lambda API is called. This happens at the following times:

- When a function is triggered by an event source
- When you use the test harness in the web console
- When you call the Lambda API invoke command yourself, typically via the CLI  or SDK, from your own code or scripts

- Invoking a function for the first time will start the following chain of activity that will
end in your code being executed.

First, the Lambda service will create a host Linux environment—a lightweight microvirtual
machine. You typically won’t need to worry about the precise nature of what
type of environment it is (which kernel, what distribution, etc.), but if you do care,
Amazon makes that information public. But don’t rely on it staying constant—Amazon
can and does make frequent changes to the OS of Lambda functions, often for
your own benefit, including automatic security patches.

Once the host environment has been created, then Lambda will start a language runtime
within it—in our case a Java virtual machine. At the time of this writing, the
JVM version will always be Java 8 or Java 11. You must supply Lambda with code
compatible with the version of Java that you choose. The JVM is started with a set of
environment flags that we can’t change.
    
Of course, the Lambda Java Runtime’s primary concern is executing our code. The
final steps of the invocation chain are (a) to load our Java classes and (b) to call the
handler method that we specified during deployment.

### Invocation Types

At a high level, Lambda functions can be invoked using the following:
- A push
- An event
- A stream-based model

AWS CLI for calling Lambda functions

> aws lambda invoke.

template.yaml : 

```yaml
AWSTemplateFormatVersion: 2010-09-09
Transform: AWS::Serverless-2016-10-31
Description: HelloWorldLambdaJava

Resources:

  HelloWorldLambda:
    Type: AWS::Serverless::Function
    Properties:
      Runtime: java8
      MemorySize: 512
      Handler: book.HelloWorld::handler
      CodeUri: target/lambda.jar

```

Run the `sam deploy` command If you go back to the Lambda console, you’ll see your strangely named Java function has now been renamed to HelloWorldJava


Let’s get back to invocation. From the terminal, run the following command:

```cmd
$ aws lambda invoke \
--invocation-type RequestResponse \
--function-name HelloWorldJava \
--payload \"world\" outputfile.txt
```

This should return the following:


```json
{
"StatusCode": 200,
"ExecutedVersion": "$LATEST"
}
```

You can also see what the Lambda function returned by executing the following:

```log
$ cat outputfile.txt && echo
"Hello, world"
```

### Lambda Function Method Signatures

Valid Java Lambda methods must fit one of the following four signatures:

• output-type handler-name(input-type input)
• output-type handler-name(input-type input, Context context)
• void handler-name(InputStream is, OutputStream os)
• void handler-name(InputStream is, OutputStream os, Context context)

**where:**
• output-type can be void, a Java primitive, or a JSON-serializable type.
• input-type is a Java primitive, or a JSON-serializable type.
• Context refers to com.amazonaws.services.lambda.runtime.Context (we describe this more later in the chapter).
• InputStream and OutputStream refer to the types with those names in the java.io package.
• handler-name can be any valid Java method name, and we refer to it in our application’s configuration.

Java Lambda methods can be either instance methods or static methods, but must be public.

A class containing a Lambda function cannot be abstract and must have a noargument  constructor—either the default constructor (i.e., no constructor specified) or an explicit no-argument constructor. The main reason to consider using a constructor at all is for caching data between Lambda calls.

---

## A Basic AWS Lambda Example With Java


### Maven Dependencies
```xml
<dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-lambda-java-core</artifactId>
    <version>1.1.0</version>
</dependency>

```

We also need the Maven Shade Plugin to build the lambda application:


```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>2.4.3</version>
    <configuration>
        <createDependencyReducedPom>false</createDependencyReducedPom>
    </configuration>
    <executions>
        <execution>
            <phase>package</phase>
	    <goals>
                <goal>shade</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```


### Create Handler
Simply put, to invoke a lambda function, we need to specify a handler; there are 3 ways of creating a handler:

1. Creating a custom MethodHandler
2. Implementing the RequestHandler interface
3. Implementing the RequestStreamHandler interface

####  Custom MethodHandler
We'll create a handler method that will be the entry point for incoming requests. We can use JSON format or primitive data types as input values.

Also, the optional Context object will allow us to access useful information available within the Lambda execution environment:

```java
public class LambdaMethodHandler {
    public String handleRequest(String input, Context context) {
        context.getLogger().log("Input: " + input);
        return "Hello World - " + input;
    }
}

```
####  RequestHandler Interface 
We can also implement the RequestHandler into our class and override the handleRequest method which will be our entry point for requests:
```java
public class LambdaRequestHandler
  implements RequestHandler<String, String> {
    public String handleRequest(String input, Context context) {
        context.getLogger().log("Input: " + input);
        return "Hello World - " + input;
    }
}
```
In this case, the input will be the same as in the first example.



####  RequestStreamHandler Interface
We can also implement RequestStreamHandler in our class and simply override the handleRequest method.

The difference is that InputStream, ObjectStream and Context objects are being passed as parameters:

```java
public class LambdaRequestStreamHandler
  implements RequestStreamHandler {
    public void handleRequest(InputStream inputStream, 
      OutputStream outputStream, Context context) {
        String input = IOUtils.toString(inputStream, "UTF-8");
        outputStream.write(("Hello World - " + input).getBytes());
    }
}
```

### Build Deployment File
With everything configured, we can create the deployment file by simply running:


```cmd
mvn clean package shade:shade
```
The jar file will be created under the target folder.


### Create Lambda Function via Management Console

Sign in to AWS Amazon and then click on Lambda under services. This page will show the lambda functions list, which is already created.

Here are the steps required to create our lambda:

1. `Select blueprint` and then select `Blank Function`
2. “Configure triggers” (in our case we don't have any triggers or events)
3. “Configure function”:
- Name: Provide MethodHandlerLambda,
- Description: Anything that describes our lambda function
- Runtime: Select java8
- Code Entry Type and Function Package: Select “Upload a .ZIP and Jar file” and click on “Upload” button. Select the file which contains lambda code.
- Under Lambda function handler and role:
  Handler name: Provide lambda function handler name com.baeldung.MethodHandlerLambda::handleRequest
  Role name: If any other AWS resources are used in lambda function, then provide access by creating/using existing role and also define the policy template.
- Under Advanced settings:
  Memory: Provide memory that will be used by our lambda function.
  Timeout: Select a time for execution of lambda function for each request.
4. Once you are done with all inputs, click “Next” which will show you to review the configuration.
5. Once a review is completed, click on “Create Function”.


### Invoke the Function

Once the AWS lambda function is created, we'll test it by passing in some data:

- Click on your lambda function from lists and then click on “Test” button
- A popup window will appear which contains dummy value for sending data. Override the data with “Interview Docs”
- Click on “Save and test” button
- 
On the screen, you can see the Execution result section with successfully returned output as:

> "Hello World - Interview Docs"


---

## How AWS Lambda Works?


 <img src="images/How%20AWS%20Lambda%20Works.png" width="1000" />

**Step 1** − Upload AWS lambda code in any of languages AWS lambda supports, that is NodeJS, Java, Python, C# and Go.

**Step 2** − These are few AWS services on which AWS lambda can be triggered.

**Step 3** − AWS Lambda which has the upload code and the event details on which the trigger has occurred. For example, event from Amazon S3, Amazon API Gateway, Dynamo dB, Amazon SNS, Amazon Kinesis, CloudFront, Amazon SES, CloudTrail, mobile app etc.

**Step 4** − Executes AWS Lambda Code only when triggered by AWS services under the scenarios such as −

   - User uploads files in S3 bucket
   - http get/post endpoint URL is hit
   - data is added/updated/deleted in dynamo dB tables
   - push notification
   - data streams collection
   - hosting of website
   - email sending
   - mobile app, etc.

**Step 5** − Remember that AWS charges only when the AWS lambda code executes, and not otherwise.

---

## Events that Trigger AWS Lambda
The events can trigger AWS Lambda are as follows −

- Entry into a S3 object
- Insertion, updation and deletion of data in Dynamo DB table
- Push notifications from SNS
- GET/POST calls to API Gateway
- Headers modification at viewer or origin request/response in CloudFront
- Log entries in AWS Kinesis data stream
- Log history in CloudTrail

AWS Lambda is a compute service mainly used to run background processes. It can trigger when used with other AWS services. The list of AWS services where we can use AWS Lambda is given below −

### S3 Object and AWS Lambda
Amazon S3 passes the event details to AWS Lambda when there is any file upload in S3. The details of the file upload or deletion of file or moving of file is passed to the AWS Lambda. The code in AWS Lambda can take the necessary step for when it receives the event details. For Example creating thumbnail of the image inserted into S3.

### DynamoDB and AWS Lambda
DynamoDB can trigger AWS Lambda when there is data added, updated and deleted in the table. AWS Lambda event has all the details of the AWS DynamoDB table about the insert /update or delete.

### API Gateway and AWS Lambda
API Gateway can trigger AWS Lambda on GET/POST methods. We can create a form and share details with API Gateway endpoint and use it with AWS Lambda for further processing, for Example, making an entry of the data in DynamoDB table.

### SNS and AWS Lambda
SNS is used for push notification, sending SMS etc. We can trigger AWS lambda when there is any push notification happening in SNS. We can also send SMS to the phone number from AWS Lambda when it receives the trigger.

### Scheduled Events and AWS Lambda
Scheduled Events can be used for cron jobs. It can trigger AWS Lambda to carry out the task at regular time pattern.

### CloudTrail and AWS Lambda
CloudTrail can be helpful in monitoring the logs on the account. We can use AWS Lambda to further process the CloudTrail logs .

### Kinesis and AWS Lambda
Kinesis is used to capture/store real time tracking data coming from website clicks, logs, social media feeds and a trigger to AWS Lambda can do additional processing on this logs.

### CloudFront and Lambda@Edge
CloudFront is a content delivery network where you can host your website and Lambda@Edge can be used to process the headers coming from viewer request, origin request, origin response and viewer response. The headers modification includes tasks such as modifying cookie data, URL rewrite, used for AB testing to change the response send to the user back, adding extra headers info for security purpose etc.



---

## More Details: 
1. [How to create a Lambda function](https://www.javatpoint.com/aws-creating-a-lambda)
2. [AWS Lambda – Overview](https://www.tutorialspoint.com/aws_lambda/aws_lambda_overview.htm)
3. [A Basic AWS Lambda Example With Java](https://www.baeldung.com/java-aws-lambda)
