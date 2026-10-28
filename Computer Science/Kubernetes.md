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

# Apply a Pod manifest
kubectl apply -f <path/to/pod-manifest.yaml>
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
# Isn't Docker Sufficient?
Containers are great, sure. They help you run your applications in simple, reproducible environments.
Think of an enterprise context, though. **Launching containers is fine, but what if one goes down?** Wouldn't it be better to have a dedicated tool than to use a bash script, or a simple `restart: unless-stopped`?
Kubernetes aims to fill this gap, by **providing a framework to run distributed systems with resilience. It takes care of scaling, and failover for your application.**
## What k8s brings to the Table
- **Service discovery and load balancing**: k8s can expose a container using a DNS name or its own [[IP Address]].
- **Storage orchestration**: k8s allows you to automatically mount a storage system of your choice, like local storage, public cloud providers, and more.
- **Automated rollouts and rollbacks**: you describe your app's desired state using k8s, and it then changes the current state to what you want, at a controlled rate. For example, you can tell k8s to create new containers, remove existing containers, and adopt all the old containers' resources to the new containers.
- **Automatic bin packing**: you can give nodes to k8s, tell it how much resources each container use, and k8s will fit containers onto your nodes to use the resources at their best.
- **Self-healing**: k8s restarts containers that fail, replaces containers, kills unhealthy ones, and doesn't advertise containers to clients until they are ready and all checks are green.
- **Secret and configuration management**: k8s lets you store and manage sensitive stuff, like passwords, secrets, keys. You can update secrets and app configurations without rebuilding images, or exposing secrets in your configuration.
- **Batch execution**: k8s can also manage the batch and CI workloads you have, replacing containers that fail if you want.
- **Horizontal scaling**: you can easily scale your app up and down by creating more containers of the same image. You can do it based on CPU usage, too!
- **Allocation of IPv4 and IPv6 addresses to pods and services**
# Cluster Architecture
A k8s cluster consists of two things: a *control plane* and set of worker machines, called *nodes*, which run the actual apps.
The worker nodes will then **host the *Pods*** that are the components of the application workload.
The control plane, as it name suggests, will **manage the worker nodes and pods in the cluster**.
As such, the control plane provides fault-tolerance and high availability. It usually runs across multiple computers in production environments.
![](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)
## Control Plane Components
The components of the control plane **work together to make decisions about the cluster** (scheduling, etc.). They also detect and respond to cluster events, for example, starting a new pod when the replicas quota isn't met.
Control plane components **can run on any machine in the cluster, but it's best to keep them all on the same machine for simplicity**, and keep from running containers on that machine, too.
### kube-apiserver
The API server **exposes the Kubernetes API, and is the front end for the Kubernetes control plane**.
The main implementation is `kube-apiserver`. It is designed to scale horizontally.
### etcd
[[etcd]] is the key value store used as k8s' backing store for all cluster data.
### kube-scheduler
kube-scheduler **watches for Pods that have no assigned node, and assigns one for them to run on**.
Decisions are based on resource requirements, hardware, software, or policy constraints, affinity and anti-affinity specs, data locality, inter-workload interferences, and deadlines.
### kube-controller-manager
This control plane component **runs controller processes**.
Logically, each controller is a separate process, but in practice they are all compiled into one binary, and run in a single process.
There are different types of controllers, including but not limited to:
- **Node controller**: responsible for noticing and responding when nodes go down
- **Job controller**: watches for Job objects that represent one-off tasks, and provisions Pods for them
- **EndpointSlice controller**: populates EntpointSlice objects to provide a link between Services and Pods
- **ServiceAccount controller**: creates default ServiceAccounts for new namespaces.
### cloud-controller-manager
This component **embeds cloud-specific control logic**. It allows you to link your cluster into your cloud provider's API, and separates the components that interface with their platform from components that only interact with your cluster.
Worth noting, it **only runs in cloud environments, not on local setups or on your own premises**.
Same thing as the kube-controller-manager, the multiple logical processes are, in practice, a single process and binary.
It is used, for example, for setting load balancer rules in the cloud controller's config when you create a LoadBalancer Service.
## Node Components
These components **run on every single node**, and maintain running pods. They also provide the Kubernetes runtime environment.
### kubelet
An **agent that runs on every node in the cluster, and makes sure that containers are running in a Pod**.
It takes a set of PodSpecs and ensures that the containers described are both running and healthy. It doesn't manage containers that weren't created by k8s.
### kube-proxy
An **optional** component, it runs on each node in your cluster and implements part of the k8s Service concept.
In so doing, it **maintains network rules on nodes, which allow communication to your Pods from network sessions inside or outside of your cluster**.
kube-proxy uses the operating system filtering layer if available. Otherwise, it does the forwarding itself.
It is optional for cases when **you have your own network plugin that implements packet forwarding for Services**, providing equivalent functionality than kube-proxy.
### Container Runtime
A fundamental component. It is **the engine that allows k8s to actually run the containers**, and is responsible for the execution and lifecycle of containers within the environment.
Kubernetes supports multiple container runtimes, like [[containerd]], [[CRI-O]], and any other implementation of the Kubernetes CRI. [[Docker]] Engine can be used as well.
# Scheduling
## Taints and Tolerations
Node affinity **determines whether pods are "attracted" to a set of nodes**, either as a preference or a hard requirement.
Taints, on the other hand, **allow a node to repel a set of pods**.
Tolerations **allow (but don't guarantee!) the scheduler to schedule pods with matching taints**.
All in all, they work together to ensure that **pods that don't tolerate a given taint aren't scheduled on a node that has that taint**.
# Objects
Kubernetes objects are **persistent entities in the Kubernetes system; it uses these entities to represent the state of your cluster**.
They are used to describe **what apps on running and on which nodes, the resources available to these apps, and the policies around them** (how they should be have, like restart policies, upgrades, and fault-tolerance).
An object in Kubernetes is declarative; **you tell k8s what to do, and controllers will constantly work to ensure that this object exists**.
You'll need to use the Kubernetes API to work with objects; tools such as the `kubectl` CLI tool makes this easier.
## Spec and Status
Almost all objects in k8s include two fields that govern its config: the `spec` and `status`.
For objects that have a `spec`, you **have to set it when you create the object**, providing a description of what you want to have (the desired state of your object).
The `status`, on the other hand, **describes the current state of the object**, supplied and updated by the k8s system and its components. It's the control plane that manages objects' states to match the desired state you have in the `spec`.
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
The individual pods making up a service can change over time. This is why having a long-lived IP or hostname is useful.
They are essentially a **named abstraction over a selector of Pods and a port**.
### Headless Services
A headless service does away with the whole load balancing part of services, **allowing clients to connect to whichever Pod it prefers, directly**.
It does this through [[Domain Name System]] entries, in the cluster's DNS service, for the individual Pods.
You make a Service headless by **specifying `"None"` in the cluster IP address `.spec.clusterIP`**. It has to be a ClusterIP Service.
## Gateway
The Gateway API (or its predecessor Ingress) allows you to **make Services accessible from outside the cluster**.
## Ingress
Ingress' job is to **expose HTTP and HTTPS routes from outside the cluster to Services inside the cluster**. Routing is controlled by rules defined on the Ingress resource itself.
### Ingress Controllers
**Creating an Ingress resource**, by itself, **doesn't change anything**. For it to do something, you'll need an Ingress Controller.
**The controller's job is to watch** your Ingress, Services and EndpointSlices **and update the actual proxy/load balancer that will receive those requests**. For the nginx controller, it's nginx.
**Usually, the controller is a Pod**, too, and sometimes even the data plane is (the proxy/load balancer). The exception is usually the cloud providers' load balancers, which obviously have to sit outside of your cluster to work as a cloud provider.
You have many available to choose, but you have to choose one and set it up in your cluster for it to have Ingress capability.
The official ones are AWS and GCE, but there are [lots of third party controllers available, too](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/#third-party-ingress-controllers).
You can actually **deploy multiple Ingress controllers using Ingress Classes** within a cluster.
Ideally, all controllers must follow [the k8s spec](https://kubernetes.io/docs/reference/kubernetes-api/service-resources/ingress-v1/#IngressSpec), but **most operate slightly differently and have some quirks**.
### Ingress Rules
Essentially, **ingress rules define paths from which to route requests to backends** (a combination of Service and port names).
You can define a route that points to another resource in the same namespace as the ingress. You can't point to both a Service and a resource in the same rule.
### Default Backend
**The default backend will be queried whenever a request doesn't match any configured routes.**
If no default backend is configured, then the routing will be up to your ingress controller. They might each handle it differently, so make sure to check their docs!
### Ingress Classes
**Each Ingress should have a class, a reference to an IngressClass resource** that contains some config info, including the name of the controller that should implement that class.
This class will then define which controller will be used, and with which parameters.
**This allows you to have multiple controllers in a single cluster**, as each Ingress can reference the class name to select their controller.
In practice, **when a controller starts, it configures itself with the routes that have their class name referenced**. If a route doesn't, the controller simply ignores it.
## Deployments
A deployment **is a declaration of a set of Pods or ReplicaSets**. You describe your desired state, and the Deployment controller works to make it happen **at a controlled rate**.
They provide three main features:
- **Availability**: set the number of replicas for a type of service/app, and work to maintain it. Schedule/delete pods to meet the required count.
- **Scalability**: Update the replica count, scale up or down.
- **Update Strategy**: Define a release strategy for pod updates, and roll them out accordingly.
## Jobs
Jobs are **one-off deployments that run a task to completion and then stop**.
It creates a certain number of Pods, and will retry execution until a quota of successful Pods is reached.
## CronJobs
CronJob resources **create Jobs at an interval**.
## Namespaces
A Kubernetes namespace **isolates groups of resources within a single cluster**.
Names of resources must be unique in a single namespace, but not across namespaces.
They are useful when multiple teams work on the same cluster; not so much when one cluster is dedicated to a team or project.
## Volumes
Volumes are a way for containers in a Pod to **access and share data through the filesystem**.
**There are different kinds of volumes available**, all built for specific purposes, such as configuration, scratch spaces, sharing files between containers, between pods, persistent storage across nodes, read-only access, etc.
Some volumes types are ephemeral, but others are persistent.
Concretely, **a volume is just a directory that is accessible to containers in a Pod**. The volume type then determines the directory's creation, the backing medium, and its contents.
### Ephemeral Volumes
Some volume kinds are ephemeral, meaning **they only exist as long as their attached Pod exists**.
These are particularly useful for applications that need to store data, but not persistently.
When adding one to a Pod's manifest and applying it, the ephemeral volume controller will automatically create a PVC for that volume, and will ensure that it gets deleted when the Pod gets deleted. The garbage collector is then responsible for deleting the PVC and the underlying volume.
### Persistent Volumes
Persistent Volumes are **a piece of storage in the cluster that has been provisioned, either manually by an administrator, or dynamically through Storage Classes**.
It is a resource in the cluster like all others.
Contrary to standard volumes, **persistent volumes have a lifecycle distinct from the pods that use it**. That's why they're, well, persistent.
Persistent Volume objects **capture the details of the underlying implementation** ([[Network File System]], [[iSCSI]], or a cloud-provider storage system).
### Persistent Volume Claims
A PVC or Persistent Volume Claim is a **request for storage by a user**.
It's similar to a pod in the sense that it **consumes storage resources**, just like a pod does with memory and CPU.
Just like a Pod can request specific levels of resources, claims can request **specific size and access modes**.
### Lifecycle of a Volume and Claim
1. You **provision** the persistent volume; either statically or dynamically
	1. Static is when **you (the administrator of the cluster) create persistent volumes** manually. They then exist in the Kubernetes API and are available for consumption.
	2. Dynamic is when none of the already-present PVs match the claim. In this case, **the cluster will attempt to provision a new volume using available StorageClasses**. Of course, you'll need to have created and configured those classes for this to work.
2. A user creates a PersistentVolumeClaim, requesting a certain amount of storage, with certain access modes. The control plane watches for these, finds a matching PV if it exists (or creates a PV from a matching StorageClass), and **binds** them together. Those binds are always exclusive. If a PV wasn't available, either statically or dynamically, the claim remains unbound until a PV is provisioned for it.
3. Finally, pods can then **use the claims as volumes**.
4. Once your pods are done using it, the volume can be **reclaimed**. The reclaim policy then defines what happens to the volume: retaining or deleting it.
### Projected Volumes
Project volumes allow you to **map multiple volumes sources into the same directory**.
### Storage Classes
Storage classes allow an administrator to **provide types of storage that can be claimed**. Instead or provisioning volumes in advance, you can provide a class, and a user can then claim a class to create a new instance of that volume.
Classes can basically mean anything you want: fast/slow storage, backup policies, or anything else that you want to distinguish between storage classes.
**They abstract away the details of how the volumes are implemented**, and effectively provide an item that PVCs can request on-demand.
You can have multiple storage classes to allow for seamless migration (the most recently added default storage class will always be used).
#### Relationships to PVs and PVCs
PVs can have a class name, which **reserves them for PVCs that want this storage class** specifically. This allows you to pre-provision persistent volumes for a given storage class.
PVCs can request a particular class, or no class with `""` which means they **will be bound to a PV with no class either**. It will not use the default storage class; for this, don't set a class name at all, not even with `""`.
#### Default Storage Class
You can **label a StorageClass as the default for your cluster**, which will be used when a PVC doesn't specify a `storageClassName`. Or,
## ConfigMaps
ConfigMaps are **key-value stores for non-confidential configuration**. Pods can consume ConfigMaps as environment variables, cli argument, or as configuration files in a volume.
They are **useful to decouple your environment-specific config from your container images**, so that the latter stay portable.
For secret stuff, make sure to use Secrets instead.
## Secrets
A Secret is an object that **contains a small amount of sensitive data, like a password, key, or token**.
These are useful to prevent adding sensitive information in your container image or application code.
They are **similar to ConfigMaps but intended for confidential data**.
Worth noting that **secrets, by default, are unencrypted in the control plane's key value store (etcd)**.

## Probes
A probe is a **diagnostic periodically performed by the kubelet on a container to monitor the health of containers in a Pod**.
You can then configure Kubernetes to restart unhealthy containers or stop sending traffic to containers that aren't ready.
There are multiple types of probes that a kubelet can perform and react to.
### Startup Probes
These probes **verify that the application within a container is started**. They only run at startup, not periodically.
It stops other probe types from executing until it suceeds. This way, the app has time to launch before being checked for health of readiness.
**If it fails, the container is killed**, and its restart policy applies.
### Liveness Probe
These probes are used **for when an app hits a deadlock, or otherwise can't continue without being restarted**.
It has a tolerance ceiling, and **when the failure count for that probe exceeds that, the kubelet restarts the container**.

> [!CAUTION]
> Be careful to set these up correctly; make sure the conditions for liveliness probes only target cases when the app truly cannot proceed without a restart. Otherwise, you'll get restarts for things that could have been resolved without one, lowering your app's stability.
### Readiness Probe
These probes **check whether the app is ready to accept traffic**, for example at startup time or after having recovered from a fault or overload.
If it fails, the EndpointSlice controller will **remove the Pod's IP from the EndpointSlices** of all Services that match the Pod.

# Controllers
Controllers **track one object type, and focus on making the specs for these objects happen**.
They watch the state of the cluster, and make changes or request them where needed. Usually, they'll make requests to the API server to actually make changes, instead of doing the work themselves. Lazy ones, I tell you.
# Manifests
When you create an object, **you must provide the object spec to define its desired state**, as well as some basic information like the name of the object.
Even when using `kubectl`, you still have to provide a JSON string in the request body for the spec.
However, most often **you'll actually describe objects to `kubectl` using *manifests***.
These are usually [[YAML]], but you could also use [[JSON]] if needed. `kubectl` and other tools convert those manifests to JSON when sending the API request over HTTP.
## Required Fields
A manifest must contain a few mandatory values:
- `apiVersion`: which version of the k8s API we're going to use
- `kind`: what kind of object we'll be creating
- `metadata`: data that helps uniquely identify the object, including `name`, `UID`, and optional `namespace`
- `spec`: the state you desire for that object
**The spec format for an object changes with the type of object you want**, and might contain specific nested fields for that object.
## Example of a Manifest
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
# Distributions
Kubernetes itself is akin to the Linux kernel: it's good, but doesn't provide the infrastructure to make it useful to end users.
K8s provides the core control-plane and node components (kube-apiserver, [[etcd]], scheduler, controller-manager, kubelet, kube-proxy), but **this doesn't give you a working cluster out of the box**.
## List of Distributions
- [[k3s]]
- [[OpenShift]]
# Operators
A Kubernetes operator is **a method of package, deploying, and managing a Kubernetes application**.
Concretely, it is a beefed up controller that will not only manage your application's state, but also bundle additional functionality in order to create, configure and manage instances of complex applications, automatically.
It uses Custom Resources to manage apps and their components; the user provides their configuration in the CRs, and the operator makes it happen based on its internal logic.
Sound familiar? The similarities to simple controllers stop here.
Kubernetes opoerators continue to monitor applications as they run, **and can back up data, recover from failures, and upgrade applications over time, automatically**.
It doesn't have to stop here though: an operator could scale the app, do version upgrades, manage kernel modules for nodes with specialized hardware, and much, much more.
## Why Though?
Sure, automation sounds nice, but isn't all of this something a controller should be able to do?
Here's the thing. **Controllers work great for stateless applications**: scaling and managing them. **Where they falter is as soon as state is involved**: databases, monitoring systems, these require additional domain-specific knowledge that Kubernetes doesn't have.
**Usually, you'd need a human** engineer to solve this problem. This becomes a problem at scale, and **it's why operators exist**.
## Implementation
Kubernetes operators use **Kubernetes extensions** to encode the specific domain knowledge.
# Resources
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [Operators - Red Hat](https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-operator)