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
- **Monitoring Pod**: [View Configuration](/configs/monitoring-pod.yml)  
  This pod captures network traffic using `tcpdump`.
  
- **NGINX ConfigMap**: [View Configuration](/configs/nginx-configmap.yml)  
  Stores NGINX configurations for reverse proxying.

- **NGINX Reverse Proxy**: [View Configuration](/configs/nginx-reverse-proxy.yml)  
  Configures NGINX as a reverse proxy to secure remote access.

- **Persistent Volume**: [View Configuration](/configs/persistent-volume.yml)  
  Defines the storage used to persist network traffic captures.

- **Persistent Volume Claim**: [View Configuration](/configs/persistent-volume-claim.yml)  
  Claims the persistent volume for use by the traffic capture and backup pods.

- **PrenticeOps Kubernetes Dashboard**: [View Configuration](/configs/prenticeops-dash.yml)  
  The Kubernetes Dashboard for managing and monitoring the cluster directly.

- **Prometheus Config**: [View Configuration](/configs/prometheus-config.yml)  
  Configures Prometheus to scrape network data from the monitoring pods.

- **Prometheus Service**: [View Configuration](/configs/prometheus-service.yml)  
  Defines the Prometheus service within the Kubernetes cluster.

- **Grafana**: Installed via Helm for visualizing metrics collected by Prometheus.

- **Traffic Backup Pod**: [View Configuration](/configs/traffic-backup.yml)  
  Handles the backup of network traffic data captured by the monitoring pod.

- **Traffic Backup Service**: [View Configuration](/configs/traffic-backup-service.yml)  
  Exposes the traffic backup pod within the cluster.

- **Traffic Collector Pod**: [View Configuration](/configs/traffic-collector.yml)  
  Collects network traffic data for analysis and backup.

- **Traffic Collector Service**: [View Configuration](/configs/traffic-collector-service.yml)  
  Exposes the traffic collector pod within the cluster.


## Project Architecture
![Project Architecture](./images/architecture-diagram.png)  <!-- You can upload an image in the repo for this -->

## Setup Guide
To set up the cluster, follow the [Setup Guide](./setup.md).

## Screenshots
![Grafana Dashboard](./images/grafana-dashboard.png)  <!-- Add a Grafana screenshot for demo purposes -->

## Future Enhancements
- Jenkins CI/CD pipeline for automated configuration updates.
