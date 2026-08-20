k8s concept
========================================
Kubernetes means "helmsman" or "driver" in Greek, which corresponds to Docker and is often referred to as K8s. Evolved from Google's Borg, Kubernetes is an open source system for automatically deploying, scaling, and managing containers.

composition
----------------------------------------
Kubernetes consists of a control plane (Master) and a data plane (Worker Node).
Core components of Master:

- API Server
- Controller-Mananger
- Scheduler
- etcd

Worker Node consists of the following nodes:

- Kubelet
- Kube-Proxy
- Container runtime

core design
----------------------------------------

Pod
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Pod is the basic scheduling unit of Kubernetes. A Pod generally contains one or more containers.
Each Pod in Kubernetes is assigned a unique IP address within the cluster, allowing applications to use the same port.
A Pod can define a volume, such as a local disk directory or a network disk, and expose it to a container in the pod.
Pods can be managed manually through the Kubernetes API or delegated to a controller for automatic management.

Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Service provides a unified entry address for a group of container applications with the same functions. It is essentially a group of Pods that work together.
