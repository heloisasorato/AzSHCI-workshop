Exercise 1: Integrate Azure Stack HCI 21H2 with Azure
==============
Overview
-----------

As part of the lab environment, we have already deployed the Azure Stack HCI 21H2 Cluster, so you don't have to deploy it and you can continue registering the already deployed cluster to unlock full functionality.

In this lab you can do all the normal operations you would expect to do with an Azure Stack HCI Cluster located in your Datacenter or Remote/Branch Office. This Lab is meant to be a nested solution that allows you to test, deploy and understand Azure Stack HCI and all of it's components, including Hyper-V, Failover Clustering, Storage Spaces Direct (S2D) and Software Defined Networking (SDN). In this lab we will focus on management of a 2-node cluster, that has been built and deployed for you, as part of this lab. You can work on the suggested scenarios presented in this lab documentation, or try out any scenarios you can come up with, the freedom is yours!

After the deployment is complete, we will have three Virtual Machines on your Azure host, two Azure Stack HCI Hosts named AZSHost1 & 2 and a Management VM, named AZSMGMT. The AZSMGMT VM is another nested Hyper-V Host, that contains 3 more Virtual Machines:

AdminCenter: A Windows 10 Workstation with Admin Center installed
BGP-TOR-Router: A Windows Server running Routing and Remote Access Server
ContosoDC: Windows Server that is our Domain Controller.

Contents
-----------
- [Overview](#overview)
- [Contents](#contents)
- [Complete Registration](#complete-registration)


Azure Stack HCI 21H2 is delivered as an Azure service and needs to register within 30 days of installation per the Azure Online Services Terms.  With our cluster configured, we'll now register your Azure Stack HCI 21H2 cluster with **Azure Arc** for monitoring, support, billing, and hybrid services. Upon registration, an Azure Resource Manager resource is created to represent each on-premises Azure Stack HCI 21H2 cluster, effectively extending the Azure management plane to Azure Stack HCI 21H2. Information is periodically synced between the Azure resource and the on-premises cluster.  One great aspect of Azure Stack HCI 21H2, is that the Azure Arc registration is a native capability of Azure Stack HCI 21H2, so there is no agent required.


## Task 1: Register Azure Stack HCI 21H2 Cluster on Azure portal.

   To complete registration, you have 2 options - you can use **Windows Admin Center**, or you can use **PowerShell**. For this lab, it's recommended to use the PowerShell as it is less likely that you will encounter unpredictible erros in the lab environment, due to WAC installed on the domain controller. In this environment, we will be using PowerShell to register to the Azure Stack HCI cluster.

 We're going to perform the registration from the **HybridHost001** machine, which we've been using with the Windows Admin Center.

1. On **HybridHost001** VM after you have already logged in, click on the windows button and look for **PowerShell ISE** and right-click on it to **Run as administrator**.

    ![Volume created on Azure Stack HCI 21H2](https://raw.githubusercontent.com/CloudLabsAI-Azure/hybridworkshop/main/media/powershell.png "Volume created on Azure Stack HCI 21H2")
    
2. With the Az.StackHCI modules installed, it's now time to register your Azure Stack HCI 21H2 cluster to Azure. However, first it's worth exploring how to check the existing registration status. The following code assumes you are still in the remote PowerShell session open from the previous commands.

     ```powershell
     Invoke-Command -ComputerName azstackcluster -ScriptBlock {
     Get-AzureStackHCI
     } 
     ```
     >Note: If you see the cluster registration status is showing as **Out of Policy**, you can ignore that as there will be no issue during the lab because of this. 
     
    ![Check the registration status of the Azure Stack HCI 21H2 cluster](./media/output.png "Check the registration status of the Azure Stack HCI 21H2 cluster")

As you can see from the result, the cluster is yet to be registered, and the cluster status identifies as **Clustered**. Azure Stack HCI 21H2 needs to register within 30 days of installation as per the Azure Online Services Terms. If it is not clustered within 30 days, the **ClusterStatus** will show **OutOfPolicy**, and if not registered within 30 days, the **RegistrationStatus** will show as **OutOfPolicy**.


3. Now copy the below code and paste it in your PowerShell window, replace *your-subscription-ID-here* with your subscription ID <inject key="Subscription ID" />. After updating the subscription ID, run the PowerShell commands to register your Azure Stack HCI 21H2 to Azure portal. 

   > **Note**: We have already updated the domain user name and password for the local host server. 
   
    ```
    
    Register-AzStackHCI -SubscriptionId *your-subscription-ID-here* -ComputerName azstackcluster.contoso.com
     
     ```

This syntax registers the cluster (azstackcluster.contoso.com), as the current user, with the default Azure region and cloud environment, and using smart default names for the Azure resource and resource group. You can also add the optional -Region, -ResourceName, -TenantId, and -ResourceGroupName parameters to this command to specify these values. Note After June 15, 2021, running the Register-AzStackHCI cmdlet will enable Azure Arc integration on every server in the cluster by default, and the user running it must be an Azure Owner or User Access Administrator. If you do not want the servers to be Arc enabled or do not have the proper roles, pass this additional parameter: -EnableAzureArcServer:$false Remember that the user running the Register-AzStackHCI cmdlet must have Azure Active Directory permissions, or the registration process will not complete; instead, it will exit and leave the registration pending admin approval. Once permissions have been granted, simply re-run Register-AzStackHCI to complete registration. Authenticate with Azure

4. Once dependencies have been installed, you'll receive a popup on **HybridHost001** to authenticate to Azure. Provide your **Azure credentials**.

    ![Login to Azure](./media/azure_login_reg.png "Login to Azure")

5. Once successfully authenticated, the registration process will begin and will take some time to finish. Once completed, you should see a message indicating success, as per below:

    ![Register Azure Stack HCI 21H2 with PowerShell](./media/registered.png "Register Azure Stack HCI 21H2 with PowerShell")

6. Once the cluster is registered, run the following command on **HybridHost001** to check the updated status:

    ```powershell
    Invoke-Command -ComputerName  azstackcluster -ScriptBlock {
    Get-AzureStackHCI
    }
    ```
    ![Check updated registration status with PowerShell](./media/connected.png "Check updated registration status with PowerShell")

You can see the **ConnectionStatus** and **LastConnected** time, which is usually within the last day unless the cluster is temporarily disconnected from the Internet. An Azure Stack HCI 21H2 cluster can operate fully offline for up to 30 consecutive days.

## Task 2: View registration details in the Azure portal ###

Once the registration is complete, you should take some time to explore the artifacts that are created in Azure.

1. Open the Edge browser and **log into https://portal.azure.com** to check the resources created there. In the **search box** at the top of the screen, search for **Stack HCI** and then click on **Azure Stack HCI**

2. You should see a new **cluster** listed, with the name you specified earlier, which in our case, is **AzStackCluster**


3. Click on the **AzStackCluster** and you'll be taken to the new Azure Stack HCI Resource Provider, which shows information about all of your clusters, including details on the currently selected cluster.

    ![Overview of the recently registered cluster in the Azure portal](./media/nwstack.png "Overview of the recently registered cluster in the Azure portal")


### Congratulations! ###
You've now successfully registered your Azure Stack HCI 21H2 cluster!

Next Steps
-----------
In this step, you've successfully registered your Azure Stack HCI 21H2 cluster. With this completed, you can now move on to the next exercise.

Product improvements
-----------
If, while you work through this guide, you have an idea to make the product better, whether it's something in Azure Stack HCI, AKS on Azure Stack HCI, Windows Admin Center, or the Azure Arc integration and experience, let us know! We want to hear from you!

For **Azure Stack HCI**, [Head on over to the Azure Stack HCI 21H2 Q&A forum](https://docs.microsoft.com/en-us/answers/topics/azure-stack-hci.html "Azure Stack HCI 21H2 Q&A"), where you can share your thoughts and ideas about making the technologies better and raise an issue if you're having trouble with the technology.

For **AKS on Azure Stack HCI**, [Head on over to our AKS on Azure Stack HCI 21H2 GitHub page](https://github.com/Azure/aks-hci/issues "AKS on Azure Stack HCI GitHub"), where you can share your thoughts and ideas about making the technologies better. If however, you have an issue that you'd like some help with, read on... 
