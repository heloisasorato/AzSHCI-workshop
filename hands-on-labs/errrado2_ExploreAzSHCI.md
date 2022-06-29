Exercise 2: Explore the management of your Azure Stack HCI 21H2 environment 
==============
Overview
-----------
With the Azure Stack HCI cluster deployed, you can now begin to explore some of the additional capabilities within Azure Stack HCI 21H2 and Windows Admin Center. We'll cover a few recommended activities below, to expose you to some of the key elements of the Windows Admin Center, but for the rest, we'll [direct you over to the official documentation](https://docs.microsoft.com/en-us/azure-stack/hci/ "Azure Stack HCI 21H2 documentation").

Contents
-----------
- [Overview](#overview)
- [Contents](#contents)
- [Create a SDN VM Network](#task-1-create-a-SDN-VM-network)
- [Download .Iso files](#task-2-download-iso-file)
- [Deploy a Windows Server 2019 virtual machine](#task-3-deploy-a-windows-server-2019-virtual-machine)
- [Deploy an Ubuntu Server 20.04 virtual machine](#task-4-deploy-an-ubuntu-server-2004-virtual-machine)
- [Live migrate a virtual machine to another node](#task-5-live-migrate-a-virtual-machine-to-another-node)


Task 1: Create a SDN VM Network
-----------

1. Navigate to **Windows Admin Center -> azstackcluster.contoso.com -> Virtual Networks**. In **Virtual Networks**, select **Inventory**.

2. In **Inventory** select **+ New**

![alt text](https://github.com/microsoft/AzStackHCISandbox/blob/3aceaf8de0f881845cec1a8dd66a1825357bbfa0/Scenarios/Media/Screenshots/03-res/1-02.png "Inventory Screen for Virtual Networks")

3. In the Virtual Network dialog, fill in the following and then click **Submit**:

|   |   |
|---|---|
| Virtual Network Name:  |  **TenantNetwork1**  |
| Address Prefixes:  | add  **192.172.0.0/16**  |
| Subnet Name: | add **TenantSubnet1**   |
| Subnet Address Prefix: | add **192.172.33.0/24**  |

![alt text](https://github.com/microsoft/AzStackHCISandbox/blob/3aceaf8de0f881845cec1a8dd66a1825357bbfa0/Scenarios/Media/Screenshots/03-res/1-07.png "Final screen of creating a virtual network")

4. Wait about a minute and then you should see the following in your Virtual Networks inventory:

![alt text](https://github.com/microsoft/AzStackHCISandbox/blob/3aceaf8de0f881845cec1a8dd66a1825357bbfa0/Scenarios/Media/Screenshots/03-res/1-03.png "Inventory Screen for Virtual Networks")

5. Step 01 is now complete.


Task 2: Download .Iso files
-----------
In this step, you will download a Windows Server 2019 and Ubuntu Server 20.04 .Iso file and upload the .Iso to your Clustered Shared Volume you created in Task 1.

### Download a Windows Server 2019 .Iso ###

1. Please download Windows Server 2019 image file from [here](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.microsoft.com%2Fen-us%2Fevalcenter%2Fevaluate-windows-server-2019%3Ffiletype%3DISO&data=04%7C01%7CFrancisco.Teles%40microsoft.com%7C3f8c97077c47407ea5e108d995653e46%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637705084332755360%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=zUzaHW7hF2BaYdzgw4wd79kNG2p201m775JKlJTveUc%3D&reserved=0)
 
2. Select ISO and complete the form to continue with your details. Download the .iso and saved in the Downloads folder.

### Download an Ubuntu Server 20.04 .Iso ### 
 
1. Please download Ubuntu Server 20.04 image file from [here](https://releases.ubuntu.com/20.04/ubuntu-20.04.4-live-server-amd64.iso)
 
2. The download of the ISO file should automatically start. Once completed you should find it in your Downloads folder.

### Upload the .Iso files to your CSV ###
 
1. Open Windows Admin Center from the desktop is not already opened, click on your previously deployed cluster, azstackcluster.contoso.com
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/media/fran1.png "Download .Iso files")
 
2. On the left hand navigation, under Compute select Servers and then Inventory.
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran2.png "Download .Iso files")

3. Click on node AzSHOST1 and then click in Manage
 
    ![Download .Iso files](./media/fran3.png "Download .Iso files")
 
4. On the left, select Files & file sharing
  
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran4.png "Download .Iso files")
  
5. Open the folder C:\ClusterStorage\S2D_vDISK1
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran5.png "Download .Iso files")
  
 
6. Click in the "…" and then Upload
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran6.png "Download .Iso files")
  
7. Click in Select Files, search for both (Windows Server 2019 and Ubuntu Server 20.04) .iso files in Downloads and click in Open, and then Submit. 
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran7.png "Download .Iso files")
 
8. It takes around 5-10 minutes to get successfully uploaded. After that, please move on to the next task.
 
Task 3: Deploy a Windows Server 2019 virtual machine
----- 
In this step, you will deploy a Windows Server 2019 virtual machine via Windows Admin Center.

1. Once logged into the **Windows Admin Center**, click on your previously deployed cluster, **azstackcluster.contoso.com**

2. On the left hand navigation, under **Compute** select **Virtual machines**.  The central **Virtual machines** page shows you no virtual machines deployed currently
    
    ![Deploy a Windows Server 2019 virtual machine](./media/vm1.png "Deploy a Windows Server 2019 virtual machine")

3. On the **Virtual machines** page, select the **Inventory** tab, and then click on **Add** and select **New**.

    ![Deploy a Windows Server 2019 virtual machine](./media/newvm.png "Deploy a Windows Server 2019 virtual machine")
 
4. In the New virtual machine pane, enter VM001 for the name, and enter the following pieces of information, then click Create
 
     * Generation: Generation 2 (Recommended)
 
     * Host: Leave as recommended
 
     * Path: C:\ClusterStorage\S2D_vDISK1
 
     * Virtual processors: 2
 
     * Startup memory (GB): 4
 
     * Use dynamic memory: Min 2, Max 6
 
     * Network: sdnSwitch
 
     * Storage: Add, then Create an empty virtual hard disk and set size to 30GB
 
     * Operating System: Install an operating system from an image file (.iso). Select the Windows Server 2019 Iso file!
 
      ![Deploy a Windows Server 2019 virtual machine](./media/fran8.png "Deploy a Windows Server 2019 virtual machine")
      
      ![Deploy a Windows Server 2019 virtual machine](./media/fran9.png "Deploy a Windows Server 2019 virtual machine")  
 
5. The creation process will take a few moments, and once complete, VM001 should show within the Virtual machines view

6. Click on the checkbox before the VM and then click on Power button and select Start - within moments, the VM should be running.

    ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran10.png "Deploy a Windows Server 2019 virtual machine")
     
    ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran11.png "Deploy a Windows Server 2019 virtual machine")
  
7. Click on VM001 to view the properties and status for this running VM.
 
    ![Deploy a Windows Server 2019 virtual machine](./media/fran12.png "Deploy a Windows Server 2019 virtual machine")
              
8. Click Connect, and when prompted with the certificate prompt, click Connect and enter Password as `Password01`.
  
    ![Deploy a Windows Server 2019 virtual machine](./media/fran15.png "Deploy a Windows Server 2019 virtual machine")
 
 
9. The VM will be in the UEFI boot summary as below
 
    ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran16.png "Deploy a Windows Server 2019 virtual machine")
 
10. Click in "Send Ctrl + Alt + Del" at the top of the page now and press any key when you see the message "Press any key at boot from CD or DVD…"
 
    ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran17.png "Deploy a Windows Server 2019 virtual machine")
 
11. Click Enter when you see the following interface
 
    ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran18.png "Deploy a Windows Server 2019 virtual machine")
 
12. From there you'll start the OOBE experience. Select the following settings according to your preferences: Language, Time currency and Keyboard

13. Click Install Now, and select the version Windows Server 2019 Standard Evaluation (Desktop Experience):
 
     ![Deploy a Windows Server 2019 virtual machine](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran19.png "Deploy a Windows Server 2019 virtual machine")
 
14. Accept the license terms and select "Custom: Install Windows only (advanced)" and then Next. It will take around 10 minutes for the VM to boot. After that, please insert the lab credentials demo!pass123 and your VM is ready to go!

Task 4: Deploy an Ubuntu Server 20.04 virtual machine
----- 
In this step, you will deploy an Ubuntu Server 20.04 virtual machine via Windows Admin Center.

1. Once logged into the **Windows Admin Center** on **HybridHost001**, click on your previously deployed cluster, **azshciclus.hybrid.local**

1. On the left hand navigation, under **Compute** select **Virtual machines**.  The central **Virtual machines** page shows one virtual machines deployed currently.
    
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm1.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the **Virtual machines** page, select the **Inventory** tab, and then click on **Add** and select **New**.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/newvm.png "Deploy an Ubuntu Server 20.04 virtual machine")
 
1. In the New virtual machine pane, enter VM002 for the name, and enter the following pieces of information, then click Create
 
     * Generation: Generation 2 (Recommended)
 
     * Host: Leave as recommended
 
     * Path: C:\ClusterStorage\Volume01
 
     * Virtual processors: 2
 
     * Startup memory (GB): 2
 
        * Use dynamic memory: -
 
     * Network: ComputeSwitch
 
     * Storage: Add, then Create an empty virtual hard disk and set size to 30GB
 
     * Operating System: Install an operating system from an image file (.iso). Select the Ubuntu Server 20.04 Iso file!
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-01.png "Deploy an Ubuntu Server 20.04 virtual machine")
      
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-02.png "Deploy an Ubuntu Server 20.04 virtual machine")  
 
1. The creation process will take a few moments, and once complete, VM002 should show within the Virtual machines view

1. Click on the VM name VM002 and then Click on Settings to view all VM properties. Click on Security
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-03.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. Make sure to change the Secure Boot template to "Microsoft UEFI Certificate Authority" in the Template drop down box, and click save security settings. Click Close.

      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-06.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. Click on Power button and select Start - within moments, the VM should be in a running state soon.

      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-04.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. Click on Connect and select connect button from the drop down- you may get a VM Connect prompt.
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-05.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. When prompted with the certificate prompt, click Connect and enter Password as `demo!pass123`.
  
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/fran15.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. Once the integrity check is done you will be able to select your language. Select English.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu01.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Installer update available screen, select "Continue without updating"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu02.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Keyboard configuration screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu03.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Network connections screen, remember the assigned IP address and select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu04.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Configure proxy screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu05.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Configure Ubuntu archive mirror screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu06.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Guided storage configuration screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu07.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the storage configuration screen, select "Done" and then Select "Continue" to confirm the destructive action popup screen.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu08.png "Deploy an Ubuntu Server 20.04 virtual machine")
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu09.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Profile setup screen complete the fields a below and then select "Done"
     * Your name: demouser
 
     * Your server's name: vm002
 
     * Pick a username: demouser
 
     * Choose a password: demo!pass123

     * Confirm your password: demo!pass123

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu10.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Enable Ubunutu Advantage screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu11.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the SSH setup screen, select "Install openSSH server" and select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu12.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Featured Server snaps screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu13.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. Now wait until you get the Install complete! screen and select "Reboot Now"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu14.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the following screen press "ENTER", now the virtual machine will reboot.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu15.png "Deploy an Ubuntu Server 20.04 virtual machine2")

1. Once the virtual machine is up and running try to login!

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu16.png "Deploy an Ubuntu Server 20.04 virtual machine")

Task 5: Live migrate a virtual machine to another node
----- 

The final step we'll cover is using Windows Admin Center to live migrate VM001 from it's current node, to an alternate node in the cluster.

1. Still within the **Windows Admin Center** on **HybridHost001**, under **Compute**, click on **Virtual machines**

2. On the **Virtual machines** page, select the **Inventory** tab

3. Under **Host server**, make a note of the node that VM001 is currently running on.  You may need to expand the column width to see the name

4. Next to **VM001**, click the tick box next to VM001, then click **More**.  You'll notice you can Clone, Domain Join and also Move the VM. Click **Move**

    ![Start Live Migration using Windows Admin Center](./media/move.png "Start Live Migration using Windows Admin Center")

5. Select the **Failover Cluster** from the drop down and leave the defaul on **Member server**, for  **Path for the VM's file** select **C:\ClusterStorage\Volume1** from the drop down, under the **ComputeSwitch** select **Computeswitch** and then click **Move**.

    ![Start Live Migration using Windows Admin Center](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/path.png "Start Live Migration using Windows Admin Center")
    
6. The live migration will then begin, and within a few seconds, the VM should be running on a different node.
     
7. Click on **Yes** on the popup of **Credential Security Service Provider CredSSP** and then enter you username as **Hybrid\azureuser** and password as **demo!pass123**.

    ![Start Live Migration using Windows Admin Center](./media/movee1.png "Start Live Migration using Windows Admin Center")
    
8. On the left hand navigation, under **Compute** select **Virtual machines** to return to the VM dashboard view, which aggregates information across your cluster, for all of your VMs.

## In this exercise, you have covered the following:
 
   - Creating a Cluster Shared Volume via Windows Admin Center.
   - Created a Windows and Ubuntu Server via Windows Admin Center
   - Performed a Live Migration

Proceed to the next exercise... 

