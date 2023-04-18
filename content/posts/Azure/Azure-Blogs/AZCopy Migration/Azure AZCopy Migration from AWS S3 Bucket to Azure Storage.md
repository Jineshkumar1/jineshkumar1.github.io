---
title: "Data Migration from AWS S3 Bucket to Azure Storage"
date: 2022-06-08T08:06:25+06:00
description: Data Migration from AWS S3 Bucket to Azure Storage
menu:
  sidebar:
    name: Data Migration from AWS S3 Bucket to Azure Storage
    identifier: Data Migration from AWS S3 Bucket to Azure Storage
    parent: Azure-Blogs
    weight: 51
hero: images/forest.jpg
tags: ["Azure","Cloud", "Azure Migration", "Data", "Azure Storage"]
categories: ["Basic"]
---

## Azure AZCopy Migration from AWS S3 Bucket to Azure Storage

Components we will use, 

- Install AZCopy  
- Data on AWS S3 bucket which will be the source.  Azure Storage Account and Container created there which will be Target.  
- Access and Authorization with Azure and AWS 
(Using SAS Token and SAK and SKI) 

Don't worry if you are new to this, I have provided Step by Step Guide on how to use all the above components and AZCopy to migrate Data from AWS S3 to Azure Container.

Follow along, 

Download Azcopy from, 
https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10


- We have to Install AZCopy and start azcopy.exe using CLI as per, 

![install and list.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629088144705/wzqQT-wb-.jpeg)

 
- Permission to access AWS S3 Bucket and Azure Storage Account 

On AWS Side, We need AWS Access Key ID and AWS Secret Access Key and set it in Azcopy CMD 

>AWS Console > IAM > Users > Select Admin User > Security Credential > Create Access Key 

Download and Set it to our Azcopy CMD Console as per below, 
(For Security purposes, I have dash out SAK and SKI)

![SAK and AKI.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629053322362/-7wIAm8DF.jpeg)

![Set SAK and AKI.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629053546034/mCeX9RlUQ.jpeg)


On Azure side, We need Azure Target Storage Account SAS Token 

> Azure Portal > Target Storage Account > Shared Access Signature > Generate > Copy the SAS Token 
As per shown in below screenshot 

Note : I could have create a SAS Token at Container Level and it would have work as well but to generalize for this blog, I did it at storage account level SAS Token.  

![AzureSASTokenJPG.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629086051083/FtKmMM4Zo1.jpeg)


- Final Command on AZCopy CMD 
We have  
AWS : S3 Bucket Name , Set Access Key ID and Secret Access Key  
Azure : Destination Storage Account Name , 
Target Container Name, 
Copied SAS Token 

Now, what we need to run , 
```
azcopy cp "https://s3.amazonaws.com/[bucket]" "https://[destaccount].blob.core.windows.net/[container]?[SAS]" --recursive=true
```
Mine looked like,  
```
C:\azurelabs\azcopy_windows_amd64_10.11.0>azcopy cp "https://s3.amazonaws.com/**migrationworkload**" "https://**migrationtargetazure**.blob.core.windows.net/**azcopytarget**?sastoken--XXXX--sastoken" --recursive=true
```
![Final Command.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629087278306/pdsOZKrPnq.jpeg)

Job Summary shows,  
How many Files got transferred   
and Final Job Status : Completed. 

And There you go, Files appeared On Target Azure Container.  
Nothing less than Magic.!!!!

![Target Azure Side.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629088683037/TilLQYZ0v.jpeg)
 
Note: AZCopy is a powerful tool. It can be used for clients who wants On-Prem Data migration over to Azure Blob Storage as well. 
The command looks similar to this, 

```
azcopy copy "<local-folder-path>" "https://<storage-account-name>.<blob or dfs>.core.windows.net/<container-name>" --recursive=true
```

Feel free to try and Let me know if you have any questions or improvements I can provide. 

Thanks for the read.  
Follow for more Awesome Azure and AWS Content. 

Regards,</br>
**Jineshkumar Patel**
