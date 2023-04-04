---
layout: default
title: Terraform
parent: DevOps
resource: true
desc: "Kubernetes interview questions and answers."
categories: [Terraform]
---

# Terraform
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

## Terraform overview

HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features.

A DSL called "HCL" (Hashicorp Configuration Language). A declarative language for defining infrastructure.


Terraform is an open-source infrastructure as code (IAC) tool that enables developers and IT professionals to manage and provision cloud infrastructure resources. With Terraform, you can write code that describes the desired state of your infrastructure, and Terraform will automatically create or modify the resources to match that state.

Terraform supports a wide variety of cloud providers, including Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), and many others. It also supports on-premises infrastructure, such as VMware vSphere.

The main advantages of using Terraform are:

1. Infrastructure as Code: Terraform allows you to manage your infrastructure as code, which means you can version control it, collaborate with other developers, and automate deployments.
2. Multi-Cloud Support: Terraform is cloud-agnostic and supports a wide variety of cloud providers, making it easy to manage and provision resources across multiple clouds.
3. Consistent Infrastructure: Terraform helps ensure consistency in your infrastructure by enabling you to define it using code. This makes it easier to ensure that your infrastructure is always up-to-date and configured correctly.
4. Resource Management: Terraform provides a unified view of your infrastructure and resources, making it easier to manage and provision resources across multiple cloud providers.


### Advantages in using Terraform or IaC in general?

1. Full automation: In the past, resource creation, modification and removal were handled manually or by using a set of tooling. With Terraform or other IaC technologies, you manage the full lifecycle in an automated fashion.
2. Modular and Reusable: Code that you write for certain purposes can be used and assembled in different ways. You can write code to create resources on a public cloud and it can be shared with other teams who can also use it in their account on the same (or different) cloud>
3. Improved testing: Concepts like CI can be easily applied on IaC based projects and code snippets. This allow you to test and verify operations beforehand


### Terraform Features

1. Declarative: Terraform uses the declarative approach (rather than the procedural one) in order to define end-status of the resources
2. No agents: as opposed to other technologies (e.g. Puppet) where you use a model of agent and server, with Terraform you use the different APIs (of clouds, services, etc.) to perform the operations
3. Community: Terraform has strong community who constantly publishes modules and fixes when needed. This ensures there is good modules maintenance and users can get support quite quickly at any point
 

### Terraform workflow?

1. Write Terraform definitions: .tf files written in HCL that described the desired infrastructure state (and run terraform init at the very beginning)
2. Review: With command such as terraform plan you can get a glance at what Terraform will perform with the written definitions
3. Apply definitions: With the command terraform apply Terraform will apply the given definitions, by adding, modifying or removing the resources

This is a manual process. Most of the time this is automated so user submits a PR/MR to propose terraform changes, there is a process to test these changes and once merged they are applied (terraform apply).

###  use cases for using Terraform

1. Infra provisioning and management: You need to automated or code your infra so you are able to test it easily, apply it and make any changes necessary.
2. Multi-cloud environment: You manage infrastructure on different clouds, but looking for a consistent way to do it across the clouds
3. Consistent environments: You manage environments such as test, production, staging, ... and looking for a way to have them consistent so any modification in one of them, applies to other environments as well

### difference between Terraform and technologies such as Ansible, Puppet, Chef, etc.

Terraform is considered to be an IaC technology. It's used for provisioning resources, for managing infrastructure on different platforms.

Ansible, Puppet and Chef are Configuration Management technologies. They are used once there is an instance running and you would like to apply some configuration on it like installing an application, applying security policy, etc.

To be clear, CM tools can be used to provision resources so in the end goal of having infrastructure, both Terraform and something like Ansible, can achieve the same result. The difference is in the how. Ansible doesn't saves the state of resources, it doesn't know how many instances there are in your environment as opposed to Terraform. At the same time while Terraform can perform configuration management tasks, it has less modules support for that specific goal and it doesn't track the task execution state as Ansible. The differences are there and it's most of the time recommended to mix the technologies, so Terraform used for managing infrastructure and CM technologies used for configuration on top of that infrastructure.

### Terraform module

A Terraform module is a reusable piece of infrastructure code that encapsulates a set of resources and configurations that can be used across multiple Terraform configurations. In other words, a module is a collection of Terraform resources and their associated configurations that can be used as a single unit.

A Terraform module is typically used to abstract away common infrastructure patterns or to represent a higher-level concept that consists of multiple resources. For example, a module could represent a web server or a database cluster, and it could contain all of the resources needed to create and configure that infrastructure.

Modules can be written in any language that Terraform supports, and they can be shared and reused by others. By using modules, you can reduce duplication of code and configurations across your infrastructure, increase your code reuse, and make your infrastructure code more modular and maintainable.

Terraform has a module registry that allows you to discover and use community-maintained modules or publish your own modules for others to use. You can also store modules in version control systems like Git or use them from local directories.

In summary, a Terraform module is a reusable piece of infrastructure code that enables you to abstract away common infrastructure patterns or represent higher-level concepts that consist of multiple resources, making your infrastructure code more modular, reusable, and maintainable.


### Terraform CLI commands

Here are some of the most commonly used Terraform CLI commands:

- terraform init: Initializes a new Terraform working directory by downloading and installing the necessary providers and modules specified in your configuration files.

- terraform plan: Generates an execution plan for your Terraform configuration, showing what changes will be made to your infrastructure resources when you apply the configuration.

- terraform apply: Applies the changes specified in your Terraform configuration to your infrastructure, creating or updating the necessary resources.

- terraform destroy: Destroys all resources created by your Terraform configuration.

- terraform validate: Validates the syntax and configuration of your Terraform files.

- terraform state: Displays the current state of your Terraform-managed resources.

- terraform output: Prints the values of output variables from your Terraform configuration.

- terraform graph: Generates a visual representation of the Terraform resources and their dependencies.

- terraform import: Imports existing infrastructure resources into your Terraform state.

- terraform taint: Manually marks a resource as tainted, forcing it to be destroyed and recreated on the next terraform apply.

- terraform  workspace: Manages Terraform workspaces, which are used to create multiple instances of the same configuration in parallel.

- terraform output: Displays the values of output variables defined in your Terraform configuration.

- terraform providers: Lists the available providers and their versions in your Terraform environment.

- terraform fmt: Formats your Terraform configuration files to follow the standard format.

- terraform show: Displays a detailed summary of the current state of your infrastructure.

- `terraform refresh`: Updates the state file of your Terraform-managed resources to match the current state of your infrastructure.

- `terraform state list`: Lists all resources currently tracked in the Terraform state file.

- `terraform state mv`: Moves a resource in the Terraform state file from one address to another.

- `terraform import`: Imports an existing resource into the Terraform state file.

- `terraform version`: Displays the current version of Terraform.



### How does Terraform manage state?

Terraform uses a state file to keep track of the resources it manages. This state file is a JSON-formatted file that describes the current state of your infrastructure, including the resources that have been created, modified, or destroyed.

When you run a Terraform command that modifies your infrastructure, such as terraform apply, Terraform reads the current state file, determines what changes need to be made to match your desired configuration, and then updates the state file with the new state of your infrastructure after the changes have been applied.

The state file is crucial to Terraform's functionality because it allows Terraform to track changes to your infrastructure over time and to determine which changes need to be applied to bring your infrastructure into the desired state.

By default, Terraform stores the state file locally on the machine running Terraform. However, in a team environment or when working with multiple machines, it's recommended to store the state file remotely, such as in a version control system, an S3 bucket, or a Terraform backend.

Terraform supports several types of backends for storing the state file, including Amazon S3, Azure Blob Storage, Google Cloud Storage, HashiCorp Consul, and more. Using a remote backend enables multiple users to share the same state file, collaborate on the same infrastructure, and allows for better security, versioning, and disaster recovery.

In summary, Terraform manages state by using a state file that tracks the current state of your infrastructure, and updates it whenever changes are made. The state file is important for tracking changes, determining what needs to be applied to your infrastructure, and keeping your infrastructure in the desired state. Storing the state file remotely is recommended for collaboration and better infrastructure management.


### What is a provider in Terraform?

In Terraform, a provider is a plugin that provides Terraform with the ability to manage resources for a particular cloud or service provider. A provider typically includes a set of resource types that represent the different types of infrastructure resources that can be created, modified, or deleted in that provider.

Terraform providers are responsible for translating Terraform configuration files into API requests that interact with the cloud provider's infrastructure. When you create a resource in your Terraform configuration, such as an AWS EC2 instance, Terraform communicates with the AWS provider to create the instance using the AWS API.

Each provider has its own set of resources and data sources, which are defined in separate Terraform configuration files. Providers are typically distributed as plugins that can be installed and configured in Terraform, and can be versioned and updated independently of Terraform.

Terraform supports a wide range of providers for popular cloud and service providers, including AWS, Azure, Google Cloud, DigitalOcean, and many others. You can also create your own custom providers if you need to manage resources that are not supported by an existing provider.

In summary, a provider is a plugin that enables Terraform to interact with a cloud or service provider's infrastructure, and provides a set of resource types that can be managed using Terraform. Providers are essential to Terraform's functionality, as they allow you to define and manage infrastructure resources across multiple providers in a unified and consistent way.

###  How can you ensure that Terraform is applying changes in the correct order?

Terraform automatically determines the correct order in which to apply changes to your infrastructure by analyzing the dependencies between resources. This is known as the dependency graph.

Terraform constructs a dependency graph based on the resource definitions in your Terraform configuration, and uses this graph to determine the order in which resources should be created or modified to ensure that dependencies are satisfied. The dependency graph takes into account the relationships between resources defined by depends_on, as well as any implicit dependencies inferred from resource types and their properties.

However, there may be cases where Terraform needs guidance to ensure that changes are applied in the correct order. For example, you may have a resource that needs to be created before another resource can be created or modified.

In such cases, you can use the depends_on argument to explicitly define the order in which resources should be created or modified. You can use the depends_on argument to specify a list of resources that a given resource depends on, and Terraform will ensure that those resources are created or modified before the dependent resource.

Another way to ensure that Terraform applies changes in the correct order is to use Terraform modules. Modules allow you to encapsulate a set of related resources and dependencies into a single reusable component. When you use a module, Terraform will apply the resources in the correct order specified by the module's dependencies.

In summary, Terraform automatically determines the order in which changes should be applied based on the dependency graph. You can use the depends_on argument to explicitly specify dependencies between resources, and use modules to encapsulate resources and their dependencies into a single reusable component.

 


### How do you manage sensitive data in Terraform?

Managing sensitive data in Terraform is an important aspect of infrastructure management. Terraform provides several options for managing sensitive data in a secure and reliable manner.

One approach to managing sensitive data is to use input variables to store sensitive information, such as passwords, access keys, and secrets. Input variables are defined in a separate file or via environment variables and can be referenced in your Terraform configuration. You can use sensitive input variables to mark certain variables as sensitive, which hides their values in Terraform output, logs, and state files.

Another approach is to use data sources to retrieve sensitive information from external sources, such as key management services, secrets stores, or configuration management tools. Terraform data sources allow you to retrieve information from external sources and use it in your configuration. You can use data sources to retrieve sensitive information without storing it in your configuration files or state files.

Terraform also supports encrypted state storage, which allows you to encrypt your state file using a key stored in an external key management service. This ensures that sensitive information in the state file is protected from unauthorized access.

In addition, you can use Terraform's remote backend to store the state file in a secure and remote location, such as an S3 bucket, Azure Blob Storage, or Google Cloud Storage. Remote backend provides additional security and reliability features, such as versioning, locking, and audit logging.

Lastly, you can use third-party tools, such as Vault by HashiCorp, to manage secrets and sensitive data. Vault provides a secure and centralized way to manage secrets and access tokens, and integrates with Terraform using the Vault provider.

In summary, Terraform provides several options for managing sensitive data, including input variables, data sources, encrypted state storage, remote backend, and third-party tools like Vault. It's important to carefully manage sensitive data in Terraform to ensure the security and reliability of your infrastructure.

### Test




 ---

## Terraform