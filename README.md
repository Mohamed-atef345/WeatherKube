# 🌦️ WeatherKube

**WeatherKube** is a containerized weather application designed to run on a Kubernetes cluster using [`kind`](https://kind.sigs.k8s.io/). It fetches and displays real-time weather data, showcasing microservice-based deployment, Kubernetes networking, and Ingress configuration.

---

## 📦 Table of Contents

- [🛠️ Setting Up kind Cluster](#️-setting-up-kind-cluster)
- [🚀 Getting Started](#-getting-started)
- [🔒 Environment Variables](#-environment-variables)
- [⚙️ Architecture](#️-architecture)

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

---

## 🔒 Environment Variables

The WeatherKube app requires certain secrets to be set as environment variables. These secrets are used to store sensitive information such as database passwords and API keys.

### 1. MySQL Root Password Secret

Create the MySQL root password secret using this command:

```bash
kubectl create secret generic mysql-secret \
  --from-literal=root-password=<your-password> \
  --from-literal=auth-password=<your-auth-password> \
  --from-literal=secret-key=<your-apikey>
```

- **`root-password`**: MySQL root password used by the MySQL StatefulSet.
- **`auth-password`**: The password used for user authentication.
- **`secret-key`**: A secret key for the authentication service.

### 2. Weather API Key Secret

If your app requires an external weather API, create the API key secret:

```bash
kubectl create secret generic weatherapi-key --from-literal=apikey=<your-apikey>
```

- **`apikey`**: The key for accessing the weather API.

### 3. TLS Secret for UI

To enable HTTPS for the UI, create the TLS secret:

```bash
kubectl create secret tls weatherapp-ui-tls-cert \
  --cert=k8s/UI/tls.crt \
  --key=k8s/UI/tls.key
```

- **`tls.crt`**: The TLS certificate.
- **`tls.key`**: The TLS private key.

---

## ⚙️ Architecture

The WeatherKube app follows a microservices architecture and runs on Kubernetes. It consists of several services, including:

1. **MySQL Database** (for authentication)
2. **Authentication Service** (for user login and registration)
3. **Weather API** (fetching real-time weather data)
4. **UI Service** (the front-end interface)

### 1. Deploy to Kubernetes

- **Step 1**: Apply Kubernetes Manifests

To deploy the app, apply each YAML file to your Kubernetes cluster. These files define the deployments, services, and other resources for the WeatherKube app.

```bash
kubectl apply -f k8s/authentication/mysql/statefulset_mysql.yaml
kubectl apply -f k8s/authentication/mysql/headless_service.yaml
```

**Note**: After deploying the MySQL StatefulSet, you must run the `mysql-init` job to initialize the database.

```bash
kubectl apply -f k8s/authentication/mysql/mysql_init_job.yaml
```

This will initialize the MySQL database and set up the necessary tables for the authentication service.

### 2. Authentication Service

Deploy the authentication service:

```bash
kubectl apply -f k8s/authentication/auth-deployment.yaml
kubectl apply -f k8s/authentication/auth-service.yaml
```

### 3. Weather App Service

Deploy the weather app backend:

```bash
kubectl apply -f k8s/weather_app/weatherapp_deployment.yaml
kubectl apply -f k8s/weather_app/weatherapp_service.yaml
```

### 4. UI Service

Deploy the front-end UI service:

```bash
kubectl apply -f k8s/UI/UI_deployment.yaml
kubectl apply -f k8s/UI/UI_service.yaml
kubectl apply -f k8s/UI/ingress.yaml
```

### 5. Verifying the Deployment

After deploying all components, check the status of your pods and services:

```bash
kubectl get pods
kubectl get services
kubectl get ingress
```

Ensure that all services are running and accessible.

---

By following these steps, you will have successfully set up the WeatherKube app on Kubernetes!

---