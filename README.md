# Learning Kubernetes (k8s)

This repository is a hands-on learning project for understanding the basic building blocks of Kubernetes using YAML manifests and simple examples.

The goal is to practice common Kubernetes concepts such as Pods, Deployments, Services, ConfigMaps, and Secrets in a beginner-friendly structure.

---

## Repository Overview

The project is organized into folders based on learning stages:

- `01-basics` - covers foundational Kubernetes resources and networking basics
- `02-app` - reserved for application deployment exercises and more advanced examples

---

## Folder-wise Explanation

### 1. `01-basics`

This folder contains the core Kubernetes manifest files used to understand the most important objects in a cluster.

#### `pod.yml`
This file defines a single Kubernetes Pod.

- `kind: Pod` means a pod is the smallest deployable unit in Kubernetes
- A pod can run one or more containers
- In this example, an `nginx` container is created and exposed on port `80`

Use this file to learn:
- how to declare a pod
- how to specify a container image
- how to define container ports

#### `deployment.yml`
This file defines a Kubernetes Deployment.

- `kind: Deployment` is used for managing replicas of an application
- `replicas: 2` ensures two pod instances are running
- the selector matches pods with the label `app: nginx`
- the template defines the pod specification created by the deployment

Use this file to learn:
- scaling and replica management
- declarative updates
- how deployments maintain desired pod state

#### `service.yml`
This file creates a Kubernetes Service of type `ClusterIP`.

- a Service exposes pods internally inside the cluster
- it selects pods using the `selector` field
- traffic on port `80` is forwarded to pod port `80`

Use this file to learn:
- service discovery
- internal communication within the cluster
- how applications connect to pods using stable service endpoints

#### `service-nodeport.yml`
This file defines a Service of type `NodePort`.

- `NodePort` exposes the app on a static port across each node in the cluster
- `nodePort: 30080` makes the app reachable externally on the node IP
- it is useful for learning how Kubernetes exposes services outside the cluster

Use this file to learn:
- external access patterns
- node-based service exposure
- difference between internal and external service access

#### `configmap.yml`
This file creates a ConfigMap.

- ConfigMaps store non-sensitive configuration data in key-value pairs
- environment variables are injected into applications through config values
- here, settings like `APP_MODE`, `APP_COLOR`, and `APP_TIMEOUT` are defined

Use this file to learn:
- separating configuration from application code
- storing environment-specific settings
- better configuration management in Kubernetes

#### `secrets.yml`
This file defines a Kubernetes Secret.

- Secrets are used to store sensitive information like passwords and tokens
- the values are base64-encoded in this example
- `type: Opaque` means the secret contains arbitrary key-value data

Use this file to learn:
- storing credentials securely
- managing sensitive application data
- difference between ConfigMap and Secret

---

### 2. `02-app`

This folder is used for more realistic application deployment scenarios, where Kubernetes resources are combined to run an app and its database together.

#### `deployment-service-db.yaml`
This file demonstrates a simple application stack using a database container managed by a Deployment.

- it creates a Deployment named `flask-db`
- the pod runs a MySQL container on port `3306`
- the label `app: flask-db` is used so traffic can be matched to the correct pod
- database settings are loaded from configuration and secret resources using environment variables

Important details in this example:
- `MYSQL_DATABASE` is taken from a ConfigMap value named `DB_HOST`
- `MYSQL_USER` and `MYSQL_PASSWORD` are taken from a Secret named `app-secret`
- this shows how Kubernetes separates configuration from secrets
- it also demonstrates the idea that applications should receive environment-based configuration rather than hardcoded values

This example helps you understand:
- how an app and database are deployed together
- how Services connect to workloads using labels and selectors
- how environment variables are injected into containers
- how configuration data and credentials are managed in a real Kubernetes setup
- how a simple application stack can be represented in YAML

#### `config-map-dbinit.yaml`
This file creates a ConfigMap that stores an SQL initialization script for the database.

- the ConfigMap is named `db-init-sql`
- it includes a key called `init.sql`
- the SQL script creates a database named `mydb`
- it also creates a table called `users` and inserts sample records

This is useful for learning:
- how to initialize database schema automatically on startup
- how to manage SQL scripts as Kubernetes config objects
- how a database can be prepared with seed data during setup

Typical examples that may go here include:
- application + database deployment patterns
- frontend and backend examples
- multi-container app setup
- ingress and networking examples
- database connection setup

---

## Learning Flow

A beginner-friendly order to study this repository is:

1. Start with `pod.yml` to understand a basic container running inside a pod
2. Move to `deployment.yml` to learn replication and scaling
3. Study `service.yml` and `service-nodeport.yml` to understand networking and service exposure
4. Learn config handling using `configmap.yml`
5. Learn secret management using `secrets.yml`
6. Expand into app-level deployment exercises in `02-app`

---

## Common Kubernetes Commands

These are useful commands while learning from this repository:

```bash
kubectl apply -f 01-basics/pod.yml
kubectl apply -f 01-basics/deployment.yml
kubectl apply -f 01-basics/service.yml
kubectl apply -f 01-basics/configmap.yml
kubectl apply -f 01-basics/secrets.yml

kubectl get pods
kubectl get deployments
kubectl get services
kubectl get configmap
kubectl get secrets

kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

---

## Notes

This project is designed for learning and experimentation. It focuses on the most common Kubernetes primitives used in beginner and intermediate Kubernetes workflows.

As you progress, you can extend this repository with:
- different application workloads
- Ingress examples
- Helm charts
- namespace examples
- real-world microservice architecture demos

---

## Summary

This repository is a simple Kubernetes learning playground that introduces:

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets

These are the foundational resources needed to understand how Kubernetes applications are deployed and managed in real environments.
