# Library Application Kubernetes Deployment

This repository contains Kubernetes configuration files for deploying a multi-tier Library application with a database, backend service, and frontend web service.

## Overview

The deployment architecture consists of the following components:

1. **Database (Postgres)** - Managed by a StatefulSet with persistent storage.
2. **Backend Service** - Deployed as a Deployment, connecting to the database and exposing an API for the web service.
3. **Frontend Web Service** - Deployed as a Deployment, connecting to the backend API.
4. **Networking and Security** - Configured using ClusterIP services, Network Policies, and Secrets for secure communication and storage.

## Components

### 1. Database Service

- **Service**: A ClusterIP service without a specific IP, used for internal database communication.
- **StatefulSet**: Ensures persistent storage using a `PersistentVolumeClaim` and scales replicas as needed.

### 2. Backend Service

- **Deployment**: Uses a rolling update strategy for zero-downtime deployment.
- **Service**: Exposes the backend API on port 8000 within the cluster.

### 3. Frontend Web Service

- **Deployment**: Runs two replicas of the web service with a rolling update strategy.
- **Service**: Exposes the frontend to the internet via a LoadBalancer.

### 4. Configurations and Secrets

- **ConfigMap**: Stores environment variables for the web service.
- **Secrets**: Securely stores database credentials and other sensitive data.

### 5. Network Policies

- **Database Network Policy**: Restricts access to the database to only the backend service.
- **Backend Network Policy**: Allows only frontend services within a specific namespace to connect to the backend.

---

## Getting Started

1. Clone the repository.
2. Apply the configurations using `kubectl apply -f <file-name>.yaml`.

## Notes

- Ensure that the necessary secrets and ConfigMap are in place for your environment variables.
- Adjust replica counts and resource limits based on your cluster's capacity.
