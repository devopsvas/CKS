kubectl utility will be either locally or in remote srever

We can inetract with kube-api server with port 6443

`curl http://<kube-api-srvere>:6443 -k --key admin.key -cert admin.crt --cacert ca.crt`


# kubectl proxy setup 

`kubectl proxy`

`curl http://localhost:8001`

It will be accessible locally 

`curl 127.0.0.1:8001/version > /root/kube-proxy-test-version.json`

# Proxy any serverice in k8s using kubectl service 


If we have a nginx service (Cluser Ip) only accessible with in teh cluster 

`kubectl proxy`

`curl http://localhost:8001/api/v1/namespaces/default/services/nginx/proxy/`


Protforward using kubectl 

`kubectl prot-forward service/nginx 28080:80`

`curl http://localhost:28080`


kubectl proxy - Opens proxy port to API server

kubectl port-forward - Opens port to target deployment pods
