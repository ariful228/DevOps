#  Kubernetes workflow diagram. 

```mermaid
graph TD
    A[Kubernetes Cluster] --> B[Master Node]
    B --> C[API Server]
    B --> D[Controller Manager]
    B --> E[Scheduler]
    B --> F[etcd]
    A --> G[Worker Nodes]
    G --> H[Kubelet]
    G --> I[Container Runtime]
    G --> J[Pods]
    J --> K[Application Containers]

    subgraph User Interaction
        L[User] --> M[kubectl]
    end

    M --> C
    C -->|API Calls| D
    C -->|API Calls| E
    C -->|Data Storage| F
    D -->|Control Actions| G
    E -->|Pod Scheduling| G
    G -->|Health Status| H
    H -->|Monitoring| J

```
<br> <br> <br> 

# Explanation of the Diagram <br>
**User Interaction:** Users interact with the Kubernetes cluster using the kubectl command-line tool.<br>
**Master Node:** The control plane that manages the Kubernetes cluster.<br>
**API Server:** The main management component that handles REST requests and updates the state of the cluster.<br>
**Controller Manager:** Manages controllers that regulate the state of the cluster.<br>
**Scheduler:** Assigns workloads to the available worker nodes based on resource requirements.<br>
**etcd:** A distributed key-value store that holds all the cluster data.<br>
**Worker Nodes:** The machines that run the application workloads.<br>
**Kubelet:** An agent that runs on each worker node, ensuring that containers are running in a pod.<br>
**Container Runtime:** Software responsible for running containers (e.g., Docker, containerd).<br>
**Pods:** The smallest deployable units in Kubernetes that can hold one or more containers.<br>
**Application Containers:** The actual applications running inside the pods.<br>

<br><br>


# Kubernetes main components:
**Control Plane Components** <br>
*API Server: *Central control point for Kubernetes.<br>
*etcd:* Stores all cluster data.<br>
*Controller Manager:* Manages controllers (e.g., node, replication).<br>
*Scheduler:* Assigns pods to nodes.<br>
*Cloud Controller Manager:* Manages cloud provider interactions.<br><br>
**Node Components**<br>
*Kubelet:* Runs on each node, manages containers.<br>
*Kube Proxy:* Handles networking for pods.<br>
*Container Runtime:* Runs containers (e.g., Docker, containerd).<br><br>
**Networking**<br>
*Service:* Exposes pods (ClusterIP, NodePort, LoadBalancer).<br>
*Ingress Controller:* Manages external access.<br><br>
**Storage**<br>
*Persistent Volumes (PV):* Allocates storage.<br>
*Persistent Volume Claims (PVC):* Requests storage.<br>
*Storage Classes:* Defines storage types.<br><br>
**Config and Secrets**<br>
*ConfigMaps:* Stores configuration data.<br>
*Secrets: *Stores sensitive information.<br><br>
**Monitoring and Logging**<br>
*Metrics Server:* Collects resource metrics.<br>
*Prometheus: *Monitoring solution.<br>
*Grafana:* Metrics visualization.<br><br>
**Others**<br>
*Namespaces: *Isolates resources.<br>
*CRDs:* Extend Kubernetes with custom resources.<br>
*kubectl:* CLI for managing the cluster.<br>
*Helm:* Kubernetes package manager.<br>
*ArgoCD: *GitOps continuous delivery tool for Kubernetes, syncing manifests from Git<br>