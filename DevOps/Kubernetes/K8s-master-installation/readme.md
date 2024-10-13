
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
>[!NOTE]
 >Nodes can show "Ready" status without Calico. <br>
 >Calico is essential for pod networking, and without it, won't be able to run pods properly across the cluster.<br>
 >Coredns can show "ContainerCreating", without CNI plugin (calico).<br>

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
```
sudo snap remove microk8s

netstat -antlp | grep 10259

sudo lsof -i :10259
sudo lsof -i :10257 ; sudo lsof -i :10250 ; sudo lsof -i :10259

sudo kill -9 85847

   
```

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
> `sudo KUBECONFIG=/etc/kubernetes/admin.conf kubectl remove -f calico.yaml`

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

<br><br>

# Error: 05

```
kubectl get pods -n kube-system
NAME                                 READY   STATUS              RESTARTS      AGE
coredns-7c65d6cfc9-5sxtj             0/1     ContainerCreating   6 (40m ago)   25h
coredns-7c65d6cfc9-qbprl             0/1     ContainerCreating   6 (40m ago)   25h
etcd-k8s-master                      1/1     Running             9             25h
kube-apiserver-k8s-master            1/1     Running             9             25h
kube-controller-manager-k8s-master   1/1     Running             11            25h
kube-proxy-2927w                     1/1     Running             6             22h
kube-proxy-gsqjw                     1/1     Running             7             25h
kube-proxy-lfx2v                     1/1     Running             7             25h
kube-scheduler-k8s-master            1/1     Running             13            25h

```

# Solution:05
>> By installing calico

<br><br>

# ERROR: 06
```
kubectl get pods -n kube-system
NAME                                       READY   STATUS                  RESTARTS          AGE
calico-kube-controllers-6879d4fcdc-xnmdp   1/1     Running                 5                 23h
calico-node-5bvs8                          0/1     Init:CrashLoopBackOff   149 (4m20s ago)   22h
calico-node-6tqbk                          0/1     Init:CrashLoopBackOff   117 (43s ago)     20h
calico-node-lgd6w                          1/1     Running                 5                 23h
coredns-7c65d6cfc9-5sxtj                   1/1     Running                 5                 23h
coredns-7c65d6cfc9-qbprl                   1/1     Running                 5                 23h
etcd-k8s-master                            1/1     Running                 7                 23h
kube-apiserver-k8s-master                  1/1     Running                 7                 23h
kube-controller-manager-k8s-master         1/1     Running                 9                 23h
kube-proxy-2927w                           1/1     Running                 5                 20h
kube-proxy-gsqjw                           1/1     Running                 6                 22h
kube-proxy-lfx2v                           1/1     Running                 5                 23h
kube-scheduler-k8s-master                  1/1     Running                 10                23h
```

# Solution: 06

<br><br>

# Error: 07

```
 kubectl get pods
NAME       READY   STATUS                   RESTARTS   AGE
test-pod   0/1     ContainerStatusUnknown   1          44m

```

# Solution:
> Install CNI plugin(calico)
> out-of-memory >[!ADD]

<br><br>

# Network adapter
```
how to do this "Check network adapters
If you have more than one network adapter, and your Kubernetes components are not reachable on the default route, we recommend you add IP route(s) so Kubernetes cluster addresses go via the appropriate adapter"
```
<br><br>

# Master Readiness Commands as raff

## 1. Basic Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `clear`                     | Clears the terminal screen.                        |
| `ls`                        | Lists the files and directories in the current directory. |
| `cd [directory]`           | Changes the current working directory.             |
| `ll`                        | Lists the files and directories in a long listing format (with details). |
| `pwd`                       | Prints the current working directory.              |
| `cat [file]`               | Displays the content of a file.                   |
| `exit`                      | Exits the terminal or current session.             |
| `history`                   | Shows the command history of the terminal.         |

## 2. Networking Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `ifconfig`                  | Displays network interface configuration.          |
| `ip a`                      | Shows IP address and network interface information. |
| `ping [IP/hostname]`       | Sends ICMP echo requests to test network connectivity. |
| `hostname`                  | Prints or sets the system's hostname.             |
| `hostname -i`              | Displays the IP address associated with the hostname. |
| `hostname -I`              | Displays all IP addresses associated with the hostname. |
| `ip route show`            | Displays the routing table.                        |
| `nc [IP] [port]`           | Netcat tool to test TCP/UDP connections.          |
| `telnet [IP] [port]`       | Opens a telnet connection to test port connectivity. |

## 3. System Management Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `apt install [package]`    | Installs a package.                               |
| `sudo apt install [package]` | Installs a package with superuser privileges.   |
| `apt-get update`           | Updates the list of available packages.           |
| `sudo apt-get update`      | Updates the package list with superuser privileges. |
| `sudo systemctl status [service]` | Checks the status of a system service. |
| `sudo systemctl enable [service]` | Enables a service to start at boot.     |
| `sudo systemctl start [service]` | Starts a system service.                 |
| `sudo systemctl restart [service]` | Restarts a system service.             |
| `sudo reboot`              | Reboots the system.                              |
| `init 0`                   | Shuts down the system.                           |

## 4. SSH & Remote Access Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `apt install ssh`          | Installs the SSH service.                         |
| `sudo apt install ssh`     | Installs SSH with superuser privileges.           |
| `sudo systemctl status ssh` | Checks the status of the SSH service.            |
| `sudo systemctl start ssh` | Starts the SSH service.                           |
| `sudo systemctl enable ssh` | Enables SSH to start at boot.                   |

## 5. File and User Permissions Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `sudo visudo`              | Opens the sudoers file for editing.               |
| `sudo cat /etc/sudoers`    | Displays the content of the sudoers file.        |
| `sudo vim [file]`          | Edits a file with vim using superuser privileges. |
| `sudo chown [user]:[group] [file]` | Changes the ownership of a file.       |
| `sudo mkdir -p [directory]` | Creates a directory (including parent directories) with superuser privileges. |

## 6. Kubernetes Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `kubeadm init`             | Initializes a Kubernetes master node.             |
| `kubectl get nodes`        | Lists all nodes in the Kubernetes cluster.        |
| `kubectl cluster-info`     | Displays cluster information.                      |
| `kubectl apply -f [file]`  | Applies a configuration file to Kubernetes.       |
| `kubectl describe [resource]` | Describes a specific Kubernetes resource.     |
| `kubectl config view`      | Views Kubernetes configuration.                    |
| `kubectl get pods -n kube-system` | Lists all pods in the kube-system namespace. |
| `sudo kubeadm reset`       | Resets the Kubernetes cluster.                     |

## 7. Networking Tools and Diagnostics
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `netstat -ntup`            | Displays network connections and listening ports.  |
| `lsof -i :[port]`          | Lists open files and ports in use on a system.    |
| `sudo lsof -i :[port]`     | Lists open files and ports using superuser privileges. |
| `netstat -antlp | grep [port]` | Filters network connections for a specific port. |

## 8. Swap and Kernel Settings
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `sudo swapoff -a`          | Disables swap.                                    |
| `swapon -s`                | Displays swap status.                             |
| `sudo sysctl -w net.ipv4.ip_forward=1` | Enables IP forwarding.                 |

## 9. File Transfer & Downloading Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `curl [URL]`               | Downloads or transfers data from a URL.          |
| `sudo curl [URL]`          | Downloads data from a URL with superuser privileges. |
| `echo [variable]`          | Prints the value of a variable.                   |

## 10. Process Management Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `ps aux | grep [process]`   | Lists processes and searches for a specific one.  |
| `kill -9 [PID]`            | Forces termination of a process by its PID.       |
| `sudo kill -9 [PID]`       | Terminates a process with superuser privileges.    |

## 11. Network Configuration Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `sudo netplan apply`        | Applies network configuration changes made with Netplan. |
| `sudo cat /sys/class/dmi/id/product_uuid` | Shows the product UUID of the system. |

## 12. Miscellaneous Commands
| Command                     | Description                                        |
|-----------------------------|----------------------------------------------------|
| `export [variable]=[value]` | Sets an environment variable.                     |
| `env`                       | Displays all environment variables.                |
