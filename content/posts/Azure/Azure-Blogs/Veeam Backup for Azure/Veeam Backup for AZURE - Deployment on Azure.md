---
title: "Veeam Backup for Azure"
date: 2020-06-08T08:06:25+06:00
description: Veeam Backup for Azure.
menu:
  sidebar:
    name: Veeam Backup for Azure
    identifier: Veeam Backup for Azure
    parent: Azure-Blogs
    weight: 10
hero: images/forest.jpg
tags: ["Azure","Cloud", "Storage", "Azure Storage", "veam Backup"]
categories: ["Basic"]
---

## Veeam Backup for AZURE  - Deployment on Azure (Native Azure Backup - SaaS)

**Advantages of Veeam Backup for Azure**,  

![Advantages.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629753274485/TaYzaAxDR.jpeg)

**Your Azure Backup Infrastructure looks like this, ** 
![1.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629752837933/Rhy8YwPnL.jpeg)  
- **Backup Appliance **   
   The backup appliance is a Linux-based Azure VM where Veeam Backup for Microsoft Azure is installed.  
Backup Appliance will run Backup Service, Config. DB, WebUI, Update Service, REST API Service.  
- **Backup Repositories**    
   A backup repository is a folder in a blob container where Veeam Backup for Microsoft Azure stores backups of Azure VMs  
- **Worker Instances**  
    A worker instance is an auxiliary Linux-based virtual machine that is responsible for the interaction between the backup appliance and other components of the Veeam Backup for Microsoft Azure infrastructure. Worker instances process the backup workload and distribute backup traffic when transferring data to backup repositories.

### **Deployment Of  "Veeam Backup for Microsoft Azure" Free Edition**  
Note: For the Demo Purposes, I am selecting the minimum resources allocation required to get started with Veeam Backup for Azure.  
1. Find "Veeam Backup for Microsoft Azure Free Edition" on Azure Marketplace  
![Marketplace.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629754618549/VtBksbzr0.jpeg)  
2.  Create a Virtual Machine: Select Username and Password. I selected Standard B2s (2vCPU, 4GB RAM)  
![Virtual machine.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629754834066/ZC8N5f9e1.jpeg)
3. VM Disks Settings  
![Disks.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629755300422/Rp247a_ZA.jpeg)
4. Networking  
![networking.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629755276271/xhfQbTMIU.jpeg)  
5. All other Settings as Default for minimum Cost. It comes down to,    
![cost product.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629755396894/4-0zlRfva.jpeg)  
![summary VM.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629755468430/WUo9MuAGR.jpeg)
6. Hit "Create"  
Your VM for **"Veeam Backup for Azure"** is Deployed.  
and below resources get created in your Azure Environment.     
![resources.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629755658491/p5MTo8iWv-.jpeg)
7. Go to VeeamAzure VM > Copy the Public IP Address and Open WebUI using https://Your.Public.IP.Address (it only works with https)  
![cbazure login.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629756494954/boiCyzTUh.jpeg)  
THIS IS YOUR WEBUI (Backup Appliance), Login with the Username and Password Set while creating a Virtual Machine.  
8. Accept the "EULA"  (No other Choice...) 
![accept EULA.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629756718437/kTJMQ6wWD.jpeg)
9. And you are in the Configuration Phase of your Veeam Backup for Azure.    
 
THREE things "TO DO" here,  
1> Add Microsoft Azure Connection  
2> Add Repository  
3> Create your first Backup Policy    
![Configuration.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629756800402/ggQ1s2jRk.jpeg)  

Add Azure Account and Authenticate and Finish.    
![Add Azure Account.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629757058013/N3qQCrdhF.jpeg)  

Add Repository  > Select New / Existing Container (Blob) Storage and Folder. Then Select Storage Tier and Encryption. 
![repository 1.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629757396467/w9GhioTSU.jpeg)  
![repository 2.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629757478226/sdK2CINiPA.jpeg)

**IMPORTANT**: Add Backup Policy (Backup Job Configuration and its Schedule settings)  

![Add Policy Settings.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629757640749/lmiIkyygK.jpeg)

Veeam allows a vast range of features for different kinds of workload including "ApplicationAware processing" (Application-aware Snapshots), Guest Scripting, Schedule, Cost Estimation inbuilt. 
 
**One Cool Feature to mention**  : To avoid downtime, high-availability systems may perform the backup on a snapshot—a read-only copy of the data set frozen at a point in time—and allow applications to continue writing to their data. Once the initial snapshot is taken of a data set, subsequent snapshots copy the changed data only and use a system of pointers to reference the initial snapshot. This method of pointer-based snapshots consumes less disk capacity than if the data set was repeatedly cloned.  

Schedule Options (ALL Configuration as per your requirements)   

![Schedule options.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629757934200/5_KVCNeea.jpeg)  

![Schedule configuration.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629758118960/SAPEraULx.jpeg)  

**Cost Estimation in built. Cool huh ?! ** (But remember, its an estimate)  
![Cost estimation.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629758009525/0lIVDt0l5.jpeg)  

And at the End, SUMMARY of your Backup Policy.  
(Here I am backing up two of my important Azure Projects At the Resource Group Level. )
![Backup Policy Summary.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629758308078/97UINWJNwg.jpeg)  

Final Overview of the WebUI for  
** "Veeam Backup for Microsoft Azure".  **

![Final Overview.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629758495892/6tViCt9Yc.jpeg)  

**Veeam Backup for Microsoft Azure** is a solution developed for protection and disaster recovery tasks for Microsoft Azure environments. With Veeam Backup for Microsoft Azure, you can perform the following operations:

- Create image-level backups and cloud-native snapshots of Azure VMs.
- Keep the backed-up data in cost-effective and long-term Microsoft Azure storage accounts.
- Restore entire Azure VMs, individual virtual disks, and guest OS files and folders.  
- It has many more key features that help Backup and Restores your Azure workload, faster, and with easy configuration.  

Veeam is continuously Leading the Industry in "Enterprise Backup and Recovery Software Solutions" and products like this will help Customers adopt Public Cloud Environment easily and rely more on their Disaster Recovery Solutions in Cloud.  

![Gartner Veeam.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629759076002/OfqKYUsc_.jpeg)

Feel free to follow along and Let me know if you have any questions or improvements I can provide.

I hope you like the Blog: "Veeam Backup for Azure". 

Thanks for the read. Follow for more Awesome Azure and AWS Content.

Regards,   
Jineshkumar Patel  





 


