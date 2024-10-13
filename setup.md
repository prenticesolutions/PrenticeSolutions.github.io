---
layout: default
title: "Setup"
---



Setup Guide: Home Kubernetes Cluster for Network Monitoring and Automation
==========================================================================

Step 1: Clone the Repository
----------------------------

Before you begin, clone the repository containing all the configuration files to your local machine. You can do this via Git, GitHub Desktop, or VS Code's integration.

### Using GitHub Desktop:

1.  Open **GitHub Desktop** and click on **Clone a repository**.
2.  Choose the repository and select the directory to save it in.

### Using VS Code:

1.  In VS Code, press `Ctrl+Shift+P` to open the command palette.
2.  Type **Git: Clone** and select **Clone Repository**.
3.  Paste the URL of your GitHub repository and choose the directory to save the files.

Once the repository is cloned, navigate to the working directory where you’ll be deploying your Kubernetes configuration files.

* * *

Step 2: Docker Desktop Configuration
------------------------------------

### Enable Kubernetes:

1.  Open **Docker Desktop**, go to **Settings** → **Kubernetes**.
2.  Toggle the switch to **Enable Kubernetes**.

### Resource Saver:

*   Under **Resources** and **Advanced**, set the **Resource Saver** to 5 minutes (optional).

### Disk Image Location:

*   Leave the **default disk image location**.

### Network Settings:

*   The project uses the **default subnet** (this can be changed later if needed).
*   **Enable Host Networking**: Under **Network**, ensure that **Enable host networking** is toggled on.

### WSL 2 Integration:

1.  Go to the **WSL** tab in settings.
2.  Toggle on **Enable integration with my default WSL distro** and select **Debian** as the distro.

### Other Settings:

*   Everything else remains at the default settings for this project.

* * *

Step 3: Setting Up the Kubernetes Cluster
-----------------------------------------

Since this is an educational project, Docker Desktop will automatically create the default namespaces required to run the cluster. You don’t need to manually manage namespaces for this setup.

* * *

Step 4: Installing Helm and Grafana
-----------------------------------

### Install Helm:

Run the following command to install Helm:

    curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

### Add Helm Repositories:

1.  Add the stable Helm chart repository:
    
        helm repo add stable https://charts.helm.sh/stable
    
2.  Add the Grafana Helm chart repository:
    
        helm repo add grafana https://grafana.github.io/helm-charts
    

### Install Grafana:

1.  Install Grafana using Helm and access the dashboard:
    
        helm install grafana grafana/grafana kubectl port-forward svc/grafana 3000:80
    
2.  Follow Grafana’s official documentation for setting up user credentials and further customization.

* * *

Step 5: Deploying the Pods
--------------------------

Once Grafana is set up, it's time to deploy the Kubernetes pods. Each configuration file is applied using `kubectl apply -f` in the following order:

### Deploy the NGINX ConfigMap and NGINX Pod:

    kubectl apply -f nginx-configmap.yml kubectl apply -f nginx-reverse-proxy.yml

### Deploy the Monitoring (Prometheus) Pod:

    kubectl apply -f monitoring-pod.yml

### Deploy the Kubernetes Dashboard Pod:

    kubectl apply -f kubernetes-dash.yml

* * *

Step 6: Accessing the Kubernetes Dashboard
------------------------------------------

To access the Kubernetes Dashboard, you need to run the following command to proxy requests from your local machine:

    kubectl proxy

Once the proxy is running, open a browser and go to the following URL:

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

This will open the Kubernetes Dashboard, where you can monitor and manage your cluster.

* * *

Step 7: Deploying the Persistent Volume and Services
----------------------------------------------------

### Deploy the Persistent Volume and Claim:

    kubectl apply -f persistent-volume.yml kubectl apply -f persistent-volume-claim.yml

### Deploy the Traffic Backup and Collector Services:

    kubectl apply -f traffic-backup-service.yml kubectl apply -f traffic-collector-service.yml

* * *

Step 8: Deploying the Traffic Pods
----------------------------------

### Deploy the Traffic Backup Pod:

    kubectl apply -f traffic-backup.yml

### Deploy the Traffic Collector Pod:

    kubectl apply -f traffic-collector.yml

* * *

Monitoring and Visualizing Metrics
----------------------------------

Once the Prometheus and Grafana services are running, you can monitor network metrics by accessing Grafana at `localhost:3000`. Follow Grafana's official documentation to set up dashboards, add data sources, and visualize real-time network traffic.

\> // Get the current URL path const currentPath = window.location.pathname.split("/").pop(); // Get all nav links const navLinks = document.querySelectorAll("nav ul li a"); // Loop through each nav link and add 'active' class to the one that matches the current path navLinks.forEach(link => { if (link.getAttribute("href") === currentPath) { link.classList.add("active"); } });