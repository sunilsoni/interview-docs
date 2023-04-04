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

### Advantages


### Advantages
 ---

## Terraform