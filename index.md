# Home Kubernetes Cluster for Network Monitoring and Automation

Welcome to the documentation for my home Kubernetes cluster project, where I’ve built a system for monitoring network traffic, storing data, and visualizing network metrics.

## Project Overview
This project involves deploying a Kubernetes cluster to capture network traffic using `tcpdump`, securely accessing it through an NGINX reverse proxy, and visualizing data using Prometheus and Grafana.

## Technologies Used
- **Kubernetes** for orchestration
- **Docker** for containerization
- **NGINX** for reverse proxying
- **Prometheus** & **Grafana** for monitoring
- **Ansible** for automation

## Key Components
- **Monitoring Pod**: [View Configuration](./configs/monitoring-pod.yml)
- **NGINX Reverse Proxy**: [View Configuration](./configs/nginx-reverse-proxy.yml)
- **Prometheus Service**: [View Configuration](./configs/prometheus-service.yml)

## Project Architecture
![Project Architecture](./images/architecture-diagram.png)  <!-- You can upload an image in the repo for this -->

## Setup Guide
To set up the cluster, follow the [Setup Guide](./setup.md).

## Screenshots
![Grafana Dashboard](./images/grafana-dashboard.png)  <!-- Add a Grafana screenshot for demo purposes -->

## Future Enhancements
- Jenkins CI/CD pipeline for automated configuration updates.
