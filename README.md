# carts service
This repository contains Kubernetes manifests and a Jenkins pipeline for 
### building, 
### running, 
### pushing, 
and deploying the carts service.

## Service Manifest

The carts service is defined in the following Kubernetes manifest file:
This manifest describes a Kubernetes Service named carts that selects pods labeled with app: 

## carts-deployment. 

The service is exposed on port 80 using the TCP protocol.

## Jenkins Pipeline
The Jenkins pipeline automates the following stages:

## Build

Builds the Docker image for the carts service.
Uses Docker commands to build the image with the specified tag.

## Run

Creates a Docker network for the build.
Runs the carts service in a detached mode with the Docker image.
Stops the running service and removes the Docker network.

## Push

Tags the Docker image for the carts service.
Logs in to Docker Hub using provided credentials.
Pushes the Docker image to the Docker Hub repository with both the specified tag and the "latest" tag.

## Deploy EKS

Configures AWS credentials and sets up AWS CLI.
Updates the Kubernetes configuration for Amazon EKS (kubeconfig).
Applies Kubernetes manifests located in the ./manifests directory to the specified namespace.
The AWS credentials, EKS cluster information, and Kubernetes configuration are retrieved from Jenkins credentials.

## Pipeline Environment Variables

The pipeline uses the following environment variables:

 `000000` DOCKER_ID: Docker Hub username.
 `000000` DOCKER_IMAGE_CARTS: Docker image name for the carts service.
 `000000` DOCKER_TAG: Docker image tag, derived from the Jenkins build ID.
 `000000` BUILD_AGENT: Build agent information (empty for now).
 `000000` NAMESPACE: Kubernetes namespace, retrieved from Jenkins credentials.
 `000000` DOCKER_PASS: Docker Hub password, retrieved from Jenkins credentials.
 `000000` KUBECONFIG: Kubernetes configuration for Amazon EKS, retrieved from Jenkins credentials.
 `000000` AWSKEY, AWSSECRETKEY, AWSREGION, EKSCLUSTERNAME: AWS and EKS configuration details, retrieved from Jenkins credentials.

Configure the Jenkins pipeline with the required credentials and execute the pipeline.
