# 🌦️ WeatherKube

**WeatherKube** is a containerized weather application designed to run on a Kubernetes cluster using [`kind`](https://kind.sigs.k8s.io/). It fetches and displays real-time weather data, showcasing microservice-based deployment, Kubernetes networking, and Ingress configuration.

---

## 📦 Table of Contents

- [🛠️ Setting Up kind Cluster](#️-setting-up-kind-cluster)
- [🚀 Getting Started](#-getting-started)
- [⚙️ Architecture](#️-architecture)
- [📂 Folder Structure](#-folder-structure)
- [🔒 Environment Variables](#-environment-variables)
- [📸 Screenshots](#-screenshots)
- [📄 License](#-license)

---

## 🛠️ Setting Up kind Cluster

Before deploying WeatherKube, you need to set up a local Kubernetes cluster using [`kind`](https://kind.sigs.k8s.io/).

Follow the official guide here:  
👉 [Setting up kind with Ingress](https://kind.sigs.k8s.io/docs/user/ingress/)

This guide will help you:
- Install `kind`
- Create a local cluster
- Enable ingress to route traffic to the weather service

Make sure Docker is running on your machine before you begin.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/WeatherKube.git
cd WeatherKube
```

# ⚙️ Architecture

### 1. Deploy to Kubernetes

- Apply Kubernetes Manifests
- Navigate to the k8s folder and apply each YAML file to your Kubernetes cluster. These files define the deployments, services, and other resources needed for the WeatherKube app.

A. MySQL StatefulSet for Authentication:

First, deploy the MySQL StatefulSet and Headless service, which will create the necessary MySQL pod:

```bash
kubectl apply -f k8s/authentication/mysql/statefulset_mysql.yaml -f k8s/authentication/mysql/headless_service.yaml
```
Note: After deploying the MySQL StatefulSet, run the mysql-init job to initialize the database.

```bash
kubectl apply -f k8s/authentication/mysql/mysql_init_job.yaml
```
This will initialize the MySQL database and create the necessary tables for the authentication service.

B. Authentication Service Deployment & Service:

 ```bash
kubectl apply -f k8s/authentication/auth-deployment.yaml
kubectl apply -f k8s/authentication/auth-service.yaml
```

C. Weather App Deployment & Service:

```bash
kubectl apply -f k8s/weather_app/weatherapp_deployment.yaml
kubectl apply -f k8s/weather_app/weatherapp_service.yaml
```
D. UI Deployment & Service:

```bash
kubectl apply -f k8s/UI/UI_deployment.yaml
kubectl apply -f k8s/UI/UI_service.yaml
kubectl apply -f k8s/UI/ingress.yaml
```



