Falco is threat ditection tool which is used to ditetct threat.

It used to monitor teh system calls using dedicated kernel module 


https://falco.org/docs/install-operate/installation/


Once install Falco pods running all nodes in the cluster 


## Ditecting threat 

Falco is installed as a kernel module in the node

# systemctl status falco 

## Create an NGINX 

`# kubectl run nginx --image=nginx`


## Find out on which pod flcon pods are running 


`# kubectl get pod -o wide`


## Login to the container 

`# kubectl exec -it nginx bash`


## Check the security logs created by falco 


`# Journalctl -fu falco`


## Falco rule file is a yaml file 

/etc/falco/rules.yml structure

- rule: <Name of the riule>
  desc: <Detailed description of rule>
  condition: <When to filter alerts matching the rule>
  output: <Output generated for the event>
  priority: <Severity of the event>


## Roload Falco 

cat /var/run/falco

kill -1 $(cat /var/run/falco.pid)


## Which file does falco rely on to function?

`/etc/falco/falco.yaml`



https://falco.org/docs/getting-started/installation/

https://github.com/falcosecurity/charts/tree/master/falco

https://falco.org/docs/rules/supported-fields/

https://falco.org/docs/rules/default-macros/

https://falco.org/docs/configuration/
