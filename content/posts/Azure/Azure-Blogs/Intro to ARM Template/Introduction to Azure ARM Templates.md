---
title: "Introduction to ARM Templates"
date: 2020-06-08T08:06:25+06:00
description: All about Azure ARM Templates.
menu:
  sidebar:
    name: Introduction to ARM Templates
    identifier: Introduction to ARM Templates
    parent: Azure-Blogs
    weight: 10
hero: images/forest.jpg
tags: ["Azure","Cloud", "ARM", "IaC"]
categories: ["Basic"]
---

## Introduction to ARM Templates  
(AZURE IaC DevOps)

 

> **ARM (Azure Resource Manager)Templates ** are what really gives us the ability to roll out Azure “Infrastructure as code”.  

They are  project's infrastructure as Code in a declarative and reusable Template. A way to declare the objects/resources you want, the types, its names, and properties in a JSON ( JavaScript Object Notation ) file format which can be checked into source control and managed like any other code file. The templates can be versioned and saved in the same source control repository as your development project.  

**The advantages to Infrastructure as a Code** are:  

- Consistent configurations, Repeatable results.
- Improved scalability and Faster deployments
- Better traceability (Tracked deployments)  
- Integration with CI/CD
- Built-in validation and Testing


**How ARM Templates configured ?**   
The template uses declarative syntax.  
- The declarative syntax is a way of building the structure and elements that outline what resources will look like without describing its control flow.
- ARM templates allow you to declare what you intend to deploy without having to write the sequence of programming commands to create it. In an ARM template, you specify the resources and the properties for those resources. Then Azure Resource Manager uses that information to deploy the resources in an organized and consistent manner.

NOTE :  Resource Manager orchestrates the deployment of the resources so they're created in the correct order. When possible, resources will also be created in parallel, so ARM template deployments finish faster than scripted deployments.
![2-template-processing.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629339371692/bXf-8L464N.png)

**What is ARM Template JSON File Structure? **  
The template files are made up of the following elements:  


- **schema:** A required section that defines the location of the JSON schema file that describes the structure of JSON data. The version number you use depends on the scope of the deployment and your JSON editor.  
- **contentVersion:** A required section that defines the version of your template (such as 1.0.0.0). You can use this value to document significant changes in your template to ensure you're deploying the right template.    
- **apiProfile: **An optional section that defines a collection of API versions for resource types. You can use this value to avoid having to specify API versions for each resource in the template.

- **parameters:**  An optional section where you define values that are provided during deployment. These values can be provided by a parameter file, by command-line parameters, or in the Azure portal.  
- **variables:** An optional section where you define values that are used to simplify template language expressions.

- **functions:** An optional section where you can define user-defined functions that are available within the template. User-defined functions can simplify your template when complicated expressions are used repeatedly in your template.  
- **resources:** A required section that defines the actual items you want to deploy or update in a resource group or a subscription.  
- **output:** An optional section where you specify the values that will be returned at the end of the deployment.  

**File structure of a ARM Template .JSON file **
```
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {  },
  "variables": {  },
  "functions": [  ],
  "resources": [  ],
  "outputs": {  }
}
``` 

**To be honest,** It is very tedious and error pron way to create an ARM template from scratch. But Don't worry, Azure has us covered.  

Visual Studio Extension to the rescue.  

![3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630341932589/uOHSsbVRz.png)

The Azure Resource Manager (ARM) Tools for Visual Studio Code provides language support, resource snippets, and resource auto-completion to help you create and validate Azure Resource Manager templates.  

Also, 
Azure Portal has a quick and easy way to generate ARM Templates from basic configuration created using Portal. You do not need to deploy the resources using azure portal. Just Download the Template as it has created while configuring the basic resource creation process on the azure portal. And then we can edit, add, remove, customize, and Improve the template to make it Deployment ready for us as we desire.  

I feel that is the quick and easy way to create new ARM Templates.

For Example, 

![download-template-before-deployment.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629342684178/40zShY7C6.png)

In above Screenshot, Shows a "Storage Account" Resouce creation (It can be any azure resource) using Azure Portal.  

- Select Review + create on the bottom of the screen. **DO NOT CLICK** Create in the next step.

- Select **Download a template for automation** on the bottom of the screen. The portal shows the generated template: 

- Select **Download** Template as per,

![Capture.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629343614767/tW2I5UDwv.jpeg)

The downloaded JSON file can be open in VS Code or a normal Notepad Application.

>If you notice there are parameters defined like "location" , "StorageAccounrName" , "AccountType", "Kind", "accessTier", "minimumTLSVersion" "AllowBlob/SharedKeyAccess" and its Values as per, 

![parameters.JPG](https://cdn.hashnode.com/res/hashnode/image/upload/v1629343843029/WcMroF_sg.jpeg)

>You can edit and Customize the "Value" of each parameter as per your desired configuration to make it a Custom ARM Template. 

> Once Desired Configuration on Custom ARM Template is set by the Edit of the JSON file.
You can Deploy the Custom Template directly back to Azure Portal. 
Check below, 
![azure-resource-manager-template-library (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629343968594/ntH7-xqjR.png)

![azure-resource-manager-template-tutorial-portal-notification.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629344409085/L4Sthupky.png)  

Or 
How Cool !! Right?  
And this is just a basic example I give here to understand the concept of ARM Template.  
 
You can make a custom ARM Template with much more using almost all Azure Resources and make it deploy ready and add it to your code repository for version control and CI/CD deployments. 

Or use Azure CLI 
Create Resource group  

az deployment group create \
  --name blanktemplate \
  --resource-group myResourceGroup \
  --template-file $templateFile  

Deploy your created Template.json file  

$templateFile="{provide-the-path-to-the-template-file}"
az deployment group create \
  --name blanktemplate \
  --resource-group myResourceGroup \
  --template-file $templateFile  

![12334.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630342944713/0v395wAuD.png)  

And verify from Portal of our successful ARM teplate deployment  

![33333.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630343024469/CC_-WzHLL.png)  


Resource to Learn more :  
Microsoft Azure Github Repo for multiple examples of ARM Templates
[AzureStack-QuickStart-Templates](https://github.com/Azure/AzureStack-QuickStart-Templates)  

Feel free to try and Let me know if you have any questions or improvements I can provide.

I hope you like the Blog: Introduction to ARM Templates.  
Thanks for the read.
Follow for more Awesome Azure and AWS Content.

Regards,  
Jineshkumar Patel







