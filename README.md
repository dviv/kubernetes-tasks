# Guestbook application on Kubernetes

This directory contains the source code and Kubernetes manifests for PHP
Guestbook application.

Follow the tutorial at https://kubernetes.io/docs/tutorials/stateless-application/guestbook/.

## Objectives
- Create php apilication that run a guest book fronend.
- Create a REdis backend to the php apilication.
- Create a Kubernetes YAML fo run.

## How to deploy?

### Install kubectl binary using curl
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
```
Make the kubectl binary executable.
```
chmod +x ./kubectl
```
Move the binary in to your PATH.
```
sudo mv ./kubectl /usr/local/bin/kubectl
```




