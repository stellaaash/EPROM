---
tags:
  - tool/infra
---
Helm helps to manage [[Kubernetes]] applications. It's basically the **package manager for k8s**.
# Capabilities
- **Install and manage applications**: deploy an entire app from a single chart instead of managing manifests yourself.
- **Package and share your own applications**: bundle your Kubernetes resources in a charrt, version it, and easily distribute it to the community.
- **Configure applications per environment**: give different values to the same chart to deploy to dev, staging and prod. No duplicating manifests.
- **Upgrade and rollback safely**: move a release to a new version, and easily return to the previous one if it doesn't work.
- **Manage dependencies**: declare the other charts your app depends on, and Helm will install them together.
# Components
## Charts? Are we building something?
Helm Charts help you **define, install, and upgrade Kubernetes applications, even complex ones**.
When you build a Kubernetes application, you have to manage multiple different manifests for deployments, services, configmaps, and more.
Helm charts aim to **package those manifests into a single unit called a *chart*, which is easier to version, share, install, and roll back**.
## Repositories
A repository is the **place where charts are collected and shared**. Just like packages, if you will.
Repositories are **simple HTTP servers** which serve YAML and tar files from GET requests.
One requirement for a repo is that it **has to serve a `index.yaml` file containing a list of all available packages**. It also includes some metadata for retrieving and verifying those packages.
## Releases
A release is **an instance of a chart running in a Kubernetes cluster**. You can install one chart multiple times in the same cluster, and each installation creates a new release with its own release name.
To create a release, **Helm merges a packaged hart with configuration information**, typically values in a [[YAML]] file.
# Templates
Helm Chart templates are written in the [[Go]] template language, with some stuff from the [[Spring]] library.
The idea is that **templates, when reconciled with values, create valid Kuberenetes resource manifests**. This process is known as *rendering* the chart.
## What's This About a Dot?
The dot is an object that gets updated as the template engine renders a template. It starts with the values passed through `values.yaml` or `-f`, and can be updated with some more info depending on the state in your template, including but not limited to `with`, `range` and others.
# Helm and OCI
Helm has support for [[Open Container Initiative]] registries; which means you can **store Helm charts in the same repo as container images**.
If you use `oci://` in a helm command, it means that you're going to fetch a chart off of an OCI repository. No `index.yaml` here as with normal repos.
That also means **you can't just `helm repo add oci://`**, it won't work since the `index.yaml` file won't exist. You need to already know the chart's path from the registry UI or CLI.
Instead, **you use `helm registry login` to login to the registry (lol)**.
This is great because it means you'll get your container images and Helm charts in the same registry.
# Resources
- [Helm Website](https://helm.sh)
- [Helm CheatSheet](https://helm.sh/docs/intro/CheatSheet)