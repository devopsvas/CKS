There are two type of traffic 

1. Ingress
2. Egress 

Ingree -> Incoming traffic 
Egress - > Outgoing traffic

Network policy is another object in k8s, We can link netwok policy to one or more pods.

We use the labels for applying NP.

Inside the pod
```yml
labels:
  apache
```
```yml
podSelector:
  matchLabels:
    role:apache
``` 

[Reference](https://kubernetes.io/docs/concepts/services-networking/network-policies/)


Create a network policy to allow traffic from the Internal application only to the payroll-service and db-service.

Use the spec given below. You might want to enable ingress traffic to the pod to test your rules in the UI.

Also, ensure that you allow egress traffic to DNS ports TCP and UDP (port 53) to enable DNS resolution from the internal pod.





apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP

