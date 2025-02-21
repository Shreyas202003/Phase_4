# Phase_4
<h3>Create a Dockerfile</h3>
FROM python:3.9-slim WORKDIR /app
COPY requirements.txt /app/requirements.txt RUN pip install -r requirements.txt
COPY . /app

CMD ["python", "app.py"]



<h3>Create Kubernetes Deployment and Service</h3>
apiVersion: apps/v1 kind: Deployment metadata:
name: myapp-deployment spec:
replicas: 3 selector:
matchLabels:
app: myapp template:
metadata:
labels:
app: myapp spec:
containers:
-	name: myapp
image: <REGISTRY_URL>/<namespace>/myapp:latest ports:
-	containerPort: 5000

2.	Service YAML: To expose the application, create a service.yaml file:
yaml apiVersion: v1 kind: Service metadata:
name: myapp-service spec:
selector:
app: myapp ports:
- protocol: TCP port: 80
targetPort: 5000 type: LoadBalancer

3.	Deploy to Kubernetes: Apply the YAML files to deploy your application:
kubectl apply -f deployment.yaml kubectl apply -f service.yaml

5.	Verify Deployment: To check the status of the deployment:
kubectl get pods kubectl get svc


<h3>Automating the Deployment with CI/CD Pipeline</h3>
4.1	Integrating with IBM Cloud Continuous Delivery

1.	Create a Delivery Pipeline:
o	From the IBM Cloud Dashboard, navigate to Continuous Delivery. 
o Create a new pipeline that will automatically build and deploy the containerized application to your Kubernetes cluster whenever a change is pushed to your GitHub repository.

2.	Pipeline Configuration:
o	Step 1: Add a Build stage to build the Docker image using the Dockerfile in your repository.
o	Step 2: Add a Deploy stage to deploy the image to your IBM Kubernetes 
cluster using kubectl.

4.	Trigger the Pipeline:
o	Set up the pipeline to trigger on code commits to the repository (e.g., via GitHub webhook).

5.	User Interface Development for Monitoring and Management

To monitor and manage your Kubernetes deployments, consider integrating tools like IBM Cloud Monitoring or Prometheus with Grafana for custom dashboards.
1.	Set Up IBM Cloud Monitoring:
Install Prometheus and Grafana using Helm* bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts helm repo add grafana https://grafana.github.io/helm-charts
helm install prometheus prometheus-community/prometheus helm install grafana grafana/grafana
2.	Prometheus and Grafana:
bash
minikube service grafana
- Default credentials: admin/admin

6.	IBM Cloud Platform Features and Considerations

This phase successfully integrates IBM Cloud Kubernetes Service (IKS) and IBM Cloud Container Registry (ICR) for deploying and managing containerized applications using a multi-cloud strategy. The CI/CD pipeline automates the build, test, and deployment processes, ensuring efficient and scalable application delivery.

