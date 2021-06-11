# Mediawiki Setup using Helm on Kubernetes




Setup is done to run on local setup of kubernetes using helm

Image used is the official dockerhub image of mediawiki
https://hub.docker.com/_/mediawiki

##### A manual image can be created using Dockerfile envs can be used for application variables.


Closne the repo and run the below command
```sh
helm install mediawiki ./mediawiki
```

Create Image pull secret which will be used to pull the image from the dockerhub
```sh
kubectl create secret docker-registry mediawiki-dockerhub --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>
```
We can store it in secret server during cloud deployment

The helm chart creates the below resources:
* Storeage Class
* Persistence Volume
* Claims
* Horizontal Pod Autoscaler 

## Running on Cloud provider
Helm chart has to be updated accordingly to run on specific cloud.
Example:
Azure

Resources which has to be updated
Persistence volume(Azure File): azurefile can be used as the Persistence volume plugin

Update Strategy used is Rolling

Scalling the Application

Hpa is enabled to scale at 80% with the reques and limits as defined below
```sh
resources
  limits:
    cpu: 100mf
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
```

