Task 2 - Kubernetes Deployment
Overview

The Java backend application from Task 1 was containerized using Docker and deployed to a Kubernetes cluster along with MongoDB.

Technologies Used

Docker

Kubernetes (Minikube or Docker Desktop)

Helm for MongoDB deployment

Implementation Details

Created a Dockerfile for the Spring Boot application.

Built and pushed the image to Docker Hub.

Created Kubernetes manifests for deployment and service.

Configured MongoDB deployment and service.

Added persistent volume and persistent volume claim for MongoDB data storage.

Modified the TaskExecution endpoint to create and run a new Kubernetes pod using the Kubernetes API to execute commands inside a BusyBox container.

Validation

The setup was verified using the following commands:

kubectl get pods

kubectl get svc

curl http://<NodeIP>:<NodePort>/tasks
