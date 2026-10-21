---
tags:
  - tool/infra
---
Hubble **plugs into [[Cilium]]'s [[eBPF]] programs to export information from them**, such as traffic history, the verdict for each incoming request, etc.
These are then aggregated for all the cluster, and you can read them either through the `hubble` cli, a UI map, [[Prometheus]] metrics.