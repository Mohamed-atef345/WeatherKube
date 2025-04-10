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
