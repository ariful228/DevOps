# Troubleshoot the control plane communication between the API server, kubelet, and etcd, and verify that they all use the same IP series.


## 1. Check API Server Configuration
>[!NOTE]
> Verify the API server’s IP address and port. The API server usually runs on the master node, listening on a specific IP.<br>
> To check the configuration of the API server:<br>
> `kubectl -n kube-system describe pod <api-server-pod-name>`

>[!TIP]
> Alternatively, you can check the configuration files typically located at `/etc/kubernetes/manifests/kube-apiserver.yaml` on the master node. <br> Look for the `--advertise-address and --bind-address flags` to see which IP the API server is using.

## 2. Check Kubelet to API Server Communication
>[!NOTE]
>The kubelet on each node communicates with the API server. To check the kubelet’s configuration and ensure it's using the correct IP for the API server:<br>
>On each worker node, check the kubelet configuration file, which is typically located at `/etc/kubernetes/kubelet.conf` or `/var/lib/kubelet/config.yaml`. <br>
>Look for the --api-servers flag (if present) or check the server address in the config file to ensure that the kubelet is communicating with the API server’s correct IP. <br>
grep server `/var/lib/kubelet/config.yaml`

## 3. Check etcd Cluster Configuration
>[!NOTE]
>The etcd cluster is critical for control plane communication and cluster state storage. <br>
>Check the etcd pod configuration in the `/etc/kubernetes/manifests/etcd.yaml` file on the master node. Look for `--advertise-client-urls` and `--listen-client-urls` to verify which IP etcd is using. <br>
`cat /etc/kubernetes/manifests/etcd.yaml`
You can also check the status of etcd members: <br>
`etcdctl --endpoints=<etcd-ip>:2379 member list`

## 4. Verify IP Series
>[!NOTE]
>To ensure that all components (API server, kubelet, and etcd) use IPs from the same series: <br>
>API Server IP: Check the IP from the kube-apiserver.yaml file. <br>
>Kubelet Configured IP: On each node, check the kubelet configuration as mentioned above to verify that it's using the same network range as the API server. <br>
etcd IP: From the etcd.yaml file, check the `--advertise-client-urls` and verify the IP series. <br>
You can list IP addresses using the following command: <br>

>`kubectl get nodes -o wide`
>The EXTERNAL-IP or INTERNAL-IP columns will show the IP addresses of the nodes, including the control plane node running the API server and etcd.

## 5. Network Connectivity Testing

>[!NOTE]
>Ping the API server, etcd, and kubelet to ensure network connectivity.

```
ping <api-server-ip>
ping <etcd-ip>
ping <node-ip>
```
>Check for connectivity between the master and worker nodes (including communication between kubelet and API server):

`curl -k https://<api-server-ip>:6443/healthz`

## 6. Check Logs for Errors
>[!NOTE]
>API Server Logs:
`kubectl logs -n kube-system <api-server-pod-name>`
>Kubelet Logs (on worker nodes):
`journalctl -u kubelet`
>etcd Logs:
`kubectl logs -n kube-system <etcd-pod-name>`
Look for any errors or timeouts indicating communication issues between the components.







Here’s a Markdown document summarizing the findings and solutions related to the Kubernetes configuration and permission issues encountered:

markdown

# Kubernetes Configuration and Permission Issues

## 1. Environment Variables

### Check Current Environment Variables
```
env
Remove KUBECONFIG from Environment
To unset the KUBECONFIG variable:
unset KUBECONFIG

Change OLPWD Variable
To change the OLDPWD variable:
export OLDPWD=/home/ariful/.kube
```

### 2. Kubeconfig Management
```
Set KUBECONFIG in .rc
To set KUBECONFIG permanently:
echo "export KUBECONFIG=/etc/kubernetes/admin.conf" >> ~/.rc
source ~/.rc

Directory Management
Create a directory for kube configuration:
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config


mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/kubelet.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

```


### 3. Permission Issues
```
Common Errors
* unable to read client-cert /var/lib/kubelet/pki/kubelet-client-current.pem for default-auth due to open /var/lib/kubelet/pki/kubelet-client-current.pem: permission denied
Steps to Fix Permission Issues

Check File Permissions
ls -l /var/lib/kubelet/pki/kubelet-client-current.pem

Change File Permissions Allow read access to the kubelet client certificate:
sudo chmod 644 /var/lib/kubelet/pki/kubelet-client-current.pem

Change File Ownership If necessary, change the ownership to your user:
sudo chown ariful:ariful /var/lib/kubelet/pki/kubelet-client-current.pem

Re-run kubectl Command After modifying permissions, retry:
kubectl get nodes

Use sudo as Last Resort If permission issues persist, you can run:
sudo kubectl get nodes
```

### 4. Additional Commands
```
View Current Kubernetes Context
kubectl config current-context

Verify Nodes Status
kubectl get nodes
```