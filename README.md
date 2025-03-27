# DevOps Assignment - Log Collection and Visualization Pipeline

This repository implements a log collection and visualization pipeline using Loki and Promtail.

## How to Run

1. Clone the repository.
2. Build the Docker images for Loki and Promtail using the Jenkins pipeline.
3. Apply the Kubernetes configurations using Minikube.

## Files

- **Dockerfile.loki**: Builds the Loki image.
- **Dockerfile.promtail**: Builds the Promtail image.
- **loki-config.yml**: Loki configuration file.
- **promtail-config.yml**: Promtail configuration file.
- **Jenkinsfile**: Jenkins pipeline file.
