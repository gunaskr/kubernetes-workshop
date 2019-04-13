Kubernetes Workshop Overview
============================

This workshop's objective is to provide hello world experience of Kubernetes. After completion of this workshop, you should be:

- Familiar with kubectl commands
- Familiar with Kubernetes UI
- Deploy your applications into local kubernetes/ docker for windows
- Deploy your applications into aws clusters

Prerequisites
=============

In order to begin the workshop, you must have the following softwares installed in your machines.
- Chocolatey - the windows package manager [Chocolatey](https://chocolatey.org/install)
- Install and verify curl
```
    choco install curl
    curl --version
```
- Install Docker For Windows latest.
```
    choco install docker-for-windows
```
 or [Docker Installation](https://docs.docker.com/docker-for-windows/install/)/ [Docker Fro Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- verify docker installation by  
```
    docker --version
```
- Enable kubernetes [Enabling Kubernetes](https://docs.docker.com/docker-for-windows/#kubernetes). Check that the `kubectl` command is correctly configured
```
    kubectl cluster-info
```
- Signup for aws cloud. Yes, you need to give your credit card information! [SingUp Page](https://portal.aws.amazon.com/billing/signup#/start)
You are set to go!

Get Docker Image
================
For the purpose of this workshop i've already built and published an image in docker hub. We will deploy this image both in local kubernetes cluster(docker-for-windows) and in aws.
1. Pulling the required image from hub
 ```
   docker pull aguna14/label
 ```
2. Run the container
```
   docker container run -p 8080:8080 aguna14/label
```
3. Check the service
```
   curl http://localhost:8080/hello
```
5. We dont need the container running. We need to stop and remove the container. 
```
   docker container ls
```
Notice the container id from the command.
```
    docker container stop <containerid>
    docker rm <containerid>
```
To verify that the container has been removed.
```
    docker ps -a
```
It shouldn't list any processes running.

Kubernetes Context and Dashboard
================================
1. Check the contexts of the kubernetes using the following command
```
    kubectl config get-contexts
```
By default you should see docker-for-desktop as one of the context. If not check the pre-requisites. If for some reason context is not set you can set the context as follows
2. Setting the context
```
    kubectl config use-context docker-for-desktop
```
3. Setup dashboard
```
    kubectl apply -f ^
https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/alternative/kubernetes-dashboard.yaml
```
4. View the dashboard
```
    kubectl proxy
```
And navigate to your Kubernetes Dashboard at: http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy

5. Refer this link for creation of user and login [Kubebenetes Dashboard User](https://github.com/kubernetes/dashboard/wiki/Creating-sample-user)

Brief Introduction To Pods, Services and Deployments
====================================================
TBD - Introduction to Kubernetes architecture and parts.

Deploying in Local
==================
1. Go to kube-local folder.
2. Creating a service.
```
    kubectl create -f service.yml
```
3. Check if service is created
```
    kubectl get services --all-namespaces
```
4. Detailed description of the service
```
    kubectl describe service rest-example
```
5. Creating a deployment
```
    kubectl create -f deployment.yml
```
6. Description of the deployment
```
    kubectl describe deployment rest-example
```
7. Check the pods
```
    kubectl get pods
```
8. Check if the service has started by checking out the logs of the pod
```
    kubectl logs <pod name>
```
9. As the localhost becomes our external ip. You can access the deployed application like so.
```
    curl http://localhost:8080/hello
```

Deploying in Cloud
==================
TBD - Mostly what we did in local, Just that we need to provide a different context and will acess the application in a generated url.


