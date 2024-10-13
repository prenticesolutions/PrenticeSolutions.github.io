---
layout: default
title: "Documentation"
---

Documentation: Kubernetes Cluster Configuration Files
=====================================================

This page provides detailed documentation for the Kubernetes configuration files used in the network monitoring and automation project.

1\. Persistent Volume Configuration
-----------------------------------

The persistent volume configuration ensures there is a static place on the host machine to store data such as backups or captured network traffic.

### File: persistent-volume.yml

    
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: backup-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      storageClassName: manual
      hostPath:
        path: /mnt/data
            

**Description:** This configuration defines a persistent volume (PV) named `backup-pv` with 1Gi of storage capacity. The `accessModes` specify that the volume can be mounted as read-write by a single node (`ReadWriteOnce`), and the `hostPath` points to the local path `/mnt/data` on the host machine.

2\. Persistent Volume Claim Configuration
-----------------------------------------

The persistent volume claim (PVC) requests storage from a persistent volume.

### File: persistent-volume-claim.yml

    
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: backup-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
            

**Description:** This configuration defines a persistent volume claim (PVC) named `backup-pvc` that requests 1Gi of storage from the persistent volume. It requires `ReadWriteOnce` access, ensuring that only one node can mount the volume at a time.

3\. Kubernetes Dashboard Pod
----------------------------

This file configures the Kubernetes Dashboard, providing a UI for managing the cluster.

### File: kubernetes-dash.yml

    
    apiVersion: v1
    kind: Pod
    metadata:
      name: kubernetes-dashboard
    spec:
      containers:
        - name: kubernetes-dashboard
          image: kubernetesui/dashboard:v2.0.0
          ports:
            - containerPort: 80
            

**Description:** This YAML file sets up the Kubernetes Dashboard pod, making it accessible through NGINX. It provides a web-based interface to monitor and control the cluster.

4\. NGINX ConfigMap and Reverse Proxy
-------------------------------------

The NGINX ConfigMap and Reverse Proxy files configure a reverse proxy to secure and manage external access.

### File: nginx-configmap.yml

    
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: nginx-config
    data:
      nginx.conf: |
        server {
          listen 80;
          location / {
            proxy_pass http://kubernetes-dashboard;
          }
        }
            

**Description:** This config sets up NGINX with routing and reverse proxy configuration to forward traffic to the Kubernetes Dashboard.

### File: nginx-reverse-proxy.yml

    
    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
          volumeMounts:
            - name: nginx-config-volume
              mountPath: /etc/nginx/nginx.conf
              subPath: nginx.conf
      volumes:
        - name: nginx-config-volume
          configMap:
            name: nginx-config
            

**Description:** This file configures the NGINX reverse proxy, allowing secure access to the Kubernetes Dashboard and Grafana.

5\. Prometheus Configuration
----------------------------

Prometheus is responsible for scraping metrics from the cluster.

### File: prometheus-config.yml

    
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: prometheus-config
    data:
      prometheus.yml: |
        global:
          scrape_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
              - targets: ['localhost:9090']
            

**Description:** This configuration file tells Prometheus how to scrape data from the traffic collector and backup pods.

### File: prometheus-service.yml

    
    apiVersion: v1
    kind: Service
    metadata:
      name: prometheus
    spec:
      ports:
        - port: 9090
          targetPort: 9090
      selector:
        app: prometheus
            

**Description:** The Prometheus service exposes the Prometheus pod, allowing Grafana and other services to access the metrics it collects.

6\. Traffic Backup and Collector Pods
-------------------------------------

These pods handle the collection and backup of network traffic data.

### File: traffic-backup.yml

    
    apiVersion: v1
    kind: Pod
    metadata:
      name: traffic-backup
    spec:
      containers:
        - name: traffic-backup
          image: traffic-backup-image
          volumeMounts:
            - name: backup-storage
              mountPath: /data
      volumes:
        - name: backup-storage
          persistentVolumeClaim:
            claimName: backup-pvc
            

**Description:** The traffic backup pod is responsible for backing up the network traffic data captured by the collector pod.

### File: traffic-backup-service.yml

    
    apiVersion: v1
    kind: Service
    metadata:
      name: traffic-backup-service
    spec:
      ports:
        - port: 8080
          targetPort: 8080
      selector:
        app: traffic-backup
            

**Description:** This service exposes the traffic backup pod within the cluster.

### File: traffic-collector.yml

    
    apiVersion: v1
    kind: Pod
    metadata:
      name: traffic-collector
    spec:
      containers:
        - name: traffic-collector
          image: traffic-collector-image
          volumeMounts:
            - name: capture-storage
              mountPath: /data
      volumes:
        - name: capture-storage
          persistentVolumeClaim:
            claimName: backup-pvc
            

**Description:** The traffic collector pod collects real-time network traffic using tcpdump.

### File: traffic-collector-service.yml

    
    apiVersion: v1
    kind: Service
    metadata:
      name: traffic-collector-service
    spec:
      ports:
        - port: 8081
          targetPort: 8081
      selector:
        app: traffic-collector
            

**Description:** The traffic collector service exposes the traffic collector pod, allowing it to capture and relay network traffic.

\> // Get the current URL path const currentPath = window.location.pathname.split("/").pop(); // Get all nav links const navLinks = document.querySelectorAll("nav ul li a"); // Loop through each nav link and add 'active' class to the one that matches the current path navLinks.forEach(link => { if (link.getAttribute("href") === currentPath) { link.classList.add("active"); } });