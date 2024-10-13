---
layout: default
title: "Changelog - Kubernetes Cluster Project"
---

# Changelog

This page documents the version history and key changes made to the Kubernetes network monitoring and automation project.

## Version 1.0 (Initial Release)
- Set up Kubernetes cluster on Docker Desktop using WSL 2.
- Deployed Prometheus and Grafana for network traffic monitoring and data visualization.
- Implemented NGINX reverse proxy for securing external access to Grafana and the Kubernetes Dashboard.
- Configured persistent volumes for network traffic data storage.
- Deployed traffic-collector and traffic-backup pods for capturing and backing up network traffic.

## Version 1.1 (Upcoming)
- Integrating Alertmanager for real-time alerting on network, pod, cluster, and security issues.
- Adding Jenkins integration for automating pod creation and configuration updates.
- Exploring the use of a database pod (MySQL or PostgreSQL) for more efficient traffic data storage.
- Enhancing security by reviewing NGINX configurations and potential automation for vulnerability checks.
- Transitioning from traffic-collector pod to **sFlow** for more efficient network traffic capture and reduced file sizes.

## Future Versions
Additional features and updates will be added as the project evolves. Refer to the [Roadmap page](roadmap.md) for more details on planned features.
