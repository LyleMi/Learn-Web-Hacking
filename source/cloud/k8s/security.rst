Safety
========================================
Cluster security considers several goals:

- Ensure container and host isolation
- Limit the interference caused by containers to infrastructure/other containers
- Principle of least privilege
- Clearly define component boundaries
- Divide the roles of ordinary users and administrators
- Grant administrator rights to users if necessary
- Allow applications with Secret data to run in the cluster

Common security issues
----------------------------------------
- Unauthorized access to K8s API Server
- k8s configuration file leaked ``$HOME/.kube/config``
- Privilege escalation
    - Escalation of privileges within Pod
    - K8s privilege escalation
- Container escape
- Denial of service
