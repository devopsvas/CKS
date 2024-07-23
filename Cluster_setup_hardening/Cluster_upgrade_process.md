## Upgrade process 


K8S will only minor three version , That is When version 1.3 is released, then 10.12 and 1.11 are supported.

1. No compenets are allowded to have higher version than kube-apiserver (Version X)

2. Controller manager and kube-scheduller can be at one version lower (Version X-1)

3. Kubelet and kube-proxy can be 2 vertsions below (Version X-2)

4. kubectl can be at (Version X +1 > X-1)

Upgrade is allowded to do minor version at a time 

v.1.10 >> v.1.111 >> v.1.12 >> v.1.13 


