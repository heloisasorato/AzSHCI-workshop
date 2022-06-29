Explore Azure Arc integration and Azure services

## Overview

Now that you have create a Kubernetes cluster and a Virtual Machine in your Azure Stack HCI, you can now explore Azure Arc and other Azure services. This time we will not provide you a step-by-step guide, so that you can explore by yourself and together with your team and coach.

Task 1: Explore Azure Hybrid Services in WAC
----

Relevant documentation:

[Connecting to Azure Hybrid Services](https://docs.microsoft.com/en-us/windows-server/manage/windows-admin-center/azure/)


Task 2: Arc-enabled the Windows Server 2019 VM you just created
----

Relevant documentation: 

[Plan and deploy Azure Arc-enabled servers](https://docs.microsoft.com/en-us/azure/azure-arc/servers/plan-at-scale-deployment)

Task 3: Apply Azure Policy, VM Insights and Azure Defender for your VM and Kubernetes cluster
----

Relevant documentation: 

[Azure Policy built-in definitions for Azure Arc-enabled servers](https://docs.microsoft.com/en-us/azure/azure-arc/servers/policy-reference)
[Azure Policy built-in definitions for Azure Arc-enabled Kubernetes](https://docs.microsoft.com/en-us/azure/azure-arc/kubernetes/policy-reference)

[Azure Monitor Container Insights for Azure Arc-enabled Kubernetes clusters](https://docs.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-enable-arc-enabled-clusters#create-extension-instance-using-azure-portal)
[Monitor a hybrid machine with VM insights](https://docs.microsoft.com/en-us/azure/azure-arc/servers/learn/tutorial-enable-vm-insights)

[Protect non-Azure resources using Azure Arc and Azure Security Center](https://techcommunity.microsoft.com/t5/azure-security-center/protect-non-azure-resources-using-azure-arc-and-azure-security/ba-p/2277215)

Task 4: Enable Azure Backup for your nodes and VMs
----

Relevant documentation: 

[Backup your Windows Servers from Windows Admin Center with Azure Backup](https://docs.microsoft.com/en-us/windows-server/manage/windows-admin-center/azure/azure-backup#setup-azure-backup)
[Back up Azure Stack HCI virtual machines with Azure Backup Server](https://docs.microsoft.com/en-us/azure/backup/back-up-azure-stack-hyperconverged-infrastructure-virtual-machines)

Task 5: Enable Azure Security Center 
----

Relevant documentation: 

[Protect Windows Admin Center resources with Security Center](https://docs.microsoft.com/en-us/azure/security-center/windows-admin-center-integration)




Congratulations
You've reached the end of the evaluation guide. In this guide you have:

* Deployed/Configured a Windows Server 2019 Hyper-V host in Azure to run your nested sandbox environment
* Deployed the AKS on Azure Stack HCI management cluster on your Windows Server 2019 Hyper-V environment
* Deployed a target cluster to run applications and services
* Optionally integrated with Azure Arc and deployed a sample application
* Set the foundation for further learning!

Great work!
**Setup the lab in your own Azure Subscription.**
This lab is based on the the following work by Matt McSpirit: https://github.com/mattmcspirit/hybridworkshop
If you want to setup the lab within your own Azure subscription and run through additional scenarios as well, you can go to the above GitHub repo and perform as mentioned.
