---
layout: default
title: "Home"
---

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
- **Monitoring Pod**: [View Configuration](/kubernetes-portfolio/yml-pages/monitoring-pod.html)
- **NGINX ConfigMap**: [View Configuration](/kubernetes-portfolio/yml-pages/nginx-configmap.html)
- **NGINX Reverse Proxy**: [View Configuration](/kubernetes-portfolio/yml-pages/nginx-reverse-proxy.html)
- **Persistent Volume**: [View Configuration](/kubernetes-portfolio/yml-pages/persistent-volume.html)
- **Persistent Volume Claim**: [View Configuration](/kubernetes-portfolio/yml-pages/persistent-volume-claim.html)
- **PrenticeOps Kubernetes Dashboard**: [View Configuration](/kubernetes-portfolio/yml-pages/kubernetes-dash.html)
- **Prometheus Config**: [View Configuration](/kubernetes-portfolio/yml-pages/prometheus-config.html)
- **Prometheus Service**: [View Configuration](/kubernetes-portfolio/yml-pages/prometheus-service.html)
- **Grafana**: Installed via Helm for visualizing metrics collected by Prometheus.
- **Traffic Backup Pod**: [View Configuration](/kubernetes-portfolio/yml-pages/traffic-backup.html)
- **Traffic Backup Service**: [View Configuration](/kubernetes-portfolio/yml-pages/traffic-backup-service.html)
- **Traffic Collector Pod**: [View Configuration](/kubernetes-portfolio/yml-pages/traffic-collector.html)
- **Traffic Collector Service**: [View Configuration](/kubernetes-portfolio/yml-pages/traffic-collector-service.html)

## Project Architecture
![Project Architecture](/kubernetes-portfolio/images/diagram.png)

[View Full Architecture Overview](/kubernetes-portfolio/architecture.md)

## Setup Guide
To set up the cluster, follow the [Setup Guide](/kubernetes-portfolio/setup.md).

## Screenshots
![Grafana Dashboard](/kubernetes-portfolio/images/grafana-dashboard.png)

## Future Enhancements
- Jenkins CI/CD pipeline for automated configuration updates.
- Alertmanager for comprehensive alerting.
