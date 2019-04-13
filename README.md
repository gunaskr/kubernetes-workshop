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
- run choco install curl
- run curl --version, to verify installation
- run choco install docker-for-windows or [Docker Installation](https://docs.docker.com/docker-for-windows/install/)
- run docker --version, to verify installation.
- Enable kubernetes [Enabling Kubernetes](https://docs.docker.com/docker-for-windows/#kubernetes)
- run kubectl version, to verify installation.
- run kubectl config get-contexts
![getcontextresult](images/getcontext.PNG)

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


