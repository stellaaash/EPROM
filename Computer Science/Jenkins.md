---
tags:
  - tool/infra
---
Jenkins is an **automation server that can be used for all sorts of tasks: building, testing, and CI/CD of software**.
# Pipelines
Pipelines is the standout feature of Jenkins, **a suite of plugins which support integrating Continuous Delivery (CD) pipelines into Jenkins**.
Jenkins abstracts those pipelines into "code", more precisely `Jenkinsfile`s ([[Groovy]] syntax), which can easily be checked into source control.
You can technicalluy define Pipelines in the web UI, but it's **best practice to define Pipelines in Jenkinsfiles and check them into source control**.
## Declarative Vs Scripted
Jenkinsfiles have two syntax flavors: declarative or scripted.
The one you choose changes the structure of your Pipeline at a fundamental level: declarative makes writing and reading Pipeline code easier, and provides more syntactical stuff over scripted syntax.
In practice, however, **most *steps* written in a Jenkinsfile are common to both syntax styles**.
## Pipeline Concepts
### Pipeline
A **user-defined model of a Continuous Delivery pipeline**. Its code defines the entire build process, including stages for building the app, testing it, and then delivering it.
### Node
A node is a **machine** which is part of the Jenkins environment and is **capable of executing a Pipeline**.
### Stage
A stage defines a **conceptually distinct group of tasks performed through the Pipeline**.
These are used by many plugins to visualize or present that progress and status of your Pipeline.
### Step
A single task, telling Jenkins **what to do at a particular point in time (step in the process)**.
For example, launching a command with `sh 'command'`.
# Resources
- [Jenkins Website](https://www.jenkins.io)