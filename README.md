# PrenticeOps.github.io

# Home Kubernetes Cluster for Network Monitoring and Automation

Welcome to the repository for my home Kubernetes cluster project, designed for monitoring network traffic, automating tasks, and visualizing network metrics using various tools.

This project aims to showcase my DevOps skills by utilizing Kubernetes, Docker, Prometheus, Grafana, and NGINX. The system captures, monitors, and visualizes home network data while providing a roadmap for future automation and enhancements.

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Key Components](#key-components)
- [Project Architecture](#project-architecture)
- [Setup Guide](#setup-guide)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)
- [Contact](#contact)

## Project Overview

This repository contains configurations and documentation for deploying a Kubernetes cluster for network monitoring. The system captures network traffic and provides detailed visualizations through a Grafana dashboard, while also employing automation tools like Ansible and Prometheus.

## Technologies Used

- **Kubernetes**: Orchestration of containerized applications.
- **Docker**: Containerization platform used for managing and deploying containers.
- **NGINX**: Reverse proxy for secure access to services.
- **Prometheus**: Monitoring and alerting toolkit, used to scrape network metrics.
- **Grafana**: Visualization tool for monitoring dashboards.
- **Ansible**: Automation platform for managing configurations and deployments.

## Key Components

- **Monitoring Pod**: Captures network traffic using `tcpdump`.
- **NGINX Reverse Proxy**: Provides secure access to services.
- **Prometheus**: Collects and scrapes data from various components.
- **Grafana**: Visualizes the network traffic and monitoring data.
- **Traffic Backup Pod**: Stores and handles network traffic backups.

For more detailed information on each component, refer to the `configs/` directory.

## Project Architecture

The project architecture consists of several interconnected components deployed in the Kubernetes cluster. It includes traffic capture, data backup, monitoring, and visualization. The components interact through services, persistent volumes, and NGINX as a reverse proxy for secure access.

![Project Architecture](./images/diagram.png)

[View Full Architecture Overview](./architecture.html)

## Setup Guide

To set up the cluster, please follow the detailed [Setup Guide](./setup.html).

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/repo-name.git
    ```

2. Deploy the Kubernetes cluster using the provided YAML files in the `configs/` directory.

3. Install the necessary Helm charts for Prometheus and Grafana:
    ```bash
    helm install prometheus stable/prometheus
    helm install grafana stable/grafana
    ```

4. Configure NGINX reverse proxy for secure access.

5. Start monitoring your network traffic.

## Screenshots

Below is a sample screenshot of the Grafana dashboard monitoring home network traffic:

![Grafana Dashboard](./images/grafana-dashboard.png)

## Future Enhancements

Here are some planned enhancements to further improve the system:

- **CI/CD Integration**: Jenkins or Flux for automated configuration updates and deployments.
- **Alerting System**: Implementation of Prometheus Alertmanager for network monitoring alerts.
- **Expanded Documentation**: More tutorials and use cases will be added.

## Contact

If you have any questions or suggestions, feel free to contact me via:

- Email: prenticesolutions@proton.me
- [GitHub Issues](https://github.com/prenticesolutions/PrenticeSolutions.github.io/issues)

---

Thank you for exploring my home Kubernetes cluster project!
