---
tags:
  - tool/infra
abbreviation: k8s
---
Kubernetes is an **open source platform for the management of containers, their workloads and services**. It aims to facilitate configuration and automation, and has an extensive, still growing ecosystem.
# `kubectl` Cheat Sheet
## Information Gathering
```bash
# Get all information 
kubectl get all
# Create a watcher to see changes in real-time
watch kubectl get all

# Get details about a resource type, or a specific resource if both arguments are provided
kubectl describe <resource-type> <resource-name>
```
## Pod
```bash
# Launch a single pod using an image
kubectl run <pod-name> <image>

kubectl delete pods <pod-1> <pod-2> ...
```
## Service
```bash
kubectl create service <service-type> <service-name> <options>
```
## Deployment
```bash
kubectl create deployment <deployment-name> --image=<image>

# Scale a deployment to a certain numbers of identical pods
kubectl scale deployment <deployment-name> --replicas=<number>

# Change the image for a deployment
kubectl set image deployment <deployment-name> <deployment-name>=<image>
# Watch the status of your rollout
kubectl rollout status deploy/<deployment-name>
```
## Configuration
```bash
# List all available contexts
kubectl config get-contexts
# Switch namespaces
kubectl config set-context --current --namespace=<namespace>
```
# Concepts
## Isn't Docker Sufficient?
Containers are great, sure. They help you run your applications in simple, reproducible environments.
Think of an enterprise context, though. **Launching containers is fine, but what if one goes down?** Wouldn't it be better to have a dedicated tool than to use a bash script, or a simple `restart: unless-stopped`?
Kubernetes aims to fill this gap, by **providing a framework to run distributed systems with resilience. It takes care of scaling, and failover for your application.**
### What k8s brings to the Table
- **Service discovery and load balancing**: k8s can expose a container using a DNS name or its own [[IP Address]].
- **Storage orchestration**: k8s allows you to automatically mount a storage system of your choice, like local storage, public cloud providers, and more.
- **Automated rollouts and rollbacks**: you describe your app's desired state using k8s, and it then changes the current state to what you want, at a controlled rate. For example, you can tell k8s to create new containers, remove existing containers, and adopt all the old containers' resources to the new containers.
- **Automatic bin packing**: you can give nodes to k8s, tell it how much resources each container use, and k8s will fit containers onto your nodes to use the resources at their best.
- **Self-healing**: k8s restarts containers that fail, replaces containers, kills unhealthy ones, and doesn't advertise containers to clients until they are ready and all checks are green.
- **Secret and configuration management**: k8s lets you store and manage sensitive stuff, like passwords, secrets, keys. You can update secrets and app configurations without rebuilding images, or exposing secrets in your configuration.
- **Batch execution**: k8s can also manage the batch and CI workloads you have, replacing containers that fail if you want.
- **Horizontal scaling**: you can easily scale your app up and down by creating more containers of the same image. You can do it based on CPU usage, too!
- **Allocation of IPv4 and IPv6 addresses to pods and services**
## Cluster Architecture
A k8s cluster consists of two things: a *control plane* and set of worker machines, called *nodes*, which run the actual apps.
The worker nodes will then **host the *Pods*** that are the components of the application workload.
The control plane, as it name suggests, will **manage the worker nodes and pods in the cluster**.
As such, the control plan provides fault-tolerance and high availability. It usually runs across multiple computers in production environments.
![](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)
### Control Plane Components
The components of the control plane **work together to make decisions about the cluster** (scheduling, etc.). They also detect and respond to cluster events, for example, starting a new pod when the replicas quota isn't met.
Control plane components **can run on any machine in the cluster, but it's best to keep them all on the same machine for simplicity**, and keep from running containers on that machine, too.
#### kube-apiserver
The API server **exposes the Kubernetes API, and is the front end for the Kubernetes control plane**.
The main implementation is `kube-apiserver`. It is designed to scale horizontally.
#### etcd
[[etcd]] is the key value store used as k8s' backing store for all cluster data.
#### kube-scheduler
kube-scheduler **watches for Pods that have no assigned node, and assigns one for them to run on**.
Decisions are based on resource requirements, hardware, software, or policy constraints, affinity and anti-affinity specs, data locality, inter-workload interferences, and deadlines.
#### kube-controller-manager
This control plane component **runs controller processes**.
Logically, each controller is a separate process, but in practice they are all compiled into one binary, and run in a single process.
There are different types of controllers, including but not limited to:
- **Node controller**: responsible for noticing and responding when nodes go down
- **Job controller**: watches for Job objects that represent one-off tasks, and provisions Pods for them
- **EndpointSlice controller**: populates EntpointSlice objects to provide a link between Services and Pods
- **ServiceAccount controller**: creates default ServiceAccounts for new namespaces.
#### cloud-controller-manager
This component **embeds cloud-specific control logic**. It allows you to link your cluster into your cloud provider's API, and separates the components that interface with their platform from components that only interact with your cluster.
Worth noting, it **only runs in cloud environments, not on local setups or on your own premises**.
Same thing as the kube-controller-manager, the multiple logical processes are, in practice, a single process and binary.
### Node Components
These components **run on every single node**, and maintain running pods. They also provide the Kubernetes runtime environment.
#### kubelet
An **agent that runs on every node in the cluster, and makes sure that containers are running in a Pod**.
It takes a set of PodSpecs and ensures that the containers described are both running and healthy. It doesn't manage containers that weren't created by k8s.
#### kube-proxy
An optional component, it runs on each node in your cluster and implements part of the k8s Service concept.
In so doing, it maintains network rules on nodes, which allow communication to your Pods from network sessions inside or outside of your cluster.
kube-proxy uses the operating system filtering layer if available. Otherwise, it does the forwarding itself.
#### Container Runtime
A fundamental component. It is the engine that allows k8s to actually run the containers, and is responsible for the execution and lifecycle of containers within the environment.
Kubernetes supports multiple container runtimes, like [[containerd]], [[CRI-O]], and any other implementation of the [[Kubernetes CRI]]. [[Docker]] Engine can be used as well.
## Objects
Kubernetes objects are **persistent entities in the Kubernetes system; it uses these entities to represent the state of your cluster**.
They are used to describe **what apps on running and on which nodes, the resources available to these apps, and the policies around them** (how they should be have, like restart policies, upgrades, and fault-tolerance).
An object in Kubernetes is declarative; **you tell k8s what to do, and the system will constantly work to ensure that this object exists**.
You'll need to use the Kubernetes API to work with objects; tools such as the `kubectl` CLI tool makes this easier.
### Spec and Status
Almost all objects in k8s include two fields that govern its config: the `spec` and `status`.
For objects that have a `spec`, you **have to set it when you create the object**, providing a description of what you want to have (the desired state of your object).
The `status`, on the other hand, **describes the current state of the object**, supplied and updated by the k8s system and its components. It's the control plane that manages objects' states to match the desired state you have in the `spec`.
## Manifests
When you create an object, **you must provide the object spec to define its desired state**, as well as some basic information like the name of the object.
Even when using `kubectl`, you still have to provide a JSON string in the request body for the spec.
However, most often **you'll actually describe objects to `kubectl` using *manifests***.
These are usually [[YAML]], but you could also use [[JSON]] if needed. `kubectl` and other tools convert those manifests to JSON when sending the API request over HTTP.
### Required Fields
A manifest must contain a few mandatory values:
- `apiVersion`: which version of the k8s API we're going to use
- `kind`: what kind of object we'll be creating
- `metadata`: data that helps uniquely identify the object, including `name`, `UID`, and optional `namespace`
- `spec`: the state you desire for that object
The spec format for an object changes with the type of object you want, and might contain specific nested fields for that object.
### Example of a Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
### Create a Deployment from an Object
`kubectl apply -f https://path/to/your/manifest.yaml`
Of course you could use local paths too.
## Pods
Pods are **the smallest deployable unit of computing you create and manage in Kubernetes**.
A pod is a **group of one or more containers, with shared resources, and a spec for how to run containers**. They are disposable, and are easily replaced whenever a problem happens on one.
A pod's contents are always run in a shared context. As such, it **models a logical host by containing one or more application containers that are relatively tightly coupled**. A bit like as if they were all running on the same machine or VM, except it's all application-level boundaries managed by k8s.
**You need a container runtime on each of your cluster's nodes, so that Pods can run there**.
Usually, you run one container per Pod, however you could have multiple containers tightly-coupled on the same Pod.
Each Pod is meant to **run a single instance of a given app**, if you want to scale horizontally, create more identical pods.
Be careful modifying pods after they run. If you try to apply a pod's configuration anew, **it might error out because most configuration is immutable**. You'll need to delete the pod and try again.
### Example of a Pod
You could deploy it manually using `kubectl`, but usually they are created using workload resources, like Deployment or Job.
Also, **make sure your Pod's OS matches the node's OS**.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
#### Resource Management for Pods and Containers
When you write the spec for a Pod, **you can specify the resources each container needs**. kubelet handles resource constraints, while resource requests are handled by kube-scheduler.
In effect, **requests are what a container *needs*, and limits are well, limits for their resource usage**.
## ReplicaSets
ReplicaSets exist to **maintain a stable set of identical Pods running at a given time**.
Usually, you define a deployment, and it is that deployment which manages ReplicaSets automatically.
As such, it's **usually best to manage ReplicaSets through Deployments rather than directly**.
## Services
Services are abstractions inside a cluster **providing a stable, long lived [[IP Address]] or [[Hostname]] for a service implemented by one or more backend Pods**.
The individual pods making up a service can change over time.
They are essentially a **named abstraction over a selector of Pods and a port**.
## Gateways
The Gateway API (or its predecessor Ingress) allows you to **make Services accessible from outside the cluster**.
## Deployments
A deployment **is a declaration of a set of Pods or ReplicaSets**. You describe your desired state, and the *Deployment* works to make it happen **at a controlled rate**.
## Controllers
Controllers **track one object type, and focus on making the specs for these objects happen**.
They watch the state of the cluster, and make changes or request them where needed. Usually, they'll make requests to the API server to actually make changes, instead of doing the work themselves. Lazy ones, I tell you.
## Namespaces
A Kubernetes namespace **isolates groups of resources within a single cluster**.
Names of resources must be unique in a single namespace, but not across namespaces.
They are useful when multiple teams work on the same cluster; not so much when one cluster is dedicated to a team or project.
## Volumes
Volumes are a way for containers in a Pod to **access and share data through the filesystem**.
**There are different kinds of volumes available**, all built for specific purposes, such as configuration, scratch spaces, sharing files between containers, between pods, persistent storage across nodes, read-only access, etc.
# Distributions?
Kubernetes itself is akin to the Linux kernel: it's good, but doesn't provide the infrastructure to make it useful to end users.
K8s provides the core control-plane and node components (kube-apiserver, [[etcd]], scheduler, controller-manager, kubelet, kube-proxy), but **this doesn't give you a working cluster out of the box**.
# Resources
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)