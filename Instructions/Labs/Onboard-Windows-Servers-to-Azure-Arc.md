# Lab 01: Onboard Windows Servers to Azure Arc

### Estimated Duration: 110 Minutes

## Overview

In this lab, you will onboard on-premises Hyper-V VMs to Azure Arc for Azure Management.

Azure Arc allows you to manage your hybrid IT estate with a single pane of glass by extending the Azure management experience to your on-premises servers that are not ideal candidates for migration. 

## Lab Objectives

- Task 1: Onboard On-prem servers to Azure Arc-enabled server

## Task 1: Onboard On-prem servers to Azure Arc-enabled server

In this task, you will deploy and configure the Azure Connected Machine agent on a Windows machine hosted outside of Azure, to ensure that it can be managed through Azure Arc-enabled servers.

1. If you are not logged in already, click on the Azure portal shortcut that is available on the desktop and log in with the Azure credentials below.

    * Azure Username/Email: <inject key="AzureAdUserEmail"></inject> 
    * Azure Password: <inject key="AzureAdUserPassword"></inject>

1. In the **search resources, services and docs bar (1)**, type **Azure arc** and select **Azure arc (2)** from Services, as shown below:
   
    ![Picture 1](../Media/ch-1.png "search azure arc")
  
1. On the **Azure Arc** page, select **Machines (1)** under **Azure Arc Resources**, click on **+ Add/create (2)** and then **Add a Machine (3)**.
    
    ![Picture 1](../Media/ch-2.png "search azure arc")
    
1. In the **Add servers with Azure Arc** page, click **Generate script** under **Add a single server**.

    ![Picture 1](../Media/ch-3.png "search azure arc")
    
1. Under the **Basics** tab, fill in the following details:
     
   - Subscription: **Select your subscription**
    
   - Resource group: **SmartHotelHostRG (1)**
  
   - Region: Select **<inject key="Region" enableCopy="false" /> (3)**
   
   - Operating system: **Windows (4)**
   
   - Leave other values as default and Click on **Download and run script (5)**
   
       ![Picture 1](../Media/ch-4.png "search azure arc")

1. Under the **Download and run script** tab, **copy (1)** the entire script and paste it into Notepad, as it will be used in the further steps and then click on **Close (2)**.

    ![Picture 1](../Media/ch-5.png "copy script")
    
1. Go to the **Start (1)** button in the VM, search for **Hyper-V Manager (2)** there and select it. 

    ![Picture 1](../Media/upd-hyper-v-manager.png "Hyper-V Manager")

   > **Note:** You can also open the **Hyper-V manager** by clicking on the icon that is present in the taskbar. 
    
1. In Hyper-V Manager, select **HOSTVMS<inject key="DeploymentID" enableCopy="false" />**. 
  
    ![Picture 1](../Media/HOL3-EX1-S10.png "Hyper-V Manager")
    
1. In Hyper-V Manager, select the **AzureArcVM (1)** VM, then select **Start (2)** on the right if not already running.

    ![Picture 1](../Media/HOL3-EX1-S11.png "Start AzureArcVM")    
    
1. In Hyper-V Manager, select the **AzureArcVM (1)** VM, then select **Connect (2)** on the right.

    ![Picture 1](../Media/secure4.png "Connect to AzureArcVM")  
    
1. In the Connect to AzureArcVM pop-up, click on **Connect** and then log into the VM with the **Administrator password**: **<inject key="SmartHotel Admin Password" />** (the login screen may pick up your local keyboard mapping, use the 'eyeball' icon to check).
 
    ![Picture 1](../Media/HOL3-EX1-S13.png)
    
1. From the **Start (1)** menu of the AzureArcVM, search for **Windows Powershell (2)** and open it **(3)**.

    ![Picture 1](../Media/upd-powershell.png)
      
1. In PowerShell, run the below command to set the execution policy as unrestricted.

    ```
    Set-ExecutionPolicy -ExecutionPolicy unrestricted
    ```

   > **Note:** Type **Y** when prompted.

1. Now, run the whole script that you copied in Notepad earlier in step 7.

1. After running the script, packages will be installed, and then you will be directed to a pop-up browser page to log into your Azure account for authentication purposes. Use the below Azure credentials:

    * Azure Username/Email: <inject key="AzureAdUserEmail"></inject> 
    * Azure Password: <inject key="AzureAdUserPassword"></inject> 

   > **Note:** Move back to the PowerShell pane, and now you have connected your AzureArcVM to Azure successfully.
   
   >**Note**: On the Welcome to Microsoft Edge page, select  **Start without your data**. On **Stay current with your browsing data**, select **Confirm and continue**, and on the help for importing Google browsing data page, select the  **Continue without this data**  button. Then, proceed to select  **Confirm and start browsing**  on the next page has a context menu.
    
    ![Picture 1](../Media/upd-package.png)
     
 1. Close the AzureArcVM, navigate to the Azure portal, go back to the **Azure Arc** page, select **Machines (1)** under **Infrastructure** and now verify that a server is connected successfully **(2)**.

    **Note:** The name of the new server added could be different. You might have to refresh to see the new server.
    
    ![Picture 1](../Media/secure5.png)
     
     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
     > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
     > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
     > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help

     <validation step="7872d02c-327e-400c-bea2-978752ec1e82" />
    
## Summary

In this lab, you explored how to deploy and configure the Azure Connected Machine agent on a Windows machine hosted outside of Azure. You learnt  about creating Azure Arc-enabled servers so that they can manage the Windows machine.

### You have successfully completed the lab!
### Click on Next >> to procced with next Lab.
![](../Media/ch-5.8.png) 
