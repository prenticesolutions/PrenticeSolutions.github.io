---
layout: default
title: "Setup"
---



# Setup Guide:
=====================

Step 1: Clone the Repository
----------------------------

Before you begin, clone the repository containing all the configuration files to your local machine. You can do this via Git, GitHub Desktop, or VS Code's integration.

## Step 1: Clone the Repository

To clone the repository using Git from the command line, follow these steps:

1. Open a terminal on your local machine.
2. Run the following command to clone the repository:
    ```bash
    git clone https://github.com/prenticesolutions/PrenticeSolutions.github.io.git
    ```
3. Navigate to the cloned directory:
    ```bash
    cd PrenticeSolutions.github.io/configs 
    ```
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

Step 4: Installing Helm, Kubernets Dashboard and Grafana
-----------------------------------

### Install Helm:

Run the following command to install Helm:

    curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

### Add Helm Repositories:

1.  Add the stable Helm chart repository:
    
        helm repo add stable https://charts.helm.sh/stable
    
2.  Add the Grafana Helm chart repository:
    
        helm repo add grafana https://grafana.github.io/helm-charts

3.  Add the Kubernetes Dashboard Helm chart repository:
    
        helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/

### Update Helm Repositories:

    helm repo update

### Install the Kubernetes Dashboard:
1.  Install the Kubernetes Dashboard using Helm:
    
        helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard

2. Follow Kubernetes Dashboard's official documentation for setting up user credentials and further customization.
    [Kubernetes Dashboard Documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
    

### Install Grafana:

1.  Install Grafana using Helm and access the dashboard:
    
        helm install grafana grafana/grafana kubectl port-forward svc/grafana 3000:80
    
2.  Follow Grafana’s official documentation for setting up user credentials and further customization.
    [Grafana Documentation](https://grafana.com/docs/grafana/latest/)

* * *

Step 6: Deploying the Persistent Volume and Services
----------------------------------------------------

### Deploy the Persistent Volume and Claim:

    kubectl apply -f persistent-volume.yml 
    kubectl apply -f persistent-volume-claim.yml

### Deploy the Traffic Backup and Collector Services:

    kubectl apply -f traffic-backup-service.yml 
    kubectl apply -f traffic-collector-service.yml

* * *

Step 7: Deploying the Traffic Pods
----------------------------------

### Deploy the Traffic Backup Pod:

    kubectl apply -f traffic-backup.yml

### Deploy the Traffic Collector Pod:

    kubectl apply -f traffic-collector.yml

* * *

Step 8: Setting Up the NGINX Reverse Proxy
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

***

Step 9: Accessing the Kubernetes and Grafana Dashboards
-------------------------------------------------------

To access the Kubernetes Dashboard, you need to run the following command to proxy requests from your local machine:

    kubectl proxy

Once the proxy is running, open a browser and go to the following URL:

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.

This will open the Kubernetes Dashboard, where you can monitor and manage your cluster. (Note: The period at the end of the URL is required.)

* * *

To access the Grafana Dashboard, you need to run the following command to forward the Grafana service to your localhost:

    kubectl port-forward svc/grafana 3000:3000

Open your browser and go to `http://localhost:3000` to access the Grafana dashboard.

***

