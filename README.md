# Udagram Instagram Mock Up

Udagram is a simple cloud application developed mocking the functionality of instagram. It allows users to register and log into a web client, post photos to the feed.

The project is split into three parts:
1. [The Simple Frontend](/frontend) a basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/restapi-user), a Node-Express user microservice.
3. [The Microservice Deployment](/deployment), a travis CI based CI/CD pipeline which build and deployes the containerized application on a AWS kubernetes cluster.

## Deployment Setup

1. The containerized application is deployed to AWS EKS 
2. The following environment variables have to be set in travis CI's environment variables
    2.1. TPF_POSTGRESS_USERNAME - base64 encoded postgress_username of the AWS RDS
    2.2. TPF_POSTGRESS_PASSWORD - base64 encoded postgress_password of the AWS RDS
    2.3. TPF_AWS_CREDENTIALS - base64 encoded aws credentials for the S3 bucket uses in the backend
    2.4.  TPF_AWS_ACCESS_KEY_ID - plain text credentials for IAM role created AWS EKS
    2.5.  TPF_AWS_SECRET_ACCESS_KEY - plain text credentials for IAM role created AWS EKS
    2.6.  KUBE_CA_CERT - certificate for accessing EKS
    2.7.  DOCKER_USERNAME - username to docker hub
    2.8.  DOCKER_PASSWORD - password to docker hub
3. Release version of the containerized microservices can be set by increasing major.minor.patch number in version file located in the root of the directory
4. The build job runs on a sucessfull merge on master_dev
5. The travis CI pipeline is configured to collectively release new images of the microservices to docker hub taging each newly released image with the version number and additionally with latest tag
6. The containerized application running on the images with the latest tag is then deployed to EKS by first configuring kubectl to access the cluster
7. secrets and env variables are injected to the kubernetes cluster
8. The frontend is exposed via load balancer to public access
9. The backend uses a nginx proxy which is exposed via load balancer to the frontend and to the public
10. New versions are deployed using a rolling update in the travis CI pipeline
11. A/B deployment of the microservice xxx is possible by locally changing the name and image version in the file udacity-c3-deployment/k8s/xxx-deployment.yaml but leaving the selector name constant. A example for the frontend is provided in udacity-c3-deployment/k8s/frontendB-deployment.yaml


