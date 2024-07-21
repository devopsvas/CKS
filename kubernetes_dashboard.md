# K8S Dash board

## References

https://redlock.io/blog/cryptojacking-tesla

https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

https://github.com/kubernetes/dashboard

https://www.youtube.com/watch?v=od8TnIvuADg

https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca

https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md


## Install k8s dashboard

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml`

`kubectl patch svc kubernetes-dashboard --type='json' -p '[{"op":"replace","path":"/spec/type","value":"NodePort"}]' -n kubernetes-dashboard`



### Create a service account "admin-user"

`$ vi k3s-dashboard.yaml`

```yaml
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kube-system
```

### Create Cluter role binding 

```yaml
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kube-system
  
```




### Apply the configuration 

  `$ kubectl create -f k3s-dashboard.yaml`

### To create Token 


`# kubectl -n kube-system  create token admin-user`


## Create a read only user 

`# kubectl create sa readonly-user -n kubernetes-dashboard`



cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: readonly-user
  namespace: kubernetes-dashboard
EOF

cat <<EOF | kubectl apply -f -
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: readonly-user-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: view
subjects:
- kind: ServiceAccount
  name: readonly-user
  namespace: kubernetes-dashboard
EOF

# generate a token for read-only user 

`kubectl -n kubernetes-dashboard get secret readonly-user -o go-template="{{.data.token | base64decode}}"`




[[Reference]]https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles
