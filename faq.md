---
layout: default
title: "FAQ"
---

FAQ - Kubernetes Cluster Project
================================

Below are answers to some frequently asked questions about setting up and using the Kubernetes-based network monitoring cluster.

General Questions
-----------------

### Q: What is the purpose of this Kubernetes project?

A: This project sets up a Kubernetes cluster for monitoring and backing up network traffic using Prometheus, Grafana, and NGINX reverse proxy for secure external access.

### Q: Can I use this project on a Linux system?

A: Yes, the project was developed on Windows 11 Pro with Docker Desktop's Kubernetes engine, but it can be replicated on a complete Linux environment using Kubernetes and Docker directly.

Setup and Installation
----------------------

### Q: How do I clone the repository?

A: You can clone the repository using Git, GitHub Desktop, or VS Code integration. Full instructions can be found in the [Setup Guide](setup.html).

### Q: How do I access the Kubernetes Dashboard?

A: To access the Kubernetes Dashboard, use the following command:

    kubectl proxy

Then open your browser and go to:

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

### Q: Why is my Grafana dashboard not loading?

A: Ensure that you have port-forwarding set up for Grafana using the following command:

    kubectl port-forward svc/grafana 3000:80

If it still doesn’t load, verify that the Grafana pod is running and the port-forward is active.

Monitoring and Metrics
----------------------

### Q: How do I monitor network traffic?

A: Network traffic is captured by the `traffic-collector` pod using `tcpdump`. Prometheus scrapes metrics from the collector and backup pods, and Grafana visualizes these metrics.

### Q: How do I add new monitoring targets to Prometheus?

A: To add new targets to Prometheus, update the `prometheus-config.yml` file by adding a new `job_name` under `scrape_configs` with the new target's address.

Troubleshooting
---------------

### Q: What should I do if a pod fails to start?

A: Check the logs of the failed pod using the following command:

    kubectl logs 

This will provide insights into why the pod isn’t starting. It could be due to incorrect configurations, missing images, or insufficient resources.

### Q: What happens if the Persistent Volume is full?

A: If the persistent volume becomes full, you may need to either expand the volume or rotate the data by backing up older data to another storage and freeing up space. You can also increase the `capacity` in the persistent volume configuration.

### Q: How do I restart a service or pod?

A: To restart a pod, you can delete it, and Kubernetes will automatically restart it based on the deployment settings. Use this command to delete a pod:

    kubectl delete pod 

Future Enhancements
-------------------

### Q: What new features are planned for this project?

A: Future enhancements include integrating Jenkins for automated CI/CD pipeline, adding more monitoring metrics to Prometheus, and scaling the cluster based on network traffic.

### Q: How can I contribute to this project?

A: You can contribute by forking the repository, making your changes, and submitting a pull request on GitHub. Be sure to check the [Changelog](changelog.html) for recent updates and the [Roadmap](roadmap.html) page for upcoming features. Also check my [Contact](contact.html) page to get in touch with me!

