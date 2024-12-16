Go Application Deployment on Kubernetes with Argo CD and GitHub Actions

This repository documents the process of deploying a Go-based application on Kubernetes using Argo CD for GitOps continuous delivery and GitHub Actions for CI/CD. Below are the detailed steps performed during the project.

Project Overview

The project demonstrates how to:

Build and test a Go application locally.

Containerize the application using Docker.

Deploy the application on Kubernetes using Helm charts.

Automate CI/CD with GitHub Actions.

Use Argo CD to manage Kubernetes deployments via GitOps.

Ensure the application is accessible via a domain name.

Prerequisites

Go installed locally.

Docker installed and configured.

Kubernetes cluster (AWS EKS used in this project).

Helm installed.

Argo CD installed on the Kubernetes cluster.

Domain name for application ingress.

Steps Performed

1. Run Go Application Locally

Verified the Go application runs successfully using:

go run main.go

Ensured the application is functional locally.

2. Dockerize the Application

Wrote a Dockerfile to containerize the Go application.

Built and ran the Docker image:

docker build -t go-web-app:latest .
docker run -p 8080:8080 go-web-app:latest

Verified the application is functional within the Docker container.

3. Create Kubernetes Manifest Files

Wrote the following Kubernetes manifests:

deployment.yaml: Defines the deployment for the application.

service.yaml: Exposes the application as a service within the cluster.

ingress.yaml: Configures ingress to access the application via a domain name.

4. Helm Chart Creation

Consolidated the Kubernetes manifests into a Helm chart.

Added a values.yaml file to parameterize configurations (e.g., image tag).

5. CI/CD with GitHub Actions

Wrote a GitHub Actions pipeline to automate CI/CD tasks:

Build and Test: Build and test the Go application.

Code Quality Check: Ensure code meets quality standards using linters.

Docker Image Push: Push the Docker image to Docker Hub with proper tagging.

Helm Chart Update: Update the Helm chart values.yaml with the new Docker image tag.

6. Create EKS Cluster

Created an Amazon EKS cluster to host the application.

Configured kubectl to interact with the cluster.

7. Install Ingress Controller and Argo CD

Installed an ingress controller (e.g., NGINX ingress) on the EKS cluster.

Installed Argo CD for GitOps-based continuous delivery.

8. Execute GitHub Actions Pipeline

Ran the GitHub Actions pipeline to:

Build and push the Docker image.

Update the Helm chart with the new image tag.

9. Deploy Application with Argo CD

Created an Argo CD application using the Helm chart.

Synced the Argo CD application to deploy the Go application on the EKS cluster.

10. Verify Application Accessibility

Accessed the Go application externally via the configured domain name.

Repository Structure

.
├── Dockerfile               # Dockerfile for building the application image
├── helm/                    # Helm chart for the application
│   ├── templates/           # Kubernetes manifest templates
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
│   └── values.yaml          # Helm values file
├── k8s/                     # Kubernetes manifests (if Helm is not used)
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
├── .github/workflows/       # GitHub Actions workflows
│   └── ci-cd.yaml           # CI/CD pipeline configuration
└── README.md                # Project documentation (this file)

Tools and Technologies

Programming Language: Go

Containerization: Docker

Orchestration: Kubernetes

CI/CD: GitHub Actions

GitOps: Argo CD

Cloud Provider: AWS (EKS)

Package Manager: Helm

How to Run

1. Run Locally

Clone the repository and navigate to the project directory.

Run the application locally:

go run main.go

2. Build and Run Docker Container

Build the Docker image:

docker build -t go-web-app:latest .

Run the Docker container:

docker run -p 8080:8080 go-web-app:latest

Access the application at http://localhost:8080.

3. Deploy on Kubernetes

Apply the Helm chart:

helm install go-web-app helm/

Access the application using the configured domain name.

CI/CD Pipeline

The GitHub Actions pipeline automates the following steps:

Build and test the application.

Perform code quality checks.

Build and push the Docker image to Docker Hub.

Update the Helm chart with the new image tag.

GitOps Deployment with Argo CD

Install Argo CD on the Kubernetes cluster.

Create an Argo CD application linked to this repository and Helm chart.

Sync the application in Argo CD to deploy the Go application.

Accessing the Application

Once deployed, the application is accessible via the domain name configured in the ingress.
