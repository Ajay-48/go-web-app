# Go Application Deployment on Kubernetes with Argo CD and GitHub Actions

This repository documents the process of deploying a Go-based application on Kubernetes using **Argo CD** for GitOps and **GitHub Actions** for CI/CD.

## Project Overview

This project demonstrates the deployment of a Go-based application on an AWS EKS cluster using modern DevOps practices. The deployment pipeline is built with:
- **Docker** for containerization.
- **Kubernetes** for orchestration.
- **Helm** for templating Kubernetes resources.
- **Argo CD** for GitOps-based continuous delivery.
- **GitHub Actions** for continuous integration and automated workflows.

---

## Features

- Local testing and validation of the Go application.
- Dockerized Go application for portability.
- Kubernetes manifests for application deployment.
- Helm charts for streamlined Kubernetes resource management.
- CI/CD pipeline using GitHub Actions.
- GitOps-based delivery with Argo CD.
- External application access using an Ingress controller and domain name.

---

## Steps Performed

### 1. Run the Go Application Locally
- Verified the Go application by running it on the local environment.

### 2. Dockerize the Application
- Created a `Dockerfile` for the application.
- Built the Docker image:
  ```bash
  docker build -t go-web-app .
  ```
- Ran the Docker container and validated the application:
  ```bash
  docker run -p 8080:8080 go-web-app
  ```

### 3. Create Kubernetes Manifests
- Wrote Kubernetes manifest files:
  - `deployment.yaml` for deploying the application.
  - `service.yaml` to expose the application internally.
  - `ingress.yaml` for external access via a domain name.

### 4. Helm Chart Creation
- Packaged the Kubernetes manifests into a Helm chart:
  - `values.yaml` file created for configurability.

### 5. GitHub Actions Pipeline
- Configured a GitHub Actions workflow with the following steps:
  1. **Build and Test**: Compiled the Go application and ran tests.
  2. **Code Quality Check**: Ensured code adheres to standards using `golangci-lint`.
  3. **Push Docker Image**: Built and pushed the Docker image to Docker Hub with appropriate tags.
  4. **Helm Chart Update**: Updated the `values.yaml` file with the new Docker image tag.

### 6. Set Up AWS EKS Cluster
- Created an EKS cluster on AWS to host the Kubernetes deployment.

### 7. Install Ingress Controller and Argo CD
- Installed an Ingress controller to enable external access to services.
- Installed Argo CD for GitOps-based deployment.

### 8. Execute CI/CD Pipeline
- Triggered the GitHub Actions workflow, which:
  - Built and tested the application.
  - Published the Docker image to Docker Hub.
  - Updated the Helm chart with the new Docker image tag.

### 9. Deploy Application via Argo CD
- Created an Argo CD application using the prepared Helm charts.
- Configured Argo CD to monitor the Git repository and deploy the application automatically.

### 10. Access Application
- Verified that the application is deployed and accessible externally using the domain name configured in the Ingress resource.

---

## Technologies Used

- **Programming Language**: Go
- **Containerization**: Docker
- **Orchestration**: Kubernetes
- **Templating**: Helm
- **CI/CD**: GitHub Actions
- **GitOps**: Argo CD
- **Cloud Provider**: AWS (EKS)

---

## Repository Structure

```
.
├── Dockerfile                      # Docker configuration file
├── k8s/
│   ├── deployment.yaml             # Kubernetes Deployment manifest
│   ├── service.yaml                # Kubernetes Service manifest
│   ├── ingress.yaml                # Kubernetes Ingress manifest
├── helm/
│   ├── Chart.yaml                  # Helm chart metadata
│   ├── templates/                  # Kubernetes resource templates
│   └── values.yaml                 # Configurable values for the chart
├── .github/
│   └── workflows/
│       └── ci-cd.yaml              # GitHub Actions workflow
└── README.md                       # Project documentation
```

---

## How to Use

### Prerequisites
- Docker installed locally.
- Kubernetes cluster (EKS recommended).
- Helm installed locally.
- Argo CD installed and configured.

### Steps
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```
2. Run the GitHub Actions workflow to build and deploy the application:
   - Push changes to the repository to trigger the pipeline.
3. Access the application using the configured domain name.

---

## Contact
