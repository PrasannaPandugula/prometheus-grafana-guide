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

 <img width="882" height="176" alt="image" src="https://github.com/user-attachments/assets/c6ab1257-09b8-4ccc-9701-2628d2bad132" />
