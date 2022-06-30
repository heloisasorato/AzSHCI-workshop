# Lab 5: Deploying Ubuntu on Stack HCI cluster 

Now that you have create a Windows Virtual Machine in your Azure Stack HCI, we are deploying an Ubuntu vm.

Task 1: Download .Iso files
-----------
In this step, you will download a Ubuntu Server 20.04 .Iso file and upload the .Iso to your Clustered Shared Volume you created in Task 1.

### Download an Ubuntu Server 20.04 .Iso ### 
 
1. Please download Ubuntu Server 20.04 image file from [here](https://releases.ubuntu.com/20.04/ubuntu-20.04.4-live-server-amd64.iso)
 
2. The download of the ISO file should automatically start. Once completed you should find it in your Downloads folder.

### Upload the .Iso files to your CSV ###
 
1. Open Windows Admin Center, click on your previously deployed cluster, azstackcluster.contoso.com
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/media/fran1.png "Download .Iso files")
 
2. On the left hand navigation, under Compute select Servers and then Inventory.
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran2.png "Download .Iso files")

3. Click on node AzHOST1 and then click in Manage
 
    ![Download .Iso files](./media/fran3.png "Download .Iso files")
 
4. On the left, select Files & file sharing
  
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran4.png "Download .Iso files")
  
5. Open the folder C:\ClusterStorage\S2D_vDISK1
 
 
6. Click in the "…" and then Upload
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran6.png "Download .Iso files")
  
7. Click in Select Files, search for the .iso file in Downloads and click in Open, and then Submit. 
 
    ![Download .Iso files](https://raw.githubusercontent.com/CloudLabsAI-Azure/AIW-Hybrid-cloud-solutions/event-27/HOL-4-azure-stack-hci/media/fran7.png "Download .Iso files")
 
8. It takes around 5-10 minutes to get successfully uploaded. After that, please move on to the next task.

Task 2: Deploy an Ubuntu Server 20.04 virtual machine
----- 
In this step, you will deploy an Ubuntu Server 20.04 virtual machine via Windows Admin Center.

1. Once logged into the **Windows Admin Center**, click on your previously deployed cluster, **azstackcluster.contoso.com**

2. On the left hand navigation, under **Compute** select **Virtual machines**.  
    
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm1.png "Deploy an Ubuntu Server 20.04 virtual machine")

3. On the **Virtual machines** page, select the **Inventory** tab, and then click on **Add** and select **New**.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/newvm.png "Deploy an Ubuntu Server 20.04 virtual machine")
 
4. In the New virtual machine pane, enter UbuntuVM for the name, and enter the following pieces of information, then click Create
 
     * Generation: Generation 2 (Recommended)
 
     * Host: Leave as recommended
 
     * Path: leave default
 
     * Virtual processors: 2
 
     * Startup memory (GB): 2
 
        * Use dynamic memory: -
 
     * Network: sdnSwitch
     
     * Virtual Network:	TenantNetwork1
     
     * Virtual Subnet:	TenantSubnet1 (192.172.33.0/24)
     
     * IP Address:	192.172.33.10
 
     * Storage: Add, then Create an empty virtual hard disk and set size to 30GB
 
     * Operating System: Install an operating system from an image file (.iso). Select the Ubuntu Server 20.04 Iso file!
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-01.png "Deploy an Ubuntu Server 20.04 virtual machine")
      
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-02.png "Deploy an Ubuntu Server 20.04 virtual machine")  
 
5. The creation process will take a few moments, and once complete, UbuntuVM should show within the Virtual machines view

6. Click on the VM name VM002 and then Click on Settings to view all VM properties. Click on Security
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-03.png "Deploy an Ubuntu Server 20.04 virtual machine")

7. Make sure to change the Secure Boot template to "Microsoft UEFI Certificate Authority" in the Template drop down box, and click save security settings. Click Close.

      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-06.png "Deploy an Ubuntu Server 20.04 virtual machine")

8. Click on Power button and select Start - within moments, the VM should be in a running state soon.

      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-04.png "Deploy an Ubuntu Server 20.04 virtual machine")

9. Click on Connect and select connect button from the drop down- you may get a VM Connect prompt.
 
      ![Deploy an Ubuntu Server 20.04 virtual machine](./media/vm002-05.png "Deploy an Ubuntu Server 20.04 virtual machine")

10. When prompted with the certificate prompt, click Connect and enter Password as `Password01`.
  
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/fran15.png "Deploy an Ubuntu Server 20.04 virtual machine")

11. Once the integrity check is done you will be able to select your language. Select English.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu01.png "Deploy an Ubuntu Server 20.04 virtual machine")

12. On the Installer update available screen, select "Continue without updating"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu02.png "Deploy an Ubuntu Server 20.04 virtual machine")

13. On the Keyboard configuration screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu03.png "Deploy an Ubuntu Server 20.04 virtual machine")

1. On the Network connections screen, remember the assigned IP address and select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu04.png "Deploy an Ubuntu Server 20.04 virtual machine")

14. On the Configure proxy screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu05.png "Deploy an Ubuntu Server 20.04 virtual machine")

15. On the Configure Ubuntu archive mirror screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu06.png "Deploy an Ubuntu Server 20.04 virtual machine")

16. On the Guided storage configuration screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu07.png "Deploy an Ubuntu Server 20.04 virtual machine")

17. On the storage configuration screen, select "Done" and then Select "Continue" to confirm the destructive action popup screen.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu08.png "Deploy an Ubuntu Server 20.04 virtual machine")
    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu09.png "Deploy an Ubuntu Server 20.04 virtual machine")

18. On the Profile setup screen complete the fields a below and then select "Done"
     * Your name: administrator
 
     * Your server's name: ubuntuvm
 
     * Pick a username: administrator
 
     * Choose a password: Password01

     * Confirm your password: Password01

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu10.png "Deploy an Ubuntu Server 20.04 virtual machine")

19. On the Enable Ubunutu Advantage screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu11.png "Deploy an Ubuntu Server 20.04 virtual machine")

20. On the SSH setup screen, select "Install openSSH server" and select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu12.png "Deploy an Ubuntu Server 20.04 virtual machine")

21. On the Featured Server snaps screen, select "Done"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu13.png "Deploy an Ubuntu Server 20.04 virtual machine")

22. Now wait until you get the Install complete! screen and select "Reboot Now"

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu14.png "Deploy an Ubuntu Server 20.04 virtual machine")

23. On the following screen press "ENTER", now the virtual machine will reboot.

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu15.png "Deploy an Ubuntu Server 20.04 virtual machine2")

24. Once the virtual machine is up and running try to login!

    ![Deploy an Ubuntu Server 20.04 virtual machine](./media/ubuntu16.png "Deploy an Ubuntu Server 20.04 virtual machine")
