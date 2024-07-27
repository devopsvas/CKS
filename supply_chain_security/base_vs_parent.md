# Images - Docker - Security - Best Pratices


## When an image is bult form scracth is called Base image 

```
FROM Scarch
ADD rootfs.tat.gz /
CMD ["bash"]
```

## BEST PRACTICE 


Build image which are modular, Like webserver, DB, etc 

Containers can forma single application, Each componenets can be sacaled upand down as requeired

Don't store data or state in a container 


All those  data should be stired in external volume or Cache called Redis 


## Choosing a Base Image 


Images with :Offical tag". "" Indicate that image is from offical sources 


Slim and Minimal images are good, It will allow to pull more images , try to use them as Base images 


## Using private repositiry in K8S

Create a new repository and create secret using 

# kubectl create secret docker-registary --docker-username=<name> --docker-password=<> --docker-server=<> --docker-email=<>


Study how to include in deployment or Pod in Container


https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

