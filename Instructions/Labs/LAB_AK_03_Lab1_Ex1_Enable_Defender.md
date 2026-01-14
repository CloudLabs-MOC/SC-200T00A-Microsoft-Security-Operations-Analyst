# Lab 02: Enable Microsoft Defender for Cloud

### Estimated Duration: 60 Minutes

## Overview

In this lab, you will enable Microsoft Defender for Cloud to enhance cloud workload protection and respond to security alerts. You will create a Log Analytics Workspace, enable Microsoft Defender for Cloud, install Azure Arc on an on-premises server, and implement security measures to protect it. 

## Objectives

In this lab, you will perform the following tasks:

- Task 1: Create a Log Analytics Workspace
- Task 2: Enable Microsoft Defender for Cloud
- Task 3: Install Azure Arc on an On-Premises Server
- Task 4: Protect an On-Premises Server

## Architecture Diagram

  ![Picture 1](../Media/SC200-Lab_Diagrams_Mod3_L1_Ex1-1.png)

## Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Log Analytics (1)**, then select **Log Analytics workspaces (2)**.

   ![Picture 1](../Media/ee2.png)

1. Click on **+ Create** from the command bar.
1. Provide the following details and click on **Review + Create (4)**:
    
     - Subscription: Select your **subscription**
     - Resource group: Select **RG-Defender (1)**
     - Name: Provide **workspace-<inject key="DeploymentID" enableCopy="false" /> (2)**  
     - Region: Keep the **default (3)**

       ![Picture 1](../Media/L2T1S3-1301.png)

1. Once the workspace validation has passed, select **Create**. Wait for the new workspace to be provisioned.

## Task 2: Enable Microsoft Defender for Cloud

In this task, you will enable and configure Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Microsoft Defender for Cloud (1)**, then select **Microsoft Defender for Cloud (2)** from the list.

   ![Picture 1](../Media/UP_0004.png)

1. In the left menu for Microsoft Defender for Cloud, under **Management**, select **Environment settings (1)** then scroll down to bottom and **select your Subscription (3)** by expanding **(2)** the Tenant Root Group.

   ![Picture 1](../Media/L2T2S2-1301.png)

1. Review the Azure resources that are now protected with the Defender for Cloud plans.

    >**Important:** If all Defender plans are *Off*, select **Enable all plans (1)**. Select the **Turn on the plan anyways (2)** and then click on **OK (3)**. Select **Save (4)** at the top of the page and wait for the *"Defender plans (for your) subscription were saved successfully!"* notifications to appear.

   ![Picture 1](../Media/L2T2S3-1301.png)

    > **Note:** You can ignore any errors for enabling plans for SQL databses or relational databases.

1. Select the **Settings & monitoring** tab from the Settings area (next to Save).

   ![Picture 1](../Media/ch-8.png)

1. Review the monitoring extensions. It includes configurations for Virtual Machines, Containers and Storage Accounts. Close the "Settings & monitoring" page by selecting the **X** on the upper right of the page.
   
   ![Picture 1](../Media/UP_0005.png)

1. Close the settings page by selecting the 'X' on the upper right of the page to go back to the **Environment settings (1)**.

1. Select the **>** to the left of your **subscription (1)** and select the **workspace-<inject key="DeploymentID" enableCopy="false" />(2)** Log Analytics workspace you created earlier to review the available options and pricing.

   ![Picture 1](../Media/L2T2S6-1301.png)

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**.

## Task 3: Install Azure Arc on an On-Premises Server

In this task, you will install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps are done on a different machine than the one you were previously working on. Look for the Virtual Machine name references.

1. In the Search bar of the Azure portal, search for **Virtual Machines (1)** and select **Virtual Machines (2)** from the Services.

   ![Picture 1](../Media/ee3.png)

1. Click on **Virtual machines (1)** on Compute infrastructure page, Select the **WIN1 (2)** VM.

   ![Picture 1](../Media/ch-1.2.png)

1. Click on **Connect** from the Connect dropdown.

   ![Picture 1](../Media/ch-1.1.png)

1. Click on **Download RDP file** and select **Keep** in the pop-up. hen click on **Open file** when the download completes.

   ![Picture 1](../Media/ee4.png)
   ![Picture 1](../Media/ch-1.3.1.png)

1. Click on **Connect**.

   ![Picture 1](../Media/secure15.png)

1. Navigate to the **Environment** tab above lab guide and copy the VM Username and VM Password which is listed under **Resource Group: WIN-1**.

   ![Picture 1](../Media/ee19.png)

1. **Paste (1)** it in the login pop-up and click on **OK (2)**.

   ![Picture 1](../Media/ee22.png)

1. Click on **Yes**.

   ![Picture 1](../Media/secure18.png)

1. Click on the Start button, search for **Hyper-V Manager** from the bottom Windows search bar, and select to open.

   ![Picture 1](../Media/UP_0009.png "Azure Portal")

1. Click on **LABVM (1)**.

1. Select and right-click on the **WINServer (2)** virtual machine from the virtual machine section in the middle and select start, then again right-click on the **WINServer** virtual machine and select **Connect (3)**.

   ![Picture 1](../Media/L2T3S11-2410.png)

1. If it asks you to press ctrl+alt+dlt, Go-to **actions** in the top of VM toolbar and click on **ctrl+alt+dlt** (**Skip if not asked**)
1. Enter the **Password** as `Password.1!!` when prompted.

    ![Picture 1](../Media/UP_0010.png "Azure Portal")

     > **Note:** To enable the clipboard Right-click on LABVM and select Hyper-V Settings click on **Enhanced session mode policy** and check the **Allow enhanced mode** click on apply Then restart your virtual machine, once vm starts you will get a configuration pop-up click on show more options and select local resources and make sure the clipboard is selected.

1. On the WINServer VM, click on the Azure Portal icon to open the portal.

    ![Picture 1](../Media/L2T3S14-1301.png "Azure Portal")

1. In the **Sign in** dialog box, provide the credentials as listed below:

    * **Azure Username/Email:** <inject key="AzureAdUserEmail"></inject> 
    * **Azure Temporary Acces Pass:** <inject key="AzureAdUserPassword"></inject>

1. Click on **Yes** on the Stay signed in dialog box.
1. In the **search resources, services and docs bar (1)**, type **Azure Arc** and select **Azure Arc (2)** from Services, as shown below:
   
   ![Picture 1](../Media/ee23.png "search azure arc")
  
1. On the **Azure Arc** page, select **Machines (1)** under **Infrastructue**, click on **+ Onboard/create (2)** and then **Onboard existing machine (3)**.
    
    ![Picture 1](../Media/UP_0023.png "search azure arc")

1. Under the **Basics** tab, fill in the following details:
     
   - Subscription: **Select your subscription**
    
   - Resource group: **RG-Defender (1)**
  
   - Region: Select **EAST US (2)**
   
   - Operating system: **Keep it as default**

   - Leave other values as default and click on **Download and run script (3)**

     ![Picture 1](../Media/L2T3S19-2810.png)

1. Scroll down and select the **Download** button.

   ![Picture 1](../Media/secure21-1.png)

   > **Note:** Select **Keep** when prompted in the pop-up.

1. From the **Start (1)** menu of the same VM, search for **Windows Powershell (2)** and open it **(3)**.

   ![Picture 1](../Media/upd-powershell.png)

1. Run the below **command (1)**:

    ```
    cd C:\Users\Administrator\Downloads
    ```

      > **Important:** If you do not have this directory, it most likely means that you are on the wrong machine. Go back to the beginning of Task 4, change to WINServer and start over.

1. In PowerShell, run the below **command (2)** to set the execution policy as unrestricted.

    ```
    Set-ExecutionPolicy -ExecutionPolicy unrestricted
    ```

1. Enter **A (3)** for Yes to All and press Enter.

    ![Picture 1](../Media/L2T3S24-1301.png)

1. Run the below **command (1)** and press enter:  

    ```
    .\OnboardingScript.ps1
    ```

    >**Important:** If you get the error *"The term .\OnboardingScript.ps1 is not recognized..."*, make sure you are doing the steps for Task 3 in the WINServer virtual machine. Other issues might be that the name of the file changed due to multiple downloads, search for *".\OnboardingScript (1).ps1"* or other file numbers in the running directory.

1. Enter **R (2)** to Run once and press Enter (this may take a couple of minutes).

    ![Picture 1](../Media/L2T3S126-1301.png)

1. The setup process will open a new Edge browser tab to authenticate the Azure Arc agent. Select the ODL email <inject key="AzureAdUserEmail"></inject>, wait for the message **"Authentication complete"**, and then go back to the Windows PowerShell window.

    ![Picture 1](../Media/UP_0014.png)

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Onboard existing machines with Azure Arc** to go back to the Azure Arc **Machines** page.

1. Select **Refresh** until WINServer server name appears and the Status is **Connected**.

   ![Picture 1](../Media/L2T3S29-2810.png)

   > **Note:** This could take a couple of minutes.

## Task 4: Protect an On-Premises Server

In this task, you will manually install the required agent on the Windows Server.

1. Search **Data Collection Rules (1)** on azure portal search bar and select **Data collection rules (2)** from Services.

   ![Picture 1](../Media/ee7.png)

1. Select **+ Create** on **Data collection rules** page.

   ![Picture 1](../Media/ch-1.6.png)

1. Provide the following details and click on **Next: Resources (3)**:

   - Rule Name: Enter **WINServer (1)**
   - Resource Group: Select **RG-Defender (2)**
   - Keep the default region
   - Ensure the box for **Windows** is checked under Platform Type

     ![Picture 1](../Media/secure24.png)

1. In the **Resources** tab, click on **+ Add resources (1)**. In the **Select a scope** page, expand the *Scope* column for **RG-Defender**, then select **WINServer (Azure Arc) (2)** and select **Apply (3)**.

   ![Picture 1](../Media/secure23-1.png)

   > **Note:** You may need to set the column filter for *Resource type* to *Server-Azure Arc* if **WINServer (Azure Arc)** is not displayed.

1. Click on **Next: Collect and deliver**
1. In the **Collect and deliver** tab, select **+ Add data source (1)**. In the **Add a data source** page, select **Performance Counters (2)** from *Data source type*.

   ![Picture 1](../Media/secure25.png)

1. Click the **Destination** tab, select **+ Add Destination (1)**. Select **Azure Monitor Logs (2)** in the **Destination Type** dropdown. Select your **workspace (3)** from the drop-down. Click on **Add data source (4)**.

   ![Picture 1](../Media/L2T4S7-1301.png)

1. Click on **Review + Create** and select **Create** after *Validation passed* is displayed.

   ![Picture 1](../Media/ch-1.7.png)

   > **Note:** The **Data Collection Rule** creation initiates the installation of the *AzureMonitorWindowsAgent* extension on **WINServer (Azure Arc)**.

1. In the **Search resources, services and docs** search bar, search for **Azure Arc (1)**, and select **Azure Arc (2)** from the Services. 

   ![Picture 1](../Media/ee8.png)

1. Navigate to **Machines** under Azure Arc resources section and select the **WINServer** which is associated with the **RG-Defender** resource group.

   ![Picture 1](../Media/L2T3S29-2810.png)

1. Select **Extensions (1)** from the left pane under Settings. The **AzureMonitorWindowsAgent (2)** should be listed with a *Status* of **Succeeded**.

   ![Picture 1](../Media/secure28.png)

   > **Note:** The extension can take 5-10 minutes to succeed. You can continue to the next lab and review the extension later. 

## Summary

In this lab, you have enabled Microsoft Defender for Cloud to enhance cloud workload protection and respond to security alerts. You created a Log Analytics Workspace, enabled Microsoft Defender for Cloud, installed Azure Arc on an on-premises server, and implemented security measures to protect it.

### You have successfully completed the lab. Click on Next >> to procced with next Lab.
![](../Media/ch-5.9.png) 
