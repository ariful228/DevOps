
# Kubernetes Cluster Master Setup

## This document outlines the steps for setting up a Kubernetes master node, including necessary commands and configurations.

## Initial Setup

### ifconfig
`ping 8.8.8.8`

<br><br>

# SSH Setup
## Check the status of SSH and enable it if necessary.

```
sudo apt install ssh
sudo systemctl status ssh
sudo systemctl enable ssh
sudo systemctl start ssh
```
<br><br>

# Verify hostname configurations.

```
hostname -I
hostname
```
## Set the hostname for the master node.

```
sudo hostnamectl set-hostname k8s-master
sudo reboot

```


# Netplan configuration directory and review the configuration.

```
cd /etc/netplan/
ls
sudo cat 50-cloud-init.yaml
sudo netplan apply
sudo vim 50-cloud-init.yaml
network:
    ethernets:
        enp0s3:
            dhcp4: true
        enp0s8:
            addresses: [192.168.10.11/24]
    version: 2
```

<br><br>


# Disable swap (required for Kubernetes).
`sudo swapoff -a`

# Enable route
`sysctl -w net.ipv4.ip_forward=1`

# Netfilter
`modprobe br_netfilter`

<br><br>


# Kubernetes Installation

## Define the Kubernetes version and used CRI-O stream

```
KUBERNETES_VERSION=v1.31
CRIO_VERSION=v1.31
```
<br><br>

## Add Kubernetes GPG key and repository.

<div>

**Distributions using deb packages**

*Install the dependencies for adding repositories*<br>
`apt-get update` <br>
`apt-get install -y software-properties-common curl`<br>

<br>

**Add the Kubernetes repository**

```
curl -fsSL https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/deb/Release.key | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/deb/ /" | tee /etc/apt/sources.list.d/kubernetes.list
```
<br>

**Add the CRI-O repository**

```
curl -fsSL https://pkgs.k8s.io/addons:/cri-o:/stable:/$CRIO_VERSION/deb/Release.key | gpg --dearmor -o /etc/apt/keyrings/cri-o-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/cri-o-apt-keyring.gpg] https://pkgs.k8s.io/addons:/cri-o:/stable:/$CRIO_VERSION/deb/ /" |  tee /etc/apt/sources.list.d/cri-o.list
```
<br>

**Install the packages**<br>
`apt-get update`<br>
`apt-get install -y cri-o kubelet kubeadm kubectl`<br>

<br>

**Start CRI-O**<br>
`systemctl start crio.service`

</div>

<br><br>


# Kubernetes Initialization <br>
## Initialize the Kubernetes cluster.<br>
`kubeadm init`<br>
`sudo kubeadm init --apiserver-advertise-address=192.168.10.10`<br>


## Set up kubeconfig for the kubectl command.

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```



<br><br>

# Networking Setup
## Apply a pod network (e.g., Calico).
`kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml`


<br><br>

## Verify that the nodes are set up correctly.
`kubectl get nodes`

<br><br>

# Additional Commands [ERRRO]
## To check the status of Kubernetes components:
`sudo systemctl status kubelet`


## To view the logs of the Kubernetes API server:
`sudo journalctl -u kube-apiserver`


## To list all pods in the kube-system namespace:
`kubectl get pods -n kube-system`


## To reset the Kubernetes cluster (use with caution):
`sudo kubeadm reset`

<br><br>

# Error -01
```
sudo kubeadm join 192.168.10.10:6443 --token m93ju8.yaqafr7acworva8l --discovery-token-ca-cert-hash sha256:16ac20accf41447cb8bcd79b0a86d44f17fd5052f36ae75f2e23f500cfacee27
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR FileAvailable--etc-kubernetes-kubelet.conf]: /etc/kubernetes/kubelet.conf already exists
        [ERROR Port-10250]: Port 10250 is in use
        [ERROR FileAvailable--etc-kubernetes-pki-ca.crt]: /etc/kubernetes/pki/ca.crt already exists
[preflight] If you know what you are doing, you can make a check non-fatal with --ignore-preflight-errors=...
To see the stack trace of this error execute with --v=5 or higher"
```
# Solution:01 
>> Remove existing app which one taken thise port

<br><br>

# Error -02

```
ariful@k8s-master:~$ kubectl get pods -n kube-system
NAME                                 READY   STATUS              RESTARTS   AGE
coredns-7c65d6cfc9-5sxtj             0/1     ContainerCreating   0          5m42s
coredns-7c65d6cfc9-qbprl             0/1     ContainerCreating   0          5m42s
etcd-k8s-master                      1/1     Running             2          5m48s
kube-apiserver-k8s-master            1/1     Running             2          5m46s
kube-controller-manager-k8s-master   1/1     Running             3          5m52s
kube-proxy-lfx2v                     1/1     Running             0          5m43s
kube-scheduler-k8s-master            1/1     Running             3          5m46s"
```

# Solution:02
## By install carico network plugin
> `kubectl delete -f https://docs.projectcalico.org/manifests/calico.yaml`
> `kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml`
> `sudo kubeadm certs renew all`
> `sudo systemctl restart kubelet`

<br><br>


# Error:03
```
 kubectl get nodes
E1012 07:56:33.833153    1290 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.10.10:6443/api?timeout=32s\": dial tcp 192.168.10.10:6443: connect: connection refused"
E1012 07:56:33.834925    1290 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.10.10:6443/api?timeout=32s\": dial tcp 192.168.10.10:6443: connect: connection refused"
E1012 07:56:33.837104    1290 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.10.10:6443/api?timeout=32s\": dial tcp 192.168.10.10:6443: connect: connection refused"
E1012 07:56:33.838791    1290 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.10.10:6443/api?timeout=32s\": dial tcp 192.168.10.10:6443: connect: connection refused"
E1012 07:56:33.840593    1290 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.10.10:6443/api?timeout=32s\": dial tcp 192.168.10.10:6443: connect: connection refused"
The connection to the server 192.168.10.10:6443 was refused - did you specify the right host or port?
```

# Solution :03
>> Copy config file to login user's home direcotory under .kube and give the permission.

<br><br>

# Error:04
```
ariful@k8s-master:~$ sudo systemctl status kubelet
● kubelet.service - kubelet: The Kubernetes Node Agent
     Loaded: loaded (/usr/lib/systemd/system/kubelet.service; enabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/kubelet.service.d
             └─10-kubeadm.conf
     Active: activating (auto-restart) (Result: exit-code) since Sat 2024-10-12 06:07:23 UTC; 2s ago
       Docs: https://kubernetes.io/docs/
    Process: 2420 ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBELET_KUBEADM_ARGS $KUBELET_EXTRA_ARGS (code=exited, status=1/F>
   Main PID: 2420 (code=exited, status=1/FAILURE```

```
# Solution:04
>> Trun off swapon 
>> Enable route 
>> Restart kubelet

# Network adapter
```
how to do this "Check network adapters
If you have more than one network adapter, and your Kubernetes components are not reachable on the default route, we recommend you add IP route(s) so Kubernetes cluster addresses go via the appropriate adapter"
```
