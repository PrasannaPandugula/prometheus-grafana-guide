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

Secrets:

Prometheus-server-TLS: Contains TLS certificates for secure communication.

ServiceAccounts:

Prometheus-server: Defines the service account used by the Prometheus server components.

ClusterRole and ClusterRoleBinding:

Prometheus-server: Grants necessary permissions to the Prometheus server components.

StatefulSet:

Prometheus-server: Manages the stateful deployment of Prometheus server pods.

Service:

Prometheus-server: Exposes the Prometheus server within the cluster.

