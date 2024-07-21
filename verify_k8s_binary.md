# Verify K8S binary before installing the same

## Download k8s binary to /opt 

`wget -O /opt/kubernetes.tar.gz https://dl.k8s.io/v1.30.0/kubernetes.tar.gz`

## Check the integrity 

`shasum -a512 /opt/kubernetes.tar.gz`

or

`sha512sum /opt/kubernetes.tar.gz`


## To check whether download file is intact 

`shasum -a512 /opt/kubernetes.tar.gz`

Comparte the sum which is mentioned in the (https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.30.md#v1300)
I am using 1.30 version hence the above link works othrwise check (https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/)
