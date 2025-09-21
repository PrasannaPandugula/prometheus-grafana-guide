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

<img width="949" height="314" alt="image" src="https://github.com/user-attachments/assets/74a02fa3-4b17-4627-8974-2d7a60a47cd6" />

Our Prometheus web UI is available now, With the installation of Prometheus on Kubernetes via Helm, the Prometheus instance is now operational within the cluster, and we can reach it by navigating to a browser or using a specific URL.


##Grafana Installation:

To begin, let’s initiate the Grafana installation. Subsequently, we’ll establish integration between Prometheus and Grafana, with Grafana configured to utilize Prometheus as its primary data source. Lastly, leveraging Grafana, we’ll craft insightful dashboards to monitor and observe the Kubernetes cluster.

Now search for the Grafana helm chart by running the below command:

      ```helm search hub grafana```

<img width="958" height="268" alt="image" src="https://github.com/user-attachments/assets/e16dc2a7-c01d-47b5-9784-898bca45b9c1" />

An alternative approach is to navigate to the [Artifact Hub](https://artifacthub.io/) repository and explore the official Grafana Helm Chart.

<img width="605" height="415" alt="image" src="https://github.com/user-attachments/assets/0a010c81-6b80-4338-9265-5286234e0d37" />

#To Get Repo Info:

  ```helm repo add grafana https://grafana.github.io/helm-charts```
  
  ```helm repo update```

  <img width="431" height="32" alt="image" src="https://github.com/user-attachments/assets/ad50b826-7062-4b3f-b92c-ff6a2be91b4e" />

  <img width="547" height="67" alt="image" src="https://github.com/user-attachments/assets/d81baa35-a6b1-4728-8668-4b141d82011f" />

As you can see the Grafana repo is added successfully. Now we need to install the Grafana.

##Install Grafana Helm Chart on Kubernetes Cluster

 For installing the Grafana on Kubernetes, Use “helm install” command

  ```helm install grafana grafana/grafana```

 <img width="842" height="311" alt="image" src="https://github.com/user-attachments/assets/82f60bd8-e2f6-4411-b3d4-9a3300fd5230" />

 Having successfully installed Grafana on the Kubernetes Cluster, the Grafana server is now accessible through port 80. To retrieve the complete list of Kubernetes Services
 
 associated with Grafana, execute the following command:

   ```kubectl get service```

<img width="688" height="146" alt="image" src="https://github.com/user-attachments/assets/8a0000cf-7eeb-4d1f-965f-19caeed31581" />

## Exposing the Grafana Kubernetes Service

To expose the Grafana-service on Kubernetes we need to run this command

   ```kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext```

Ootput: 

<img width="749" height="161" alt="image" src="https://github.com/user-attachments/assets/12e29c82-b819-4e12-914d-7d38477ce551" />


By executing this command, we transition the service type from ClusterIP to NodePort, enabling external access to Grafana beyond the Kubernetes Cluster. The service will now be reachable on port 32449.

Run below command will generate the following URL to access the Grafana dashboard.

   ```minikube service grafana-ext```

<img width="517" height="142" alt="image" src="https://github.com/user-attachments/assets/92b538b2-4365-4de0-b5b9-6ae33b803c7e" />

# Grafana UI:

<img width="862" height="409" alt="image" src="https://github.com/user-attachments/assets/4afa4041-e967-429d-bc52-8dc56853ed70" />

UserName: admin

Password: run below command

kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }

Login to Grafana:

<img width="931" height="351" alt="image" src="https://github.com/user-attachments/assets/071427fe-c586-4a41-b694-428fbc818275" />

# Now lets add the data source as Prometheus. To add Prometheus as the data source, follow these steps:

  1. On the Welcome to Grafana Home page, click Add your first data source
     
  2. Select Prometheus as the data source

<img width="706" height="295" alt="image" src="https://github.com/user-attachments/assets/bb8cbb98-b5dd-41de-8287-2cab2a4f7b38" />

Include the internal cluster URL of your Prometheus application by referring to the initial URL displayed when executing the ‘minikube service prometheus-server-ext’ command earlier.

<img width="577" height="107" alt="image" src="https://github.com/user-attachments/assets/e9cdd2b2-9fed-4c63-a12d-36791a7c1243" />

## Grafana Dashboard

In this section, our focus will be on importing a Grafana Dashboard to streamline the process.

To import a Grafana Dashboard, follow these steps:

Get the Grafana Dashboard ID from the Grafana public Dashboard library (https://grafana.com/grafana/dashboards/)

<img width="1292" height="585" alt="image" src="https://github.com/user-attachments/assets/7c465d13-cf12-4cdf-8f64-2f6bb8797988" />

1. Now go to the search dashboard, and search for Kubernetes:

<img width="855" height="345" alt="image" src="https://github.com/user-attachments/assets/f1acfb08-3e30-493d-b678-254cd6fc6523" />

2. Select Dashboard and copy the Dashboard ID:

<img width="557" height="425" alt="image" src="https://github.com/user-attachments/assets/7cc38b0b-fd0f-4cab-a6b0-6eb20e45ac13" />











