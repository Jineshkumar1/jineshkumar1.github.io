---
title: "Deploy Voting App using AKS"
date: 2020-06-08T08:06:25+06:00
description: Deploy Voting App using AKS.
menu:
  sidebar:
    name: Deploy Voting App using AKS
    identifier: Deploy Voting App using AKS
    parent: Azure-Blogs
    weight: 10
hero: images/forest.jpg
tags: ["Azure","Cloud", "AKS", "Azure Kubernetes"]
categories: ["Basic"]
---

## Deploy "Voting App" using Azure Kubernetes Cluster Service

**Azure Kubernetes Service (AKS)** is a managed Kubernetes service that lets you quickly deploy and manage clusters. 

This is a Tutorial on how to deploy a container-based application (Voting-App) using Azure Kubernetes Cluster service.

### First, Few very basics about Kubernetes,  
  
Kubernetes is a production-ready, portable, open-source platform for managing **containerized workloads** and services, that facilitates both declarative configuration and automation.  

Basically, Kubernetes is a **container orchestration tool**  When you deploy Kubernetes, you get a cluster. This Cluster has MASTER NODE and WORKER NODEs.  

The abbreviation K8s is derived by replacing the eight letters of “ubernete” with the digit 8.  

To understand Kubernetes Architecture overview, I post some Images and their Source which are good place to start learning about Kubernetes if you are new to k8s.  

> Note : This is just overview understand this Application Deployment for this Blog. I have plans to provide more in-depth Kubernetes tutorials coming soon. Consider Following my Blogs.Thx.  
      
![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630040481776/3LcQ6fDo6.png)
Image Source : https://kubernetes.io/docs/tutorials/kubernetes-basics/ 
 
![12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630040619098/M72npMo7o.png)
Image Source : https://www.edureka.co/blog/kubernetes-tutorial/  

![123.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630040785917/xRXHpDE_mD.png)

Image source : https://collabnix.com/5-minutes-to-kubernetes-architecture/  

# Let's get started with our Deployment,   

To-do List :  
- Deploy an AKS(Azure K8s Service) cluster using Azure Portal.  
- Run a multi-container application with a web front-end and a Redis instance in the cluster.(Voting App. taken from Open Source Github Repo: [dockersamples/
example-voting-app](https://github.com/dockersamples/example-voting-app ) )
 
### Create Azure Kubernetes Cluster Service using Azure Portal  

- On Azure Portal > Search Kubernetes Service > Create k8s Cluster and It will ask for Product details like Resource Group Name, Cluster Name, Region, Availability Zones, Kubernetes Version, Node Size, Scale Method(AutoScaling), Node Count Range (1-2).  
Configure those as you want then  Review + Create  As per,   
![11.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630042341315/qzcnTp9u5.png)
![22.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630042349177/8dukA3EEr.png)  
> Note: Primary node pool    
The number and size of nodes in the primary node pool in your cluster. For production workloads, at least 3 nodes are recommended for resiliency. For development or test workloads, only one node is required.   

- Validation passed > Hit Create.  
And We have successfully deployed Azure Kubernetes Cluster with 2 nodes on which we can deploy our Container-based Voting Application.
![33.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630042971644/WLARPBMW7.png)  

### Get into ** Azure Cloud Shell** to run our k8s Cluster and Deploy our app.  

- Go to Resource once deployment successful notification popup.  
![44.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630043264264/68IGl4gZN.png)  

- Our K8s Cluster (VotingAppCluster) Overview page,  
![55.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630043374120/ZpQ3B4Ljk.png)  

- Open Azure CLI from the Azure Portal button from top-right corner. Bash Azure Cloud Shell will pop from the bottom,    

> Note : When you first-time open the Cloud Shell, you will find that it requires you to create a Storage account. The reason for that Storage Account is to persist the scripts, keys, etc that you'll use over and over as you interact with your resources  

![66.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630043596567/nBNmGtxmd.png)  

- Get access credentials for a managed Kubernetes cluster.  
```
az aks get-credentials --resource-group YourResourceGroupNAME --name YourAKSClusterNAME
``` 
![77.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630043988795/foWDntU7q.png)  

- Verify the connection to your cluster using the "kubectl get nodes"  This command returns a list of the cluster nodes.  (We have 2) 
![88.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044085054/BrvApDyLR.jpeg)

### Run the Application  
- The sample Azure Vote Python applications.  
- A Redis instance.  

- First Create a file named votingapp.yaml  
I used nano editor to create, Edit, and save .yaml file.  

![99.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044874284/pjRV2-Snu.jpeg)

-paste below content into the nano editor for votingapp.yaml file  
run > nano votingapp.yaml  
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  selector:
    matchLabels:
      app: azure-vote-back
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      nodeSelector:
        "kubernetes.io/os": linux
      containers:
      - name: azure-vote-back
        image: mcr.microsoft.com/oss/bitnami/redis:6.0.8
        env:
        - name: ALLOW_EMPTY_PASSWORD
          value: "yes"
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  selector:
    matchLabels:
      app: azure-vote-front
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      nodeSelector:
        "kubernetes.io/os": linux
      containers:
      - name: azure-vote-front
        image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
``` 
- Paste the Above Copied content in there.  
- Cnt + 0 to save file [Wrote 85 lines] in my .yaml  
and  Cnt + z to exit out.   

![100.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045270822/lQ5Iuvwsz.jpeg)  

- Deploy the application using the "kubectl apply" specify the name of your YAML manifest file. as per, 
```
kubectl apply -f votingapp.yaml
```   
- Our Voting App is deployed successfully when you get that "azure-vote-back" and  "azure-vote-front" get created.  

![110.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045463194/96E1akKYp.png)

### Now it's about time to TEST Out the App.  

- We need the Public IP Address. To get our deployment has created an external IP, run below command,  

```
 kubectl get service azure-vote-front --watch
``` 
This shows our Application's external Public IP address.  
My App's External-IP = 52.190.47.180  

![120.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045901221/Qh44RHVz7.png)  

- Copy External-IP (52.190.47.180  ) and paste it on your Browser  

![Final Deployed App.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630046124301/XGSFRI4Sr.png)  

You got that. This App is deployed on 2 Cluster Nodes with high availibility and resiliency.  

- Nodes and Cluster Monitoring  for our Voting App
Under AKS > Cluster Insight / Monitor Tabs respectively.  

![Node Monitors 1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630046443936/Z5OHfteOS.png)  


![Node Monitors 2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630046457314/OieY-thla.png)

** Success.  **

### Azure Kubernetes Cluster Service, 
- It is a fully managed Kubernetes Cluster Service. Deploy a managed Kubernetes cluster in Azure.
– Reduces the complexity and operation overhead of managing
K8s by offloading much of that responsibility to Azure
- Azure AKS Cluster Handles critical operations tasks like load balancing, scaling, health monitoring, and maintenance for you.

> I am on my continuous learning quest and Kubernetes is in the top list. I apologize if I may have missed some key details or explained less on some commands performed above.  
I will be coming up with more in-depth tutorials and blogs about Kubernetes and DevOps in future content.

Hope you have followed along and like the Blog about   
**Deploy "Voting App" using Azure Kubernetes Cluster Service**

Let me know if you have any questions or suggestions to improve my knowledge.  

Thanks for your time.  
Follow for more Awesome Azure and AWS Content.

Regards,  
Jineshkumar Patel
 











