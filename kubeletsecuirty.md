# How to check kubeclet running 

`ps -aux | grep kubelet` 

Port numbers used 

10250 - Servers API that allows full acecss 

10255 - API athat allows unauthenticated full acecss 

`curl -sk https://localhost:10255/metrics`

# Prevent unauthoprized access to kubelet 

Set kubelet service to dsiable anonymous 

`ExecStart=/usrlocal/kubelet`
....
....
`- anonymous=false`

Or set the same in kubelet-config.yaml 
(find out the current config is in use using kubelet-config.yaml)

# Refer certificate based authentication in Keubelet 


# To Disbale 10255

in kublet configuration file 

set 

`--read-only-port=0`

or kubelet-config configuration 

`readOnlyPort: 0`


`ps -aux | grep kubelet`


root        3849  0.0  0.1 1480700 271144 ?      Ssl  07:51   0:12 kube-apiserver --advertise-address=192.11.21.9 --allow-privileged=true --authorization-mode=Node,RBAC --client-ca-file=/etc/kubernetes/pki/ca.crt --enable-admission-plugins=NodeRestriction --enable-bootstrap-token-auth=true --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt --etcd-keyfile=/etc/kubernetes/pki/apiserver-etcd-client.key --etcd-servers=https://127.0.0.1:2379 --kubelet-client-certificate=/etc/kubernetes/pki/apiserver-kubelet-client.crt --kubelet-client-key=/etc/kubernetes/pki/apiserver-kubelet-client.key --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname --proxy-client-cert-file=/etc/kubernetes/pki/front-proxy-client.crt --proxy-client-key-file=/etc/kubernetes/pki/front-proxy-client.key --requestheader-allowed-names=front-proxy-client --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt --requestheader-extra-headers-prefix=X-Remote-Extra- --requestheader-group-headers=X-Remote-Group --requestheader-username-headers=X-Remote-User --secure-port=6443 --service-account-issuer=https://kubernetes.default.svc.cluster.local --service-account-key-file=/etc/kubernetes/pki/sa.pub --service-account-signing-key-file=/etc/kubernetes/pki/sa.key --service-cluster-ip-range=10.96.0.0/12 --tls-cert-file=/etc/kubernetes/pki/apiserver.crt --tls-private-key-file=/etc/kubernetes/pki/apiserver.key
root        7741  0.0  0.0 3766768 90156 ?       Ssl  07:54   0:01 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --container-runtime-endpoint=unix:///var/run/containerd/containerd.sock --pod-infra-container-image=registry.k8s.io/pause:3.9
root        8245  0.0  0.0   6928  2200 pts/0    S+   07:54   0:00 grep --color=auto kubelet





# Calling pods API 

`curl -sk https://localhost:10250/pods`


# Setting authorization mode to  Webhhok in kubelet 

```
vi /var/lib/kubelet/config.yaml 
```
```
apiVersion: kubelet.config.k8s.io/v1beta1
authentication:
  anonymous:
    enabled: true
  webhook:
    cacheTTL: 0s
    enabled: true
  x509:
    clientCAFile: /etc/kubernetes/pki/ca.crt
authorization:
  mode: Webhook
```


`# systemctl restart kubelet`


# Then check if you can still access pods endpoint with

`# curl -sk https://localhost:10250/pods`


# Disable unauthorized authetication mode 

`# vi /var/lib/kubelet/config.yaml`

apiVersion: kubelet.config.k8s.io/v1beta1
authentication:
  anonymous:
    enabled: false

` # systemctl restart kubelet`


# Output 

` controlplane ~ ➜  curl -sk https://localhost:10250/pods`
Unauthorized


# Check the metrics is on 10255

` curl -sk http://localhost:10255/metrics1`


# Disable metrics endpoint on readOnlyPort.


`/var/lib/kubelet/config.yaml`

runtimeRequestTimeout: 0s
shutdownGracePeriod: 0s
shutdownGracePeriodCriticalPods: 0s
staticPodPath: /etc/kubernetes/manifests
streamingConnectionIdleTimeout: 0s
syncFrequency: 0s
volumeStatsAggPeriod: 0s
readOnlyPort: 0

` # systemctl restart kubelet `


# Check metrics 

`curl -sk http://localhost:10255/metrics`
