---
layout: default
title: "How-To Guide"
---
How-To Guide
================

This page provides step-by-step guides on essential tasks for managing and using the Kubernetes network monitoring cluster.

1\. Deploying New Pods
----------------------

Follow these steps to deploy a new pod in your Kubernetes cluster:

1.  Create your pod configuration file (YAML format).
2.  Use the `kubectl apply` command to deploy the pod:
```bash
   kubectl apply -f
```

4.  Verify that the pod is running by checking the pod status:
```bash
    kubectl get pods
```

6.  If the pod fails to start, you can check the logs for more information (see section on getting logs).

2\. Running Port Forward for Grafana and Kubernetes Dashboard
-------------------------------------------------------------

To access Grafana and the Kubernetes Dashboard, you'll need to set up port forwarding:

### Port Forward for Grafana:

1.  Run the following command to forward the Grafana service to your localhost:
```bash
    kubectl port-forward svc/grafana 3000:3000
```
3.  Open your browser and go to `http://localhost:3000` to access the Grafana dashboard.

### Port Forward for Kubernetes Dashboard:

1.  Run the following command to proxy the Kubernetes Dashboard to your localhost:
```bash
    kubectl proxy
```
3.  Open your browser and go to the following URL:

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

5.  For more information on setting up the Kubernetes Dashboard, visit the official documentation: [Kubernetes Dashboard Documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).

3\. Getting Logs and Pods
-------------------------

It's important to monitor pod activity and retrieve logs when debugging. Here are the key commands:

### Get All Running Pods:

To view all running pods in the cluster:
```bash
    kubectl get pods
```
### Check Pod Logs:

To view logs for a specific pod, use the following command:
```bash
    kubectl logs
```