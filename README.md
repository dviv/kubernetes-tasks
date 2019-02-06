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

