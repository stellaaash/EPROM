---
tags:
  - standard
  - organization
abbreviation: OCI
---
The OCI or Open Container Initiative **standardized container images as a format**, and created a spec for [[HyperText Transfer Protocol]] registries to distribute them.
OCI **publishes three notable specifications**: distribution, image, and runtime.
# Image
The image specification aims to **standardize the structure of container images**.
It does this through three main goals: be translatable to a runtime environment (the OCI runtime spec), be content-adressable (able to be referenced by content via a hash, rather than just through its name), and to support multiple platforms (through the image index, referencing multiple image manifests, each for a specific architecture).
## Aren't These Just Docker Images?
A *container image* is sometimes mistaken to be any image built using [[Docker]]. However, **Docker images are OCI images, the tool doesn't define the specification.**
This means that any supported too, including Docker, but also [[Podman]] or [[Kaniko]] could build OCI images, and run images built by other tools, as well!
## Structure of an OCI Image
### Manifest
A metadata file that **describes the components of the image**.
### Layers
The layers that stack to **form the image.** Each layer **represents incremental changes to the file system of the image**.
### Configuration
A file that **describes environment variables, startup commands, working directories, and more**.
# Distribution
The distribution specification **specifies distributions methods for container images, so that they can interact with repositories through standardized [[HyperText Transfer Protocol]] APIs**.
## Registries
The specification defines *registries* which **provide HTTP APIs for storing, pulling, and distributing OCI images**.
Public and private registries are possible. Respectively, an example would be Docker Hub, and Harbor.
# Runtime
The runtime specification **defines the standards for actually running and managing the container images**.
## Configuration
The specification defines the **container configuration by a `config.json` file**.
This file describes container processes, mounts, hooks, resource limits, and more.
## Execution Environment
The spec also ensures a consistent environment for executing an image, including the way of extracting the image into the runtim filesystem bundle (*translating*).
## Lifecycle
The specification defines the **detailed process of a container from creation to termination**.
# Resources
- [OCI Image Format Specification - GitHub](https://github.com/opencontainers/image-spec/blob/main/spec.md)
- [OCI Introduction - Rifewang on Medium](https://medium.com/@rifewang/oci-introduction-the-full-journey-from-code-to-container-in-a-kubernetes-environment-1e36d2890ca5)