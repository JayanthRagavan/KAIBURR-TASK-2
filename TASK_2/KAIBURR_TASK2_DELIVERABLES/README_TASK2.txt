KAIBURR Task 2 - Kubernetes deliverables
----------------------------------------
Files included:
- Dockerfile
- k8s/namespace.yaml
- k8s/task1-deployment.yaml
- k8s/task1-service-nodeport.yaml
- k8s/mongo-service.yaml
- k8s/mongo-statefulset.yaml
- patch/TaskService-k8s-exec.patch (Java code patch to replace local shell execution with Kubernetes Pod execution)
- pom.fabric8.xml (a small pom.xml fragment showing required dependency)

Quick run (Docker Desktop or Kind):
1. Build the Docker image locally (Docker Desktop or kind with local registry):
   docker build -t task1-api:latest -f Dockerfile .

2. Apply manifests:
   kubectl apply -f k8s/namespace.yaml
   kubectl apply -f k8s/mongo-statefulset.yaml
   kubectl apply -f k8s/mongo-service.yaml
   kubectl apply -f k8s/task1-deployment.yaml
   kubectl apply -f k8s/task1-service-nodeport.yaml

3. Verify:
   kubectl get pods -n kaiburr-assessment
   kubectl get pvc -n kaiburr-assessment

4. From host, call the API:
   curl http://localhost:30080/tasks

Notes:
- The MongoDB StatefulSet uses a PersistentVolumeClaim (volumeClaimTemplates) so data persists if the mongo pod is deleted.
- The application reads MongoDB uri from SPRING_DATA_MONGODB_URI environment variable (set in the deployment).
- If using kind, you may need to load the image into the kind cluster:
   kind load docker-image task1-api:latest --name <your-kind-cluster-name>
