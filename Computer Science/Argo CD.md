---
tags:
  - tool/infra
---
Argo CD is **an open-source [[Kubernetes]] deployment tool**.
# Argo CD and GitOps
There are two ways to run CD on a [[Kubernetes]] cluster:
1. The standard way: GitHub actions running `kubectl apply` or `helm install` to automate your installation. Problem: **this means giving your GitHub actions access to your cluster's credentials**. Not ideal. This is called the *push model*, because you push changes into the cluster.
   That's also another drawback: **it can be easy to have a configuration drift**. Your pipelines will apply once, and then exit. If someone manually modifies something, you'll have drift: git will say something, and your cluster another.
2. The *pull model* way: instead of having CD be something external to your cluster, **you put it inside your cluster**. **This is Argo CD.**
   You point Argo to your [[Git]] repo, and it will read the state, compare it with what's actually in the cluster, and apply the difference.
   If they match, the app is *Synced*, otherwise, it's *OutOfSync*. You can configure Argo to either fix it automatically, or just show you the diff.
The second approach is called *GitOps*, since you make Git the source of truth, with the agent (Argo CD) acting on that source of truth inside of the cluster.
# Core Concepts
## Application
A CRD for a group of Kubernetes resources, so one manifest for multiple resources.
## Application Source Type
Which Tool is used to build the app.
## Target State
The desired state of the application, as represented in the Git repository.
## Live State
The current state of that application: what resources are deployed.
## Sync Status
Whether or not the live state matches the target state.
## Sync
The process of updating the live state to the target state.
It could happen, for example, but applying changes to a k8s cluster.
## Sync Operation Status
Whether or not a sync succeeded.
## Refresh
Compare the current state in Git to the live state, and figure out what is different.
## Health
The health of the app: whether it's running correctly, can server requests, etc.
## Tool
A tool to create manifests from a directory of files: [[Kustomize]], [[Helm]].
Essentially, it should take a group of files and output ready Kubernetes manifests.
# Detecting Changes
Argo CD plugs into the Kubernetes watch API for resources it manages. This way, as soon as a change is made manually, the resource will switch to OutOfSync.
# Syncing
## Manual Sync
With this, Argo CD shows OutOfSync and the diff, then wait for someone to confirm the sync.
## Auto-Sync
ArgoCD applies automatically, but only when the source of truth, Git, changes.
Your manual changes aren't applied automatically.
## Auto-Sync + Self-Heal
Like auto-sync, but will even revert live drift done manually, so you're back to the source of truth's state directly.