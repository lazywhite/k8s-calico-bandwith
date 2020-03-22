## requirement for installing calico on kubernetes
```
Calico can run on any Kubernetes cluster which meets the following criteria.

The kubelet must be configured to use CNI network plugins (e.g --network-plugin=cni).
The kube-proxy must be started in iptables proxy mode. This is the default as of Kubernetes v1.2.0.
The kube-proxy must be started without the --masquerade-all flag, which conflicts with Calico policy.
The Kubernetes NetworkPolicy API requires at least Kubernetes version v1.3.0.
```

## minikube use calico
```
wget https://docs.projectcalico.org/manifests/calico.yaml
# make sure bandwidth plugin is enabled in configmap

kubectl apply -f calico.yaml
# check /etc/cni/net.d/, /opt/cni/bin

minikube stop
minikube start --network-plugin=cni 
```
## traffic shaping
```
kubectl apply -f bandwidth.yml
kubectl logs -n policy-demo iperf-client   # has bandwidth limitation
kubectl logs -n policy-demo iperf-client2
```
### calicoctl
```
wget https://github.com/projectcalico/calicoctl/releases/download/v3.13.1/calicoctl
export DATASTORE_TYPE=kubernetes
export KUBECONFIG=~/.kube/config
calicoctl get workloadendpoints
```
