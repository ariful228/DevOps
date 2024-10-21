# Descriptions

## Node Metadata

### Name: `k8s-master`
The name of this node in the Kubernetes cluster, functioning as the **master node**.

### Roles: `control-plane`
This node is part of the control plane, responsible for managing the Kubernetes cluster, including the API server, controller manager, etc.

### Labels:
- `beta.kubernetes.io/arch=amd64`: The node uses **amd64 architecture** (64-bit system).
- `beta.kubernetes.io/os=linux`: The node's operating system is **Linux**.
- `kubernetes.io/arch=amd64`: Kubernetes label for the **architecture (64-bit)**.
- `kubernetes.io/hostname=k8s-master`: The **hostname** of this node is `k8s-master`.
- `kubernetes.io/os=linux`: This node is running the **Linux OS**.
- `node-role.kubernetes.io/control-plane`: Label specifying the node's role as part of the **control plane**.
- `node.kubernetes.io/exclude-from-external-load-balancers`: Prevents this node from being used by **external load balancers**.

### Annotations:
- `kubeadm.alpha.kubernetes.io/cri-socket`: Refers to the **container runtime interface (CRI)** socket path, using `crio`.
- `node.alpha.kubernetes.io/ttl`: **Time to live (TTL)** for the node, set to `0`, meaning the node should persist.
- `volumes.kubernetes.io/controller-managed-attach-detach`: Indicates Kubernetes manages **volume attachment and detachment**.

### Creation Timestamp:
- **Wed, 16 Oct 2024 11:09:16 +0000**

---

## Taints:
- **node-role.kubernetes.io/control-plane:NoSchedule**  
  This taint prevents regular workloads from being scheduled on the control-plane node unless the pod has a matching toleration.

---

## Lease:
- **HolderIdentity**: The current holder of the node lease is `k8s-master`.
- **RenewTime**: **Wed, 16 Oct 2024 18:04:53 +0000**  
  The most recent time when the node's lease was renewed.

---

## Conditions:
These represent the node's **health status**:
- **NetworkUnavailable**: `False`, meaning the **network is available** and Cilium (the network component) is running properly.
- **MemoryPressure**: `False`, indicating that the node has sufficient memory.
- **DiskPressure**: `False`, meaning there is **no disk pressure** (sufficient disk space).
- **PIDPressure**: `False`, showing that the node has enough **PID (Process IDs)** available.
- **Ready**: `True`, indicating the node is **ready** and able to run workloads.

---

## Addresses:
- **InternalIP**: `192.168.10.10`  
  The **internal IP address** of the node.
- **Hostname**: `k8s-master`  
  The **hostname** assigned to the node.

---

## Capacity and Allocatable Resources:

### Capacity:
- `cpu: 2`: The node has **2 CPU cores**.
- `memory: 2015104Ki`: Around **2 GB** of memory.
- `ephemeral-storage: 11758760Ki`: Approximately **11 GB** of storage available.
- `pods: 110`: The maximum number of **pods** that this node can run is **110**.

### Allocatable:
The actual resources available for workloads, considering **system overhead**:
- `cpu: 2`, `memory: 1912704Ki`: About **1.9 GB** of usable memory.
- `ephemeral-storage: 10836873199`: Available storage of approximately **10 GB**.

---

## System Info:
- **Machine ID**: Unique identifier for the machine (`bdacd68fa3e540cfad1154ce66849412`).
- **System UUID**: Hardware-specific unique identifier (`3a8d9f67-4507-504f-bd65-369086385fcc`).
- **Boot ID**: Unique identifier for the current boot session (`19bfdd5e-e9c0-461b-970c-9425cb3df945`).
- **Kernel Version**: The version of the **Linux kernel** in use (`6.8.0-45-generic`).
- **OS Image**: The version of the operating system (**Ubuntu 24.04.1 LTS**).
- **Operating System**: **Linux**.
- **Architecture**: The CPU architecture is **amd64** (64-bit).
- **Container Runtime Version**: The container runtime in use is **cri-o** version `1.31.1`.
- **Kubelet Version**: The version of the **Kubelet agent** running on this node (`v1.31.1`).
- **Kube-Proxy Version**: The version of **Kube-Proxy** (`v1.31.1`).

---

## Pods Running on Node:
The **namespace** column tells where each pod is deployed, followed by the resource requests and limits.

### Namespace:
- `kube-system`: The namespace for **Kubernetes system components**.

### Pods:
- **cilium-envoy-ddk2x**: Pod for the **Cilium networking component**, no specific CPU/memory resources requested or limited.
- **cilium-h4xxt**: Another Cilium pod requesting **100m CPU** and **10Mi memory**.
- **coredns-7c65d6cfc9-xvmsd**: CoreDNS pod, which handles **DNS resolution** within the cluster, requesting **100m CPU** and **70Mi memory**.
- **etcd-k8s-master**: Etcd (the **distributed key-value store** used by Kubernetes) pod, requesting **100m CPU** and **100Mi memory**.
- **kube-apiserver-k8s-master**: Kubernetes **API server**, which handles communication within the cluster, requesting **250m CPU**.
- **kube-controller-manager-k8s-master**: The **controller manager**, responsible for running background tasks, requesting **200m CPU**.
- **kube-scheduler-k8s-master**: The **scheduler**, which assigns pods to nodes, requesting **100m CPU**.

---

## Allocated Resources:
- **CPU**: `950m` (**47%**) of the total available CPU is requested by the running pods.
- **Memory**: `250Mi` (**13%**) of the total memory is requested, with `340Mi` (**18%**) as the memory limit.

---

## Events:
- **NodeNotReady**: The node was marked as **NotReady** 9 minutes ago, meaning it was temporarily unable to run workloads.
- **NodeReady**: The node has since returned to a **Ready** state 8 minutes ago, meaning it is now ready to handle workloads.
