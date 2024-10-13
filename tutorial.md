---
layout: default
title: "Tutorials"
---
How-To Guides and Tutorials
===========================

This page provides step-by-step guides on essential tasks for managing and using the Kubernetes network monitoring cluster.

1\. Deploying New Pods
----------------------

Follow these steps to deploy a new pod in your Kubernetes cluster:

1.  Create your pod configuration file (YAML format).
2.  Use the `kubectl apply` command to deploy the pod:

    kubectl apply -f 

4.  Verify that the pod is running by checking the pod status:

    kubectl get pods

6.  If the pod fails to start, you can check the logs for more information (see section on getting logs).

2\. Running Port Forward for Grafana and Kubernetes Dashboard
-------------------------------------------------------------

To access Grafana and the Kubernetes Dashboard, you'll need to set up port forwarding:

### Port Forward for Grafana:

1.  Run the following command to forward the Grafana service to your localhost:

    kubectl port-forward svc/grafana 3000:80

3.  Open your browser and go to `http://localhost:3000` to access the Grafana dashboard.

### Port Forward for Kubernetes Dashboard:

1.  Run the following command to proxy the Kubernetes Dashboard to your localhost:

    kubectl proxy

3.  Open your browser and go to the following URL:

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

5.  For more information on setting up the Kubernetes Dashboard, visit the official documentation: [Kubernetes Dashboard Documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).

3\. Getting Logs and Pods
-------------------------

It's important to monitor pod activity and retrieve logs when debugging. Here are the key commands:

### Get All Running Pods:

To view all running pods in the cluster:

    kubectl get pods

### Check Pod Logs:

To view logs for a specific pod, use the following command:

    kubectl logs 

4\. Setting Up the NGINX Reverse Proxy
--------------------------------------

Setting up the NGINX reverse proxy allows secure access to the Grafana and Kubernetes dashboards.

### Within the Cluster:

1.  Create the NGINX ConfigMap:

    kubectl apply -f nginx-configmap.yml

3.  Deploy the NGINX pod:

    kubectl apply -f nginx-reverse-proxy.yml

5.  Verify the NGINX pod is running:

    kubectl get pods

### From Another Machine (External Access):

1.  Install NGINX on the external machine:

    sudo apt install nginx

3.  Configure NGINX to forward requests to the Kubernetes cluster. Edit the `/etc/nginx/nginx.conf` file to include:

    
    server {
        listen 80;
        location /grafana/ {
            proxy_pass http://:3000;
        }
        location /kubernetes-dashboard/ {
            proxy_pass http://:8001;
        }
    }
                

5.  Restart NGINX to apply the changes:

    sudo systemctl restart nginx

7.  Now, when users go to `http:///grafana/`, they will be securely forwarded to the Grafana dashboard.

\> // Get the current URL path const currentPath = window.location.pathname.split("/").pop(); // Get all nav links const navLinks = document.querySelectorAll("nav ul li a"); // Loop through each nav link and add 'active' class to the one that matches the current path navLinks.forEach(link => { if (link.getAttribute("href") === currentPath) { link.classList.add("active"); } });