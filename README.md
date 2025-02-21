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
4.	Verify Deployment: To check the status of the deployment:
kubectl get pods kubectl get svc
