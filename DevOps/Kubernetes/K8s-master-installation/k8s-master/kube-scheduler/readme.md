```sql
                +------------------------------------+
                |         kube-apiserver             |
                | (Receives Pod Creation Requests,   |
                |   Watches for Unschedled Pods)     |
                +------------------------------------+
                             |
                             v
                +------------------------------------+
                |         kube-scheduler             |
                |   (Selects Node for Pod Placement, |
                |    Based on Policies & Resources)  |
                +------------------------------------+
                             |
                             v
           +--------------------------------------------+
           |         Filtering and Scoring Phases       |
           |   (Filters Nodes, Scores Based on Metrics) |
           +--------------------------------------------+
                             |
                             v
           +--------------------------------------------+
           |      Selects the Best Node for the Pod     |
           |     (Based on Resources & Constraints)     |
           +--------------------------------------------+
                             |
                             v
                +------------------------------------+
                |         kube-apiserver             |
                | (Informs API Server of Scheduling, |
                |    Updates Cluster State in etcd)  |
                +------------------------------------+
                             |
                             v
                +------------------------------------+
                |         Target Node (Worker)       |
                |    (Pod is Deployed and Started)   |
                +------------------------------------+

```


# Explanation of the Process:
## kube-apiserver:

When a user requests the creation of a new Pod (through kubectl or other means), the kube-apiserver receives the request.
The Pod is created but remains in an unscheduled state, meaning it does not have an assigned node to run on yet.
The kube-apiserver watches for these unscheduled Pods and informs the kube-scheduler that scheduling is required.

## kube-scheduler:

The kube-scheduler is responsible for assigning Pods to the best available node. It monitors the kube-apiserver for newly created Pods that need to be scheduled.
It decides on the node placement based on factors such as:
Available CPU and memory resources on the nodes.
Policies and constraints defined in the Pod specification (like node affinity, tolerations, etc.).
Custom priorities and affinity rules (if configured).

## Filtering and Scoring:

The scheduling process happens in two main phases:
Filtering Phase: The scheduler eliminates nodes that are unsuitable for the Pod based on criteria like resource availability (CPU, memory), taints, and tolerations, or node affinity.
Scoring Phase: After filtering out the unsuitable nodes, the scheduler scores the remaining nodes based on factors such as the node's current workload, available resources, and the pod's resource requirements.

## Selecting the Best Node:

The node with the highest score (the one that best fits the Pod’s needs) is selected. The kube-scheduler chooses this node for the Pod and passes this decision back to the kube-apiserver.
kube-apiserver Updates Cluster State:

The kube-apiserver records the scheduling decision by updating etcd, which stores the cluster’s desired state and the Pod’s assignment to the chosen node.

## Target Node (Worker):

The chosen node (often a worker node) is then responsible for deploying the Pod. The kubelet on that node pulls the required container images, creates the Pod, and starts the container(s).
The Pod transitions from the "Pending" state to "Running."

## Summary:

The kube-scheduler is responsible for placing Pods on the most suitable nodes in the cluster based on resource availability and other constraints.
It works by:
Watching the kube-apiserver for unscheduled Pods.
Filtering and scoring available nodes based on resource usage, policies, and rules.
Selecting the best node for the Pod and informing the kube-apiserver.
Once a node is selected, the kubelet on that node handles the actual creation and deployment of the Pod, transitioning it from pending to running.