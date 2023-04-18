---
title: "SYNC your On-Premise AD  with AZURE AD"
date: 2020-06-08T08:06:25+06:00
description: How-To SYNC your On-Premise AD  with AZURE AD (Hands-On).
menu:
  sidebar:
    name: SYNC your On-Premise AD  with AZURE AD
    identifier: SYNC your On-Premise AD  with AZURE AD
    parent: Azure-Blogs
    weight: 10
hero: images/forest.jpg
tags: ["Azure","Cloud", "AzureAD", "Identity"]
categories: ["Basic"]
---

## How-To SYNC your On-Premise AD  with AZURE AD (Hands-On)

In this Tutorial Blog, We will integrate a Single Forest On-Premise Active Directory (AD) with our Azure Active Directory(AAD) using   
Azure AD Connect > **"Azure AD cloud sync"**

### What is Azure AD Connect cloud sync?  
Azure AD Connect Cloud Sync is a cloud service alternative to Azure AD Connect software. The organization deploys one or more lightweight agents in their on-premises environment to bridge AD and Azure AD. The configuration is done in the cloud.

### Prerequisites  
1.   Global administrator account on your Azure AD.  
2.  Tenant in Azure Active Directory.    
3.  On-Premise AD Server Administrator Access.   

My Set up    
1. Server 2016 running from VirtualBox. Conside it On-Prem Server. 
2. AD DS Role Installed (AD Server.)(Local Forest Domain is JP.local) 
3. Azure Portal Global Administrator access.  

### Step by step guide to Follow  
1.  Create Azure AD and Create a Tanent  
Tanent Type : Azure Active Directory
![AAAAAAAA.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631479733088/Htsalj-S3.jpeg)
Configure the Organization Name and Domain Name.  Review+Create 
![AAA.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631480485379/pE4dRQRlb.jpeg)

2.  Download **Azure AD cloud sync** Agent and Move it to your Local On Premise Active Directory Server  
![CCCCCC.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631480787404/38FGiPXsZ.jpeg)  

3.  **Installing AADConnectProvisioningAgentSetup.exe on On Prem AD Server.  **
![1.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631481425696/fwW0wthaL.jpeg)
Connect/Authenticate Login to Azure AD using Global Admin Account created for Azure AD Directory. 
![2 authenticate.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631481439934/guAxY7uxQ.jpeg)
Configure Service Account
![3 Service account Domain Admin.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631481487489/ifRqtbhki.jpeg)
Connect On Prem Active Directory Domain (Mine is JP.local)  
![4 Directory local.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631481535766/62QbvijVf.jpeg)
Agent Install Configuration Confirm Page.  
Active Directory Configuration to Local Domain (JP.LOCAL)    
Azure Active Directory Global Administrator Login configuration.   
![5 final confirm.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631481625673/F1rALv-I5q.jpeg)
Your agent Installation and Configuration is complete. Provision on Azure AD Portal.
![6 Complete.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482072044/TRrbYkmy8.jpeg)

4. Azure portal agent verification by > Azure AD> Azure AD Connect Cloud Sync > Review All Agents >It shows Active for my AD Machine.
![7 Verified Agents.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482172272/iXTXpZ_as.jpeg)
Also, verify on On-Premise AD Server Services where "Azure AD Connect Agent" Services are running,  
![8 Services Verified on local.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482310087/XVIheF2Rg.jpeg)
**So far so good. Verified. Status: Active.**  

5.  Configure Azure AD Connect cloud sync    
Portal > Azure AD > Azure AD Connect > Manage Azure AD cloud sync > New Configuration.  
![11. New configuration on AAD Connect sync.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482704144/2KcP6vrq-.png)
It will automatically filled recently installed AD Connect Cloud Sync Agent Domain (Mine is JP.local)
![12 new configuration asking sync which AD.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482767364/-GSnMo9tf.jpeg)  
Next will allow to edit this provisioning configuration which asks Configuration Scope for Domain or if you want to use any Filter for scope for sync.  Also Validate , Notification settings and deploy.  
![15 Azure aD Sync Configuration Save.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631482936097/VrugNgUVL.jpeg)
Great ! Saved and My AD Provisioning for JP.local domain is showing **"HEALTHY" STATUS **
![16 healthy local domain AD.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1631483451965/FVRQuX34H.jpeg)
6.  Verify users are created and synchronization is occurring  
For this Test, I created 4 Users (First, Second, Third, Fourth) 
![18 Local AD Created 4th User.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631483091137/8K3gzAr4l.png)

**And Wooooalllaaaa!!**  It all synced in few Seconds to my Azure AD under all Users.  Note : Directory Synced: YES for local AD Synced Users.  
![19 all 4 users synced.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631483183671/GwbQ9EkBo.png)

Managing Users from Microsoft 365 Admin Center    
I could have also assigned an Administrator Role and have New User signed in into MS 365 Admin Center to manage AD Administration.  
![20 Office 365 Admin Center Access All Users.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631483727577/T-brXJA1v.png)

### We have now successfully configured a hybrid identity environment between On-Prem AD and Azure AD using Azure AD Connect cloud sync.  


Hope you followed up with this hands-on tutorial.
Thank you for the read. I appreciate your time. Let me know if you have any questions or queries during following along with the steps.

Follow for more Azure and AWS Content.

Regards,  
Jineshkumar Patel
 
