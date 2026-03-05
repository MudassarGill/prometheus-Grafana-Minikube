# Prometheus-Grafana-Minikube Monitoring

This project demonstrates a monitoring and alerting implementation using **FastAPI**, **Prometheus**, and **Grafana** deployed on a **Minikube** Kubernetes cluster.

## 🚀 Project Overview

The application is a Python-based FastAPI service that exposes custom metrics for Prometheus scraping. It tracks:
- **Total API Requests**: A counter for all hits to the `/metrics` endpoint.
- **Request Processing Latency**: A gauge simulating response times.
- **Model Success Rate**: A gauge simulating machine learning model performance.

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:
- [Docker](https://www.docker.com/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- Python 3.9+ (for local development)

## 📂 Project Structure

- `app.py`: The FastAPI application with custom Prometheus metrics.
- `Dockerfile`: Containerization setup for the FastAPI app.
- `deployment.yaml`: Kubernetes Deployment and Service definitions (NodePort).
- `README.md`: Project documentation.

## ⚙️ Setup & Deployment

### 1. Build the Docker Image
To build the image manually:
```bash
docker build -t fastapi-metrics-app:latest .
```

### 2. Deploy to Minikube
Ensure Minikube is running and use the local Docker daemon:
```bash
minikube start
eval $(minikube docker-env) # On Windows use: minikube docker-env | Invoke-Expression
kubectl apply -f deployment.yaml
```

### 3. Access the Application
The application is exposed via a NodePort on port `30007`. Get the URL:
```bash
minikube service fastapi-metrics-app --url
```
Access the metrics endpoint at `/metrics`.

## 📊 Monitoring with Prometheus

The `deployment.yaml` also includes a service definition for Prometheus (NodePort `30008`). You can track the following custom metrics:
- `total_api_requests_total`
- `request_processing_latency_seconds`
- `model_prediction_success_rate`

## ⚖️ Resource Management
The deployment is configured with resource requests and limits to ensure stability:
- **Requests**: 100m CPU, 32Mi Memory
- **Limits**: 200m CPU, 64Mi Memory
