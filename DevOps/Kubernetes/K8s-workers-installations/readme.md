# Kubernetes Node Configuration: k8s-node01

This document outlines the steps to configure the Kubernetes node `k8s-node01`.

## 1. Set Hostname

`sudo hostname k8s-node01` <br>
`ip a`<br>
`sudo hostnamectl set-hostname k8s-node01`<br>
`hostname`<br>
`reboot`<br>


# 2. Install OpenSSH Server
```
sudo apt install openssh-server
sudo systemctl status ssh
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
reboot
sudo reboot
```

# 3. Check Sudoers File
```
cat /etc/sudoers
sudo cat /etc/sudoers
sudo visudo
sudo cat /etc/sudoers
```

# 4. Network Configuration
```
ip link
sudo cat /sys/class/dmi/id/product_uuid
nc 127.0.0.1 6443 -v

nc -lk 6443
 >> hello

nc 192.168.10.12 6443
 >> hello

nc -lk 22
nc -zv 192.168.10.10 6443

```
# Netplan configuration directory and review the configuration.

```
cd /etc/netplan/
ls
sudo cat 50-cloud-init.yaml
sudo vim 50-cloud-init.yaml
sudo netplan apply

Edit:
network:
    ethernets:
        enp0s3:
            dhcp4: true
        enp0s8:
            addresses: [192.168.10.11/24]
    version: 
    
    ```

# 5. Disable Swap
`sudo swapoff -a`

# 6. Remove MicroK8s (if applicable)
```
sudo snap remove microk8s
sudo microk8s stop
sudo rm -rf /var/snap/microk8s
sudo rm -rf /snap/microk8s
```

# 7. Network Connectivity Test

`ping 8.8.8.8`

# 8. Install Kubernetes Components
`kubectl versio`n

# Set Kubernetes and CRI-O versions
```
KUBERNETES_VERSION=v1.31
CRIO_VERSION=v1.31
```

# Update package lists
`sudo apt-get update`<br>
`sudo apt-get install -y software-properties-common curl`


# Add Kubernetes APT key and repository
```
sudo curl -fsSL https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
# Add CRI-O APT key and repository
```
curl -fsSL https://pkgs.k8s.io/addons:/cri-o:/stable:/$CRIO_VERSION/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/cri-o-apt-keyring.gpg
sudo echo "deb [signed-by=/etc/apt/keyrings/cri-o-apt-keyring.gpg] https://pkgs.k8s.io/addons:/cri-o:/stable:/$CRIO_VERSION/deb/ /" | sudo tee /etc/apt/sources.list.d/cri-o.list
```

# Final updates and installation
```
apt-get update
sudo apt-get update
sudo apt-get install -y cri-o kubelet kubeadm kubectl
```

# 9. Verify Installations
```
kubectl version
kubelet version
kubelet --version
swapon -s
kubectl get nodes
```

# 10. Manage Kubelet Service
```
systemctl status kubelet
sudo systemctl start kubelet
sudo systemctl enable kubelet
systemctl status kubelet
sudo journalctl -u kubelet -f
```

# 11. Check Node Status
```
kubectl --kubeconfig /etc/kubernetes/kubelet.conf get nodes
top
sudo systemctl restart kubelet
systemctl status kubelet
kubectl get nodes
cat /etc/kubernetes/kubelet.conf
```


# 12. Configure Swap and Sysctl

```
sudo vim /etc/fstab
sudo swapoff -a
sudo vim /etc/sysctl.conf
sudo systemctl restart kubelet
sudo systemctl enable kubelet
sudo systemctl status kubelet
sudo journalctl -u kubelet -b
```

# 13. Reboot Node
```
reboot
sudo reboot
```

# 14. Final Node Verification
    
```
kubectl get nodes
sudo systemctl status kubelet
```

# 15.  Join the Kubernetes Cluster

# Alternative join command with different IP
```
sudo kubeadm join 192.168.10.10:6443 --token m93ju8.yaqafr7acworva8l --discovery-token-ca-cert-hash sha256:16ac20accf41447cb8bcd79b0a86d44f17fd5052f36ae75f2e23f500cfacee27
```

# 16. Final Check of Nodes
`kubectl get nodes`


# Error -01
```
NAME          READY         STATUS              RESTARTS      AGE
k8s-master    ready
k8s-node01    Notready

```

# Solution: 01

## 1. Disable swap (permanently):
```
udo swapoff -a
Edit /etc/fstab to ensure swap is off after reboot.
Route settings (permanently):
```
## 2. Route on
`sudo vim /etc/sysctl.conf`

##  3. Reboot the system:
`sudo reboot`


# Error -02
```
does not working " sudo kubectl get nodes
E1012 11:01:55.693241    2280 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1012 11:01:55.695241    2280 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1012 11:01:55.697375    2280 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1012 11:01:55.699349    2280 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
E1012 11:01:55.701268    2280 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
The connection to the server localhost:8080 was refused - did you specify the right host or port?"

```
# Solution: 02

## Create a directory .kube for the current user:
`mkdir -p ~/.kube`

## Move the kubelet.config file there and give permissions:
```
cp /etc/kubernetes/kubelet.conf ~/.kube/config
chmod 600 ~/.kube/config
```

## Verify kubectl command:
`kubectl get nodes`