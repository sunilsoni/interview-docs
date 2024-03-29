---
layout: default
title: API Gateway
parent: AWS
resource: true
desc: " AWS API Gateway interview questions and answers."
categories: [API Gateway]

---

# AWS API Gateway
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


## API Gateway


API Gateway is a fully managed service for developers that makes it easy to build, publish, manage, and secure entire APIs. With a few clicks in the AWS Management Console, you can create an API that acts as a “front door” for applications to access data, business logic, or functionality from your back-end services, such as workloads running on EC2) code running on AWS Lambda, or any web application.

### API Gateway Key Details
- Amazon API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management.
- Amazon API Gateway has no minimum fees or startup costs. You pay only for the API calls you receive and the amount of data transferred out.
- API Gateway does the following for your APIs:
  - Exposes HTTP(S) endpoints for RESTful functionality
  - Uses serverless functionality to connect to Lambda & DynamoDB
  - Can send each API endpoint to a different target
  - Runs cheaply and efficiently
  - Scales readily and effortlessly
  - Can throttle requests to prevent attacks
  - Track and control usage via an API key
  - Can be version controlled
  - Can be connected to CloudWatch for monitoring and observability
- Since API Gateway can function with AWS Lambda, you can run your APIs and code without needing to maintain servers.
- Amazon API Gateway provides throttling at multiple levels including global and by a service call.
  - In software, a throttling process, or a throttling controller as it is sometimes called, is a process responsible for regulating the rate at which application processing is conducted, either statically or dynamically.
  - Throttling limits can be set for standard rates and bursts. For example, API owners can set a rate limit of 1,000 requests per second for a specific method in their REST APIs, and also configure Amazon API Gateway to handle a burst of 2,000 requests per second for a few seconds.
  - Amazon API Gateway tracks the number of requests per second. Any requests over the limit will receive a 429 HTTP response. The client SDKs generated by Amazon API Gateway retry calls automatically when met with this response.
- You can add caching to API calls by provisioning an Amazon API Gateway cache and specifying its size in gigabytes. The cache is provisioned for a specific stage of your APIs. This improves performance and reduces the traffic sent to your back end. Cache settings allow you to control the way the cache key is built and the time-to-live (TTL) of the data stored for each method. Amazon API Gateway also exposes management APIs that help you invalidate the cache for each stage.
- You can enable API caching for improving latency and reducing I/O for your endpoint.
- When caching for a particular API stage (version controlled version), you cache responses for a particular TTL in seconds.
- API Gateway supports AWS Certificate Manager and can make use of free TLS/SSL certificates.
- With API Gateway, there are two kinds of API calls:
  - Calls to the API Gateway API to create, modify, delete, or deploy REST APIs. These are logged in CloudTrail.
  - API calls set up by the developers to deliver their custom functionality: These are not logged in CloudTrail.

### API Gateway

Amazon Web Services (AWS) API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.

API Gateway enables developers to build RESTful APIs, WebSocket APIs, and HTTP APIs that act as a “front door” for applications to access data, business logic, or functionality from backend services. Developers can use API Gateway to create APIs that integrate with AWS Lambda, AWS Elastic Beanstalk, Amazon EC2, or any publicly accessible web service.

API Gateway provides a number of features that make it easy to manage APIs. These features include:

`API creation and management`: Developers can use the API Gateway console or API to create and manage APIs, define resources and methods, and set up authentication and authorization.

`Integration with AWS services`: API Gateway can be integrated with AWS services such as Lambda, Elastic Beanstalk, and EC2 to create a scalable and reliable backend for APIs.

`Security and access control`: API Gateway provides a number of features for securing APIs, including support for OAuth 2.0 and JSON Web Tokens (JWTs), and integration with AWS Identity and Access Management (IAM).

`Monitoring and logging`: API Gateway provides detailed metrics and logging for APIs, allowing developers to monitor API usage, identify issues, and troubleshoot problems.

`API deployment and scaling`: API Gateway makes it easy to deploy APIs to multiple stages (e.g., development, testing, production), and provides automatic scaling to handle changes in API traffic.


### Configure API using AWS API Gateway with AWS Lambda as a backend

- Create a Lambda function: First, create a Lambda function that will act as the backend for your API. You can do this using the AWS Management Console or the AWS CLI. For example, you could create a function that retrieves data from a database or performs some other business logic.

- Create an API Gateway: Next, create an API Gateway using the AWS Management Console or the AWS CLI. You'll need to define a REST API and configure its resources and methods. For example, you could define a GET method on the "/users" resource that retrieves a list of users from your Lambda function.

- Set up integration between API Gateway and Lambda: Once you've created your API Gateway, you need to set up integration between API Gateway and your Lambda function. You can do this using the AWS Management Console or the AWS CLI. For example, you could set up a Lambda Proxy integration that maps incoming requests to your Lambda function and returns the function's output to the client.

- Add security to your API: To secure your API, you can use API Gateway's built-in support for OAuth 2.0 and JSON Web Tokens (JWTs), or you can integrate with AWS Identity and Access Management (IAM) to control access to your API.

- Deploy your API: Once you've configured your API, you can deploy it to a specific stage (e.g., development, testing, production). You can do this using the AWS Management Console or the AWS CLI.

- Test your API: Finally, test your API to make sure it's working as expected. You can do this using a tool like Postman or by sending requests directly from your client application.




