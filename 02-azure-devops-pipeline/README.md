# Azure DevOps Pipeline - Flask API

CI/CD pipeline for the Flask API from project 01, built using Azure
DevOps. The focus of this project is the pipeline itself rather than
the application - specifically, enforcing a code quality gate before
any deployment happens.

## Pipeline

1. Build - Docker image built from the Flask API source
2. Scan - SonarQube static analysis with a quality gate. The pipeline
   fails at this stage if code quality thresholds are not met, before
   the image is pushed anywhere
3. Push - Image pushed to Azure Container Registry
4. Deploy - Azure App Service pulls the updated image and restarts
   the container

## Why this setup

Most personal DevOps projects stop at "build and deploy." This one
adds the piece that matters in a production environment: nothing
reaches deployment without passing a quality/security check first.
That's the same shape used in real enterprise pipelines, just at a
smaller scale.

## Tools

Azure DevOps, Docker, SonarQube, Azure Container Registry, Azure App
Service, Azure Key Vault (for pipeline secrets)

## Notes

Reuses the Flask API from 01-dockerized-api rather than a new
application, since the goal here is the CI/CD flow, not the app
logic.
