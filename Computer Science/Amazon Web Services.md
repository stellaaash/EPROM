---
tags:
  - infra
abbreviation: AWS
---
One of the leading **cloud services provider**. For better or for worse.
# Elastic Kubernetes Service (EKS)
[Official Docs](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)
An AWS-managed option for **deploying a [[Kubernetes]] cluster**. For when you want a cluster without the hastle of creating and managing a cluster yourself.
Basically, AWS handles the data plane part of your cluster: **you can easily add worker nodes to the cluster**. This is done through their intregration with [[#Elastic Compute Cloud (EC2)]] and [[#Fargate]].
It's managed using the `eksctl` CLI utility.
## Zones??
EKS has the added benefit of **high availability and scalability over multiple availability zones**.
These *zones* each run a control plane instance, which minimizes the risk of downtime for your cluster as a whole.
# Elastic Compute Cloud (EC2)
A service that **provides resizable compute capacity** in the cloud.
It's meant to deploy, manage and scale applications of any size. It includes load balancing (with Elastic Load Balancer ELB), monitoring, and auto-scaling.
You only pay for the time they run. You also pay by being basically locked in to their ecosystem after adopting it, though.
# Elastic Container Registry (ECR)
**An [[Open Container Initiative]] compliant container image registry**, fully managed by AWS.
It integrates with other services such as ECS or EKS for simple storage, managing and deploying of container images.
# Simple Storage Service (S3)
A cloud **storage service**. It provides multi-purpose storage: backup, archives, IoT, and much more.
## Buckets
Buckets are **namespaces for objects on Amazon S3**.
Each object in a bucket has a key that is unique to the object and identifies it for storage or retrieval.
