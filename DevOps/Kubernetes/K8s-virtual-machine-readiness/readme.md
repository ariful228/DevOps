 # Virtual Machine Readiness
 >[!NOTE]
 >1. Downloal and install Virtual BOX
 >2. Ubuntu servier installed
 >3. hostname configured as k8s-master
 >4. IP address configured as 192.168.10.10
 >5. ssh server installed
 >6. We have added 2nd NETWORK ADPATER
 >7. Take VM snapshot
 >8. Login by MobaXtrem

<br><br>

# Prerequisite Summary for Installing kubeadm

## System Requirements: CPU(2) & RAM(2GB)
>[!NOTE]
 >Compatible Linux host (Debian or Red Hat based).
 >Minimum 2 GB RAM and 2 CPUs for control plane machines.

<br>

## Network Requirements:
>[!NOTE]
 >Full network connectivity between all cluster machines.
 >Unique hostname, MAC address, and product_uuid for each node.

<br>

## Network Adapters:(one or more)
>[!NOTE]
 >Ensure the correct network adapter is used for Kubernetes components. If multiple adapters exist, configure appropriate IP routes.

<br>

## Ports:(6443)
>[!NOTE]
 >Required ports must be open for Kubernetes components.

<br>

## Routing:
>[!NOTE]
 >Verify that routes are properly configured.
`sysctl -w net.ipv4.ip_forward=1`

<br>

## Loading the br_netfilter module:
>[!NOTE]
 >br_netfilter module is often necessary when using network plugins like Calico, Flannel.
`modprobe br_netfilter`

<br>


## Swap Configuration:
>[!NOTE]
 >Disable swap `/etc/fstab` for persistence.

<br>

## Container Runtime:
>[!NOTE]
 >Install a compatible container runtime (e.g. CRI-O).

<br>

## Define the Kubernetes version and used CRI-O stream
>[!NOTE]
 >KUBERNETES_VERSION=v1.31
 >CRIO_VERSION=v1.31

<br>

## Install Packages:
>[!NOTE]
 >Install kubeadm, kubelet, and kubectl.

<br>

## Cgroup Driver:
>[!NOTE]
 >Ensure matching cgroup drivers for kubelet and container runtime.

<br>

## Calico Network Plugin:
>[!NOTE]
 >Install Calico for pod networking and network policy management.