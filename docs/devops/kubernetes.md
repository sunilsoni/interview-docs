---
layout: default
title: Kubernetes
parent: DevOps
resource: true
desc: "Kubernetes interview questions and answers."
categories: [Docker]
---

# Kubernetes
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

## Kubernetes overview


Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It was developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

Kubernetes consists of several components that work together to provide a highly available and scalable platform for deploying and managing containerized applications. Here are some of the key components:

`Master Node`: The master node is the control plane of the Kubernetes cluster. It manages the overall state of the cluster and coordinates the activities of the worker nodes.

`Worker Nodes`: The worker nodes are the compute nodes of the Kubernetes cluster. They run the containerized applications and provide the compute resources needed to run those applications.

`Kubernetes API Server`: The API server is the central component of the Kubernetes control plane. It exposes the Kubernetes API, which allows users and other components to interact with the cluster.

`etcd`: etcd is a distributed key-value store that is used to store the state of the Kubernetes cluster. It is the source of truth for the entire cluster, and it is used by the Kubernetes API server to store and retrieve data.

`Kubernetes Controllers`: Kubernetes controllers are responsible for monitoring the state of the cluster and making decisions about how to handle changes. They ensure that the desired state of the cluster is maintained at all times.

`Kubernetes Scheduler`: The scheduler is responsible for assigning workloads to the worker nodes. It takes into account the resource requirements and constraints of the workloads and ensures that they are deployed in the most efficient way possible.


Using Kubernetes with AWS is a common scenario. AWS provides several ways to run Kubernetes clusters on its platform, including Amazon Elastic Kubernetes Service (EKS), which is a fully managed service that makes it easy to run Kubernetes on AWS. Here are the general steps to use Kubernetes with AWS:

Using Kubernetes with AWS is a common scenario. AWS provides several ways to run Kubernetes clusters on its platform, including Amazon Elastic Kubernetes Service (EKS), which is a fully managed service that makes it easy to run Kubernetes on AWS. Here are the general steps to use Kubernetes with AWS:

`Create an Amazon EKS cluster`: Use the AWS Management Console, AWS CLI or SDKs to create an EKS cluster in your AWS account.

`Configure kubectl`: Install and configure kubectl, the Kubernetes command-line tool, to interact with the EKS cluster.

`Deploy containerized applications`: Use kubectl or other Kubernetes deployment tools to deploy containerized applications to the EKS cluster.

`Scale and manage the cluster`: Use Kubernetes controllers and other Kubernetes management tools to scale and manage the EKS cluster.

---

## Kubernetes

