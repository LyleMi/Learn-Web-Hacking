k8s concept
========================================
Kubernetes means "helmsman" or "driver" in Greek, and corresponds to Docker, often referred to as K8s. Kubernetes evolved from Google's Borg and is an open source system for automatically deploying, scaling, and managing containers.

composition
----------------------------------------
Kubernetes consists of a control plane (Master) and a data plane (Worker Node).
The core components of Master:

- API Server
- Controller-Mananger
- Scheduler
- etcd

Worker Node consists of the following nodes:

- Kubellet
- For proxy
- Container runtime

Core design
----------------------------------------

Pod
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A pod is the basic scheduling unit of Kubernetes. A pod generally contains one or more containers.
Each Pod in Kubernetes is assigned a unique IP address within a cluster so that the application can use the same port.
A Pod can define a volume, such as a local disk directory or network disk, and expose it to a container in the pod.
Pods can be managed manually through the Kubernetes API or delegated to the controller for automatic management.

Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Service is a unified entry address for a set of container applications with the same function, and is essentially a set of pods that work together.
