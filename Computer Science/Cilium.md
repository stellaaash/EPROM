---
tags:
  - tool/infra
---
Cilium is a **Container Network Interface (CNI) plugin built on [[eBPF]]**.
In a [[Kubernetes]] cluster,  it gives pods IPs and routes traffic between them.
# How It Works
It uses eBPF to plug into the cluster's nodes and their interfaces. This allows it to do some neat things:
- **Replace kube-proxy** by using its own eBPF hash maps instead of [[iptables]] rules.
- **Enforce network policies by identity** instead of using IPs, by assigning pods a numeric identity based on their labels.
It is usually deployed using a DaemonSet alongside a cluster-wide operator deployment.
## Operator Shenanigans
The controller/data plane split is back, baby! While cilium does need an agent running on all nodes of a k8s cluster, it also has an operator responsible for managing and gathering data.
# As an Ingress Controller
Cilium isn't just a CNI, it **also has a built-in Ingress controller**. Just set `ingressClassName: cilium` on an Ingress and Cilium will handle it if you've got it installed.
## Gateway?
It also implements the Gateway API.
## Controller Vs Data Plane
For the ingress controller scenario, the controller/data plane split still applies:
- The controller watches Ingress objects and translates them to routing configuration.
- The data plane embeds [[Envoy]] as a layer 7 proxy, taking a similar role as [[nginx]]. It doesn't run in a separate deployement, instead tagging along in the DaemonSet of Cilium agents, or as its separate DaemonSet.