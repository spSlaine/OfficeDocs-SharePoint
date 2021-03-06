---
title: "Deploying SharePoint Server 2016 with SQL Server AlwaysOn Availability Groups in Azure"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 10/19/2017
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: sharepoint-server-itpro
localization_priority: Priority
ms.collection:
- Ent_O365
- IT_Sharepoint_Server
- IT_Sharepoint_Server_Top
- Strat_O365_Enterprise
ms.custom:
- Ent_Solutions
ms.assetid: af7cf3e7-94b1-4a5d-8cb9-80c5a0b397f2
description: "Summary: Get an overview of deploying SharePoint Server 2016 in Microsoft Azure with links to each phase of the deployment."
---

# Deploying SharePoint Server 2016 with SQL Server AlwaysOn Availability Groups in Azure

 **Summary:** Get an overview of deploying SharePoint Server 2016 in Microsoft Azure with links to each phase of the deployment. 
  
Step through the deployment an intranet-only, high availability SharePoint Server 2016 farm in Azure with these virtual machines:
  
- Two SharePoint front end and distributed cache servers
    
- Two SharePoint application and search servers
    
- One cluster majority node server
    
- Two domain controllers
    
Here is the configuration, with placeholder names for each server.
  
**An intranet-only, high availability SharePoint Server 2016 farm in Azure**

![Phase 4 of the SharePoint Server 2016 highly-available farm in Azure with SharePoint servers](../media/8f421518-773f-4b4d-8084-005d8a50c38e.png)
  
Two virtual machines for each role ensure high availability. All of the virtual machines are in a single cross-premises Azure virtual network. Each group of virtual machines for a specific role is in its own subnet and availability set.
  
> [!NOTE]
> Because this VNet is connected to the on-premises network, this configuration does not include jumpbox or monitoring virtual machines on a management subnet. For more information, see [Running Windows VMs for an N-tier architecture](https://docs.microsoft.com/azure/guidance/guidance-compute-n-tier-vm). 
  
## Bill of materials

This baseline configuration requires the following set of Azure services and components:
  
- Nine virtual machines.
    
- Four availability sets.
    
- One cross-premises virtual network with five subnets.
    
- One Azure subscription.
    
Here are the virtual machines and their default sizes for this configuration.
  
|**Item**|**Virtual machine description**|**Gallery image**|**Default size**|
|:-----|:-----|:-----|:-----|
|1.  <br/> |First domain controller  <br/> |Windows Server 2016 Datacenter  <br/> |D2  <br/> |
|2.  <br/> |Second domain controller  <br/> |Windows Server 2016 Datacenter  <br/> |D2  <br/> |
|3.  <br/> |First database server  <br/> |Microsoft SQL Server 2016 Enterprise - Windows Server 2016  <br/> |DS4  <br/> |
|4.  <br/> |Second database server  <br/> |Microsoft SQL Server 2016 Enterprise - Windows Server 2016  <br/> |DS4  <br/> |
|5.  <br/> |Majority node for the cluster  <br/> |Windows Server 2016 Datacenter  <br/> |D2  <br/> |
|6.  <br/> |First SharePoint application and search server  <br/> |Microsoft SharePoint Server 2016 Trial - Windows Server 2012 R2  <br/> |DS4  <br/> |
|7.  <br/> |Second SharePoint application and search server  <br/> |Microsoft SharePoint Server 2016 Trial - Windows Server 2012 R2  <br/> |DS4  <br/> |
|8.  <br/> |First SharePoint front end and distributed cache server  <br/> |Microsoft SharePoint Server 2016 Trial - Windows Server 2012 R2  <br/> |DS4  <br/> |
|9.  <br/> |Second SharePoint front end and distributed cache server  <br/> |Microsoft SharePoint Server 2016 Trial - Windows Server 2012 R2  <br/> |DS4  <br/> |
   
To compute the estimated costs for this configuration, see the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/). 
  
> [!NOTE]
> The Azure Pricing Calculator does not include the additional costs for the SQL Server license for the two virtual machines running SQL Server 2016 Enterprise. See [Virtual Machines Pricing-SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql) for more information. 
  
## Phases of deployment

You deploy this SharePoint Server 2016 farm with the following phases:
  
- [SharePoint Intranet Farm in Azure Phase 1: Configure Azure](http://technet.microsoft.com/library/f957e1ce-0a39-490c-b533-4ddab4f5bb7a%28Office.14%29.aspx)
    
    Create resource groups, availability sets, and a cross-premises virtual network.
    
- [SharePoint Intranet Farm in Azure Phase 2: Configure domain controllers](http://technet.microsoft.com/library/5f80cdb8-d6d1-45f0-9710-d30544fcb3e6%28Office.14%29.aspx)
    
    Create and configure replica Windows Server Active Directory (AD) domain controllers
    
    > [!NOTE]
    > SharePoint Server 2016 also supports the use of [Azure Active Directory (AD) Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) as a substitute for virtual machines running as domain replicas. However, at this time, this deployment guide only describes the use of virtual machine-based replica domain controllers. 
  
- [SharePoint Intranet Farm in Azure Phase 3: Configure SQL Server Infrastructure](http://technet.microsoft.com/library/b71ccbbf-37c0-46c2-a403-20934e1e104e%28Office.14%29.aspx)
    
    Create and configure the SQL Server virtual machines, prepare them for use with SharePoint, and create the cluster.
    
- [SharePoint Intranet Farm in Azure Phase 4: Configure SharePoint servers](http://technet.microsoft.com/library/8c733fb9-18b9-4770-b90b-364bd7ab30d1%28Office.14%29.aspx)
    
    Create and configure the four SharePoint server virtual machines.
    
- [SharePoint Intranet Farm in Azure Phase 5: Create the availability group and add the SharePoint databases](http://technet.microsoft.com/library/62d0b8d3-e8ea-4523-a69f-62623fb340fb%28Office.14%29.aspx)
    
    Prepare databases and create a SQL Server AlwaysOn availability group.
    
This configuration is a prescriptive, phase-by-phase guide for a predefined architecture to create a highly available intranet SharePoint Server 2016 farm in Azure infrastructure services. Keep the following in mind:
  
- If you are an experienced SharePoint implementer, feel free to adapt the instructions in phases 3 through 5 and build the farm that best suits your needs. 
    
- If you already have an existing Azure hybrid cloud deployment, feel free to adapt or skip the instructions in phases 1 and 2 and host the new SharePoint farm on the appropriate set of subnets. 
    
To build a dev/test environment or a proof-of-concept of this configuration, see [Intranet SharePoint Server 2016 in Azure dev/test environment](intranet-sharepoint-server-2016-in-azure-dev-test-environment.md).
  
## Next step

Start the configuration with [SharePoint Intranet Farm in Azure Phase 1: Configure Azure](http://technet.microsoft.com/library/f957e1ce-0a39-490c-b533-4ddab4f5bb7a%28Office.14%29.aspx).
  
> [!TIP]
> For a set of files to more quickly deploy your SharePoint Server 2016 high availability farm in Azure, see the [SharePoint Server 2016 High Availability Farm in Azure Deployment Kit](https://gallery.technet.microsoft.com/SharePoint-Server-2016-3d3d9071). 
  
## See also

#### Concepts

[Install SharePoint Server](../install/install.md)
#### Other Resources

[SharePoint Server 2016 in Microsoft Azure](sharepoint-server-2016-in-microsoft-azure.md)
  
[Designing a SharePoint Server 2016 farm in Azure](designing-a-sharepoint-server-2016-farm-in-azure.md)

