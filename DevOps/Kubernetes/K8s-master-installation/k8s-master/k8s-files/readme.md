# Kubernetes Files, Locations, and Purposes

## 1. Kubernetes Configuration Files
- **`kubelet` Configuration**
  - **Location:** `/etc/kubernetes/kubelet.conf`
  - **Purpose:** Configuration file for the Kubelet, which manages the pods and containers on each node.

- **`kube-apiserver` Configuration**
  - **Location:** `/etc/kubernetes/manifests/kube-apiserver.yaml`
  - **Purpose:** Configuration file for the API server, which handles requests from users and internal components.

- **`kube-controller-manager` Configuration**
  - **Location:** `/etc/kubernetes/manifests/kube-controller-manager.yaml`
  - **Purpose:** Configuration for the Controller Manager, which manages various controllers to regulate the state of the cluster.

- **`kube-scheduler` Configuration**
  - **Location:** `/etc/kubernetes/manifests/kube-scheduler.yaml`
  - **Purpose:** Configuration file for the Scheduler, which assigns pods to nodes based on resource availability.

- **`etcd` Configuration**
  - **Location:** `/etc/kubernetes/manifests/etcd.yaml`
  - **Purpose:** Configuration for the etcd key-value store, which serves as the backing store for all cluster data.

## 2. Manifest Files
- **Pod Definitions**
  - **Location:** Typically located in a user-defined directory or in the `/etc/kubernetes/manifests` folder for static pods.
  - **Purpose:** YAML files defining the desired state for pods, including container images, resource requests, and configurations.

- **Deployment Definitions**
  - **Location:** User-defined directory (e.g., `/path/to/deployments/`)
  - **Purpose:** YAML files specifying the desired state for deployments, including the number of replicas and update strategies.

- **Service Definitions**
  - **Location:** User-defined directory (e.g., `/path/to/services/`)
  - **Purpose:** YAML files defining services to expose pods, including type (ClusterIP, NodePort, LoadBalancer) and port mappings.

## 3. Kubelet and Node Configuration
- **Kubelet Configuration**
  - **Location:** `/var/lib/kubelet/config.yaml` or `/etc/kubernetes/kubelet.conf`
  - **Purpose:** Configuration for the Kubelet, specifying node registration parameters and runtime settings.

- **Kubelet Certificates**
  - **Location:** `/var/lib/kubelet/pki/`
  - **Purpose:** Certificates and keys used for secure communication between the Kubelet and the API server.

## 4. Network Configuration
- **CNI Configuration Files**
  - **Location:** `/etc/cni/net.d/`
  - **Purpose:** Configuration files for Container Network Interface (CNI) plugins used for pod networking.

- **CNI Plugin Binaries**
  - **Location:** `/opt/cni/bin/`
  - **Purpose:** Binaries for CNI plugins that facilitate pod networking.

## 5. Log Files
- **Kubelet Logs**
  - **Location:** Typically found in system logs (e.g., `/var/log/syslog` or `/var/log/messages`).
  - **Purpose:** Logs related to the Kubelet's operations, including pod management.

- **API Server Logs**
  - **Location:** `/var/log/kube-apiserver.log`
  - **Purpose:** Logs detailing requests made to the API server and responses sent back.

- **Controller Manager Logs**
  - **Location:** `/var/log/kube-controller-manager.log`
  - **Purpose:** Logs related to the operations of the Controller Manager.

- **Scheduler Logs**
  - **Location:** `/var/log/kube-scheduler.log`
  - **Purpose:** Logs detailing the scheduling decisions made by the Scheduler.

## 6. Cluster Configuration
- **Kubeconfig Files**
  - **Location:** `~/.kube/config`
  - **Purpose:** Configuration file used by `kubectl` to access the Kubernetes API server, containing information about clusters, contexts, and users.

## 7. Additional Directories
- **`/etc/kubernetes/manifests`**
  - **Purpose:** Directory for static pod manifests that are managed directly by the Kubelet.

- **`/etc/kubernetes/pki`**
  - **Purpose:** Directory for public/private key pairs and certificates used for secure communication within the cluster.

## 8. Monitoring and Metrics
- **Prometheus Configurations**
  - **Location:** User-defined, often within `/etc/prometheus/` or similar directories.
  - **Purpose:** Configuration files for Prometheus, a monitoring tool used to collect and query metrics from Kubernetes.

## 9. Helm Charts
- **Helm Chart Files**
  - **Location:** Typically user-defined directories (e.g., `/path/to/charts/`)
  - **Purpose:** Package files used by Helm to define, install, and manage Kubernetes applications.
