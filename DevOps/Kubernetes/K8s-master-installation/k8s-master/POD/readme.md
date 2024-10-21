# Kubernetes System Pods Overview

# 1. Cilium Components
Cilium is a networking solution that provides secure and observable networking between Kubernetes workloads.

cilium-envoy-*:
Envoy proxy instances managed by Cilium. They handle Layer 7 (application layer) traffic policies and enforce security rules between services.

cilium-*:
Cilium agents that run on each Kubernetes node. These agents manage network traffic, enforce security policies, and handle pod-to-pod communication.

cilium-operator-*:
A Cilium operator pod that manages Cilium-specific tasks, such as creating and managing Kubernetes custom resources and scaling Cilium components.

# 2. CoreDNS
CoreDNS is a DNS server that plays a key role in Kubernetes service discovery.

coredns-*:
CoreDNS pods are responsible for DNS resolution within the Kubernetes cluster, ensuring that services can be reached by their DNS names.
# 3. etcd
etcd is a distributed key-value store used by Kubernetes to store all its cluster data.

etcd-k8s-master:
This is the etcd pod running on the master node, which stores all cluster configuration and state data required for Kubernetes to function.
# 4. Kube-API Server
The Kubernetes API server is the central management point for all cluster operations.

kube-apiserver-k8s-master:
This pod exposes the Kubernetes API, processes REST requests, and is the core interface for controlling the cluster.
# 5. Kube-Controller Manager
The controller manager handles control loops that regulate the state of the cluster, ensuring desired states are met.

kube-controller-manager-k8s-master:
This pod runs the Kubernetes controller manager, which handles node lifecycle management, job automation, and other background tasks.
# 6. Kube-Proxy
Kube-Proxy is responsible for managing network rules on nodes, allowing communication between pods across nodes.

kube-proxy-*:
Each kube-proxy pod manages network rules and routing to ensure that services can communicate properly across different nodes.
# 7. Kube-Scheduler
The scheduler is responsible for assigning pods to nodes based on resource requirements and availability.

# 8. kube-scheduler-k8s-master:
This pod handles pod scheduling, ensuring that pods are placed on nodes with enough resources and according to constraints.


-----
<br><br>

# Kubernetes Pod Description Summary

## General Information
- **Name**: The name of the pod.
- **Namespace**: The namespace in which the pod resides (e.g., `kube-system`).
- **Priority**: The priority assigned to the pod. Higher values indicate higher priority.
- **Priority Class Name**: The name of the priority class associated with the pod.
- **Node**: The node on which the pod is currently running (includes the node name and IP address).
- **Start Time**: The timestamp when the pod was started, indicating its age.

## Labels and Annotations
- **Labels**: Key-value pairs used for identifying and organizing resources (e.g., `component=etcd`), helpful for selecting pods in queries.
- **Annotations**: Metadata associated with the pod, often used for non-identifying information (e.g., configuration details). Annotations can hold larger amounts of data compared to labels.

## Status
- **Status**: The current status of the pod (e.g., `Running`, `Pending`, `Succeeded`, `Failed`, `Unknown`).
- **SeccompProfile**: The security profile applied to the pod, which can help enforce security constraints.
- **IP**: The IP address assigned to the pod, used for communication.
- **IPs**: Any additional IP addresses assigned to the pod, useful for multi-homed pods.

## Containers
- **Containers**: Information about the containers within the pod, including:
  - **Container ID**: The unique identifier of the container in the runtime.
  - **Image**: The container image used (e.g., `registry.k8s.io/etcd:3.5.15-0`).
  - **Image ID**: The unique identifier for the image pulled from the registry.
  - **Port**: The port on which the container listens.
  - **Host Port**: The port on the host that maps to the container port.
  - **Command**: The command executed in the container.
  - **State**: The current state of the container (e.g., `Running`, `Waiting`, `Terminated`).
  - **Started**: The timestamp when the container was started.
  - **Ready**: Indicates if the container is ready to serve requests (`True` or `False`).
  - **Restart Count**: The number of times the container has restarted, which can indicate issues.
  - **Requests**: Resource requests made by the container (e.g., CPU and memory) that the scheduler uses to allocate resources.
  - **Limits**: Resource limits defined for the container, capping the usage.
  - **Liveness**: Liveness probe configuration to check container health, ensuring it’s restarted if unhealthy.
  - **Readiness**: Readiness probe configuration to check if the container is ready to serve traffic.
  - **Startup**: Startup probe configuration, checking if the application is ready to start.
  
## Conditions
- **Conditions**: The conditions indicating the state of the pod (e.g., `PodReady`, `Initialized`, `Ready`, `ContainersReady`, `PodScheduled`).

## Volumes
- **Volumes**: Information about volumes mounted in the pod, including:
  - **Volume Type**: The type of volume (e.g., `HostPath`, `PersistentVolumeClaim`, `ConfigMap`).
  - **Path**: The path where the volume is mounted inside the pod.
  - **Access Modes**: Permissions for accessing the volume (e.g., `ReadWriteOnce`, `ReadOnlyMany`).

## QoS and Scheduling
- **QoS Class**: The Quality of Service class assigned to the pod (e.g., `Guaranteed`, `Burstable`, `BestEffort`).
- **Node-Selectors**: Labels that determine the nodes on which the pod can run, influencing scheduling decisions.
- **Tolerations**: Conditions under which the pod can be scheduled onto nodes with taints.
- **Affinity/Anti-affinity Rules**: Rules that specify how pods should be placed relative to each other, affecting pod scheduling.

## Lifecycle Management
- **Termination Grace Period**: The duration the pod has to gracefully shut down before being forcibly terminated.
- **Init Containers**: Containers that run before the main containers in the pod, typically used for initialization tasks.
- **Preemption**: Whether the pod can preempt other pods to gain resources.

## Events
- **Events**: Any events associated with the pod, which may indicate warnings or important status changes, useful for debugging and monitoring.

## Resource Usage
- **Resource Metrics**: Information about resource usage, if metrics are available (e.g., CPU and memory usage).

## Networking
- **Host IP**: The IP address of the host node.
- **Service Account**: The service account under which the pod is running, affecting its permissions and access.

## Configuration
- **Environment Variables**: Any environment variables defined for the container.
- **Configurations**: Configurations defined through ConfigMaps or Secrets, affecting the application behavior.
