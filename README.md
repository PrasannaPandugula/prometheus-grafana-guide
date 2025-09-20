## Overview of Prometheus, Grafana, and Helm:

<img width="800" height="210" alt="image" src="https://github.com/user-attachments/assets/b2a7aa34-6750-4ae0-81c9-94d275a6acd7" />

Prometheus: An open-source monitoring and alerting toolkit designed for Kubernetes, Prometheus excels in collecting and querying real-time metrics.
Grafana: A powerful analytics and monitoring platform that integrates seamlessly with Prometheus, offering visually stunning dashboards.
Helm: The Kubernetes package manager that simplifies the deployment and management of applications through charts.

## Prerequisites:
      1.Minikube 
      2.kubectl 
      3.Helm installed 

Prometheus Installation:
Step 1: Run the following command to add prometheus to helm chart

      helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
      helm repo update

## Install Prometheus Helm Chart on Kubernetes Cluster
To install the Prometheus helm chart we need to run the “helm install” command as below shown

      helm install prometheus prometheus-community/prometheus

We have successfully installed Prometheus on Kubernetes, Now to check the deployed Kubernetes resources by running the ‘kubectl’ command
Output:

 <img width="764" height="506" alt="image" src="https://github.com/user-attachments/assets/bebecc32-a418-41a7-ae0b-5be59f700622" />

When you install the Prometheus Helm chart, it creates several Kubernetes resources to set up the Prometheus monitoring system. Here’s a brief list of the key resources that are typically created:

ConfigMaps:

Prometheus-server: Contains the main Prometheus configuration.
Prometheus-rule files: Stores Prometheus alerting and recording rules.

1. Secrets:

   Prometheus-server-TLS: Contains TLS certificates for secure communication.

2. ServiceAccounts:

    Prometheus-server: Defines the service account used by the Prometheus server components.

3. ClusterRole and ClusterRoleBinding:

    Prometheus-server: Grants necessary permissions to the Prometheus server components.

4. StatefulSet:

    Prometheus-server: Manages the stateful deployment of Prometheus server pods.

5. Service:

    Prometheus-server: Exposes the Prometheus server within the cluster.

The next step is to access and launch the Prometheus Kubernetes application. You’ll access the application using the Kubernetes services for Prometheus. To get all the Kubernetes Services for Prometheus, run this command:

        kubectl get service
      
Output:

<img width="698" height="134" alt="image" src="https://github.com/user-attachments/assets/13af8700-57fb-43b0-9e63-4a7fcd5abbf1" />

##Prometheus-alert manager(ClusterIP): 

  Alertmanager is a component of Prometheus that manages and handles alerts. This service provides the ClusterIP for communication within the cluster on port 9093.
  
##Prometheus-alert manager-headless(ClusterIP): 

  This is a headless service for Alertmanager, meaning it does not provide a ClusterIP. It is used for discovery purposes, typically when other services need to discover the     IP addresses of Alertmanager instances.
## Prometheus-kube-state-metrics (ClusterIP):

 Kube-state-metrics is an add-on service for Prometheus that exposes Kubernetes resource metrics. This service provides a ClusterIP for communication within the cluster on     port 8080.

## Prometheus-prometheus-node-exporter (ClusterIP):

 Node Exporter is a Prometheus exporter that collects system-level metrics from nodes in the cluster. This service provides a ClusterIP for communication within the cluster    on port 9100.
## Prometheus-prometheus-pushgateway (ClusterIP):

 Pushgateway allows ephemeral and batch jobs to expose their metrics to Prometheus. This service provides a ClusterIP for communication within the cluster on port 9091.

## Prometheus-server (ClusterIP):

  Prometheus server is the core component that collects, stores, and queries metrics. This service provides a ClusterIP for communication within the cluster.

## Exposing the Prometheus-server service on Kubernetes

 To expose the Kubernetes Prometheus-server service, run this command

   ```kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext```

If you need to access Prometheus from outside the Kubernetes cluster, exposing it as a NodePort allows you to do so. You can use the node’s IP and the allocated NodePort to reach Prometheus. If you have external monitoring or visualization tools that need to connect to Prometheus, exposing it as a NodePort facilitates this external integration.

After making the Prometheus-server Kubernetes service accessible, let’s reach the Prometheus application by employing the provided command.

  ```minikube service prometheus-server-ext```

Output: 

<img width="616" height="177" alt="image" src="https://github.com/user-attachments/assets/ac444e0b-2c28-482a-8ada-73ac778fbbe6" />



