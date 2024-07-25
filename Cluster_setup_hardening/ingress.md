## Ingress

 [Refernce](https://kubernetes.io/docs/concepts/services-networking/ingress/)

Ingress is a layer 7 load balancer built inside k8s as any other load balancer, Yiu can manage it a k8s object 


Ingress you need to expose it to the outside world


Ingress controllers - GCP load balancer, NGINX, Contour, HA proxy, Trafeik , Istio


Solution we implement is - Ingress controller 

Set of rules confifgure are - Ingress resources

n k8s version 1.20+, we can create an Ingress resource in the imperative way like this:-

kubectl create ingress  --rule="host/path=service:port"

kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"

## How to chekc the ingress Controller, resources and application deployed 

`# kubectl get all -A`

## Checking the name of the ingress controlelr deployed 

`# kubectl get deploy -A`

ingress-nginx   ingress-nginx-controller   1/1     1            1           4m15s

## How to check all application deployed in one namesapce

`# kubectl get deploy --namespace app-space`

## To find the ingress respurce deployed in 

`# kubectl get ingress --all-namespaces`


# How to check the ingress resource in detail 


`# kubectl describe ingress --namespace app-space `


# How to find the default routing path in Ingress 

`# kubectl describe ingress --namespace app-space `

Find the filed "Defult backend" like given beloe

Default backend:  <default>

<default> value means  it is rouuted to default path mentioned in ngnix controller deployment 

## to check the same 

`# kubectl get deploy ingress-nginx-controller -n ingress-nginx -o yaml`


containers:
      - args:
        - /nginx-ingress-controller
        - --publish-service=$(POD_NAMESPACE)/ingress-nginx-controller
        - --election-id=ingress-controller-leader
        - --watch-ingress-without-class=true
        - --default-backend-service=app-space/default-backend-service




## To make the video available in /stream 


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
  name: ingress-wear-watch
  namespace: app-space
spec:
  rules:
  - http:
      paths:
      - backend:
          service:
            name: wear-service
            port: 
              number: 8080
        path: /wear
        pathType: Prefix
      - backend:
          service:
            name: video-service
            port: 
              number: 8080
        path: /stream
        pathType: Prefix


```

You are requested to make the new application available at /pay.

Identify and implement the best approach to making this application available on the ingress controller and test to make sure its working. Look into annotations: rewrite-target as well.

## Check the service and understand the prot 

`# kubectl get svc -n critical-space`

```yaml
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
  - http:
      paths:
      - path: /pay
        pathType: Prefix
        backend:
          service:
           name: pay-service
           port:
            number: 8282
```



Ref:- https://learn.kodekloud.com/user/courses/certified-kubernetes-security-specialist-cks/module/eac6dac8-4481-4138-96ef-a2135f20e05e/lesson/416fc31d-8436-4fb2-be44-8d29bee19334
