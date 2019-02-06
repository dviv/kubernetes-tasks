# Guestbook application on Kubernetes

This directory contains the source code and Kubernetes manifests for PHP
Guestbook application.

Follow the tutorial at https://kubernetes.io/docs/tutorials/stateless-application/guestbook/.

## Objectives
- Start up a Redis master.
- Start up Redis slaves.
- Start up the guestbook frontend.
- Expose and view the Frontend Service.
- Clean up

## Before you begin
You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster. If you do not already have a cluster, you can create one by using Minikube, or you can use one of these Kubernetes playgrounds:

- [Katacoda](https://www.katacoda.com/courses/kubernetes/playground)
- [Play with Kubernetes](https://https://labs.play-with-k8s.com/)



## Start up the Redis Master
Apply the Redis Master Deployment from the redis-master-deployment.yaml file:
```
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/redis-master-deployment.yaml
```

## Creating the Redis Master Service
Apply the Redis Master Deployment from the redis-master-service.yaml file:
```
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/redis-master-service.yaml
```

## Start up the Redis Slaves
Creating the Redis Slave Deployment
Deployments scale based off of the configurations set in the manifest file. In this case, the Deployment object specifies two replicas.
Apply the Redis Slave Deployment from the redis-slave-deployment.yaml file:
```
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/redis-slave-deployment.yaml
```

## Creating the Redis Slave Service
Apply the Redis Slave Service from the following redis-slave-service.yaml file:
```
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/redis-slave-service.yaml
```

## Set up and Expose the Guestbook Frontend
The guestbook application has a web frontend serving the HTTP requests written in PHP. It is configured to connect to the redis-master Service for write requests and the redis-slave service for Read requests

Apply the frontend Deployment from the frontend-deployment.yaml file:
```
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/frontend-deployment.yaml
```
Query the list of Pods to verify that the three frontend replicas are running:
```
  kubectl get pods -l app=guestbook -l tier=frontend
```
The response should be similar to this:
```
  NAME                        READY     STATUS    RESTARTS   AGE
  frontend-3823415956-dsvc5   1/1       Running   0          54s
  frontend-3823415956-k22zn   1/1       Running   0          54s
  frontend-3823415956-w9gbt   1/1       Running   0          54s
```

## Creating the Frontend Service
Apply the frontend Service from the frontend-service.yaml file:
```  
  kubectl apply -f https://raw.githubusercontent.com/dviv/kubernetes-tasks/master/guestbook/frontend-service.yaml
```
Query the list of Services to verify that the frontend Service is running:
```
  kubectl get services 
```
The response should be similar to this:
```
  NAME           TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
  frontend       ClusterIP   10.0.0.112   <none>       80:31323/TCP   6s
  kubernetes     ClusterIP   10.0.0.1     <none>        443/TCP        4m
  redis-master   ClusterIP   10.0.0.151   <none>        6379/TCP       2m
  redis-slave    ClusterIP   10.0.0.223   <none>        6379/TCP       1m
```
## Cleaning up
Run the following commands to delete all Pods, Deployments, and Services.
```
  kubectl delete deployment -l app=redis
  kubectl delete service -l app=redis
  kubectl delete deployment -l app=guestbook
  kubectl delete service -l app=guestbook
```
Query the list of Pods to verify that no Pods are running:

```
  kubectl get pods
```
The response should be this:
```
  No resources found.
```
