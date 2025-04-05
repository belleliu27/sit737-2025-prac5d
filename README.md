```
# SIT737/323 Task 5.2D: Dockerization - Publishing the Microservice into the Cloud

## Overview

This project demonstrates how to containerize a simple web application and publish it to a **private container registry** on **Google Cloud**.

The task continues from 5.1P and covers:
- Authenticating with Google Cloud
- Creating a Docker image
- Pushing the image to **Artifact Registry**
- Running the image from the cloud

---

## Tech Stack

- Node.js
- Docker
- Google Cloud Platform (GCP)
- Artifact Registry
- GitHub

---

## Prerequisites

- Google Cloud SDK installed and configured
- A Google Cloud project with **billing enabled**
- Permissions to enable services and push to Artifact Registry
- Docker installed locally

---

## Step-by-Step Instructions

### 1. Authenticate with Google Cloud

```bash
gcloud auth login
gcloud auth configure-docker australia-southeast2-docker.pkg.dev
```

### 2. Set Your Project and Region

```bash
gcloud config set project sit737-455908
gcloud config set compute/region australia-southeast2
```

### 3. Enable Required Services

> ⚠️ You must have the required permissions on the GCP project.

```bash
gcloud services enable artifactregistry.googleapis.com
```

### 4. Create Artifact Registry (one-time setup)

```bash
gcloud artifacts repositories create my-docker-repo \
  --repository-format=docker \
  --location=australia-southeast2 \
  --description="My Docker Repo"
```

### 5. Build Docker Image

```bash
docker build -t simple-app .
```

### 6. Tag Image for GCP

```bash
docker tag simple-app australia-southeast2-docker.pkg.dev/sit737-455908/my-docker-repo/simple-app
```

### 7. Push Image to GCP Artifact Registry

```bash
docker push australia-southeast2-docker.pkg.dev/sit737-455908/my-docker-repo/simple-app
```

### 8. Verify Image Upload

```bash
gcloud artifacts docker images list \
  australia-southeast2-docker.pkg.dev/sit737-455908/my-docker-repo
```

### 9. Run the Image from Cloud

```bash
docker run -d -p 8080:8080 australia-southeast2-docker.pkg.dev/sit737-455908/my-docker-repo/simple-app
```

Visit: [http://localhost:8080](http://localhost:8080)

---

## Repository Structure

```
.
├── Dockerfile
├── index.js
├── package.json
└── README.md
```

---

## GitHub Repository

🔗 https://github.com/belleliu27/sit737-2025-prac5d

---

## Author

- **Zhaojun Liu**
- Deakin University – SIT737/SIT323 Cloud Native Application Development
```
