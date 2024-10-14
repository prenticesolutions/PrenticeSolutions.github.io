---
layout: default
title: "Roadmap"
---

# Roadmap

## Future Enhancements and Roadmap
===============================

This page outlines the planned enhancements and roadmap for the Kubernetes-based network monitoring cluster. Each enhancement is designed to improve functionality, automation, and security in a phased approach.

Planned Enhancements
--------------------

### 1\. Alerting and Transition to Efficient Traffic Capture (30 days)

*   Integrate **Alertmanager** to notify on various types of network, pod, cluster, and security issues.
*   Replace the existing traffic-collector pod with **sFlow** for more efficient network traffic capture.

### 2\. Jenkins Integration (90 days)

**Goal:** Automate the process of creating pods and updating configurations of existing pods using Jenkins.

### 3\. Database Pod Exploration (180 days)

**Goal:** Investigate the efficiency of using a dedicated database pod (e.g., MySQL or PostgreSQL) for storing network traffic data compared to the current traffic backup pod.

### 4\. Enhancing Security (Ongoing)

**Goal:** Continuously improve the security of the cluster. Review NGINX configurations for vulnerabilities and automate security checks.

Roadmap Timeline
----------------

### Phase 1: Alerting & sFlow (30 Days)

Complete the integration of Alertmanager and replace traffic-collector pod with sFlow.

### Phase 2: Jenkins Integration (90 Days)

Automate pod creation and configuration management with Jenkins.

### Phase 3: DB Pod Exploration (180 Days)

Explore the efficiency of using a database pod for storing network traffic data.

### Ongoing: Security Enhancements

Continuously improve security, starting with NGINX vulnerability checks.