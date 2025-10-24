# Lab 04: Connect Windows devices to Microsoft Sentinel using data connectors

### Estimated Duration: 30 Minutes

## Overview

In this lab, you act as a Security Operations Analyst responsible for onboarding Windows hosts into Microsoft Sentinel. 

You will learn how to collect Windows security event telemetry from both Azure virtual machines and non‑Azure Windows servers (on‑premises or other clouds), using the Windows Security Events solution, the Azure Monitor Agent (AMA) with Data Collection Rules (DCRs), and Azure Arc where required.

## Objectives

 In this lab, you will perform the following tasks:
 
- Task 1: Create a Microsoft Sentinel Workspace
- Task 2: Create a Windows Virtual Machine in Azure
- Task 3: Install Azure Arc on an On-Premises Server
- Task 4: Connect an Azure Windows virtual machine
- Task 5: Connect a non-Azure Windows Machine

## Architecture Diagram

  ![Lab overview.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

## Task 1: Create a Microsoft Sentinel Workspace

  > **Note:** Perform this task in **SmartHotelHost** VM (Lab VM). 

  > **Note:** While accessing Sentinel workspace if you see an error that the page was moved to Defender portal, click on the link on the top left side of the page to access the old experience.

   ![](../Media/old-experience.png) 

In this task, you will connect the Microsoft Entra ID connector to Microsoft Sentinel.

 1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

    ![Picture 1](../Media/ee6.png)

 1. Select **+Create** from the command bar.
    
    ![Picture 1](../Media/ch-2.5.png)

 1. Select **uniquenameDefender (1)** and click on **Add (2)**.

    ![Picture 1](../Media/ch-2.6.png)

      > **Note:** In the Microsoft Sentinel free trial activated pop-up, click on **OK**.

## Task 2: Create a Windows Virtual Machine in Azure

  > **Note:** Perform this task in **SmartHotelHost** VM (Lab VM). 

In this task, you will create a Windows virtual machine in Azure.

1. In the azure portal, Select **+ Create a Resource**. 

   ![](../Media/l8e1-1.png)

1. In the **Search services and marketplace** box, enter **Windows 10 (1)** and select **Windows 10 (2)** from the drop-down list.

   ![](../Media/L4T2S2-2410.png)

1. On the **Marketplace** page,  Select the box for **Windows 10**.

   ![](../Media/L4T2S3-2410.png)

1. Open the *Plan* drop-down list and select **Windows 10 Enterprise, version 22H2 (1)**.

1. Select **Start with a pre-set configuration (2)** to continue.

   ![](../Media/L4T2S5-2410.png)

   > **Note:** Select **Dev/Test** and then select **Continue to create a VM** if prompted.

      ![](../Media/ch-2.8.png)

1. On **Create a virtual machine** page, configure the disk and then select **Review + create (11)**. 

    | Setting | Value |
    | --- | --- |
    | Subscription | your default subscription **(1)** | 
    | Resource Group | Select **RG-AZWIN01 (2)**   |
    | Virtual machine name |  Enter **AZWIN01 (3)**  | 
    | Region | **<inject key="Region" enableCopy="false" /> (4)** |

      ![](../Media/ch-2.9.1.png)

    | Setting | Value |
    | --- | --- |
    | Image | **Windows 10 Enterprise, version 22H2 (5)**  | 
    | Size| Should be selected as **Standard_B2s**. If it appears empty, select **See all sizes**, choose the **Standard_DS1_v2 (6)** click **Select**. |

      ![](../Media/ch-2.9.2.png)

    | Setting | Value |
    | --- | --- |
    | Username | Enter **azureuser(7)**  |
    | Password  | Enter **Password.1!! (8)**  |
    | Confirm Password  | Enter **Password.1!! (9)** |

      ![](../Media/l8e1-8.png)
    
1. Select the Checkbox **(10)**, and click on **Review + create (11)**.
    
   ![](../Media/l8e1-9.png)

1. Select **Create**. Wait for the Resource to be created, this may take a few minutes.

   ![](../Media/l8e1-10.png)

   >**Note:** If there is a *Networking* validation failure, select that tab, review its contents, and then select **Review + create** again.

## Task 3: Install Azure Arc on an On-Premises Server

In this task, you will install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

>**Important:** The *Windows Security Events via AMA* data connector requires Azure Arc for non-Azure devices. 

1. Login to the **WIN1** VM by using the RDP file which we have downloaded in the previous lab.

1. In the **WIN1** virtual machine, search for **Hyper-V Manager** from task bar and select to open.

   ![](../Media/l8e1-13.png)

1. Select **LABVM (1)**, then select **WIN2**. Right-click on the **WIN2 (2)** virtual machine and choose **Start**, then click **Continue**. After that, right-click on the **WIN2** virtual machine again and select **Connect (3)**.

   ![](../Media/ch-3.0.png)
 
1. Inside **WIN2** Click on **connect**.
 
   ![](../Media/l8e1-14.png)

1. Enter the **Password** as `Password.1!!` when prompted then hit on **Enter**.

   ![](../Media/l8e3-16.png)

1. In the **WIN2**, click on the Azure Portal icon as shown below:
 
   ![Launch Azure Portal](../Media/sc900-image(1).png)

1. In the **Sign in** dialog box, copy and paste **Email/Username: <inject key="AzureAdUserEmail"></inject>** and then select Next.

1. In the **Enter Temporary Access Pass** dialog box, copy and paste **Password: <inject key="AzureAdUserPassword"></inject>** and then select **Sign in**.

1. In the Search bar of the Azure portal, type **Azure Arc (1)**, then select **Azure Arc (2)**.

   ![](../Media/ee23.png)

1. In the navigation pane under **Azure Arc resources** select **Machines (1)**
1. Select **+ Add/Create (2)**, then select **Add a machine (3)**.

   ![](../Media/ch-2.png)

1. Select **Generate script** from the "Add a single server" section.

   ![](../Media/ch-3.png)

1. In the **Add a server with Azure Arc** page, select the **Default Subscription (1)**, select the **RG-Defender (2)** Resource group under Project details.
1. For *Region*, select **(US) East Us (3)** from the drop-down list.

    ![](../Media/ch-3.1.png)

1. Review the Server details and Connectivity method options. Keep the default values and select **Next** to get to the Tags tab.
1. Review the default available tags. Select **Next** to get to the Download and run script tab.

   ![](../Media/ch-3.2.png)

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it.

   ![](../Media/ch-3.3.png)

1. In Microsoft Edge Browser, select the ellipsis button (...) if needed and then select **Keep**.

   ![](../Media/l8e121.png)
    
1. Right-click the Windows Start **(1)** button and select **Windows PowerShell (Admin) (2)**.

   ![](../Media/l8e1-11.png)

1. Enter *Administrator* for "Username" and *Passw0rd!* for "Password" if you get a UAC prompt.

1. Run the below command to navigate to Downloads:

    ```
    cd C:\Users\Administrator\Downloads
    ```

1. Run the below command:
   
   ```
   Set-ExecutionPolicy -ExecutionPolicy Unrestricted
   ```

1. Enter **A** for Yes to All and press enter.

    ![](../Media/l8e123.png)

1. Run the below command to run the file:

    ```
    .\OnboardingScript.ps1
    ```

1. Enter **R** to Run once and press enter (this may take a couple minutes).

    ![](../Media/l8e125.png)

1. The setup process opens a new Microsoft Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message **"Authentication complete"** and then go back to the Windows PowerShell window.

    ![](../Media/ch-3.4.png)

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Machines** page.

    ![](../Media/l8e127.png)

1. Select **Refresh** until WINServer server name appears and the Status is *Connected*.
  
    ![](../Media/ee25.png)

    >**Note:** This could take a couple of minutes.

## Task 4: Connect an Azure Windows virtual machine

In this task, you will connect an Azure Windows virtual machine to Microsoft Sentinel.

1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/ee6.png)

1. Select your Microsoft Sentinel Workspace you created earlier.

   ![](../Media/l8e130.png)

1. In the Microsoft Sentinel left menus, scroll down to the **Content management** section and select **Content Hub (1)**.

1. In the **Content hub**, search for the **Windows Security Events (2)** solution and select **Windows Security Events (3)** from the list.

1. On the **Windows Security Events** solution page select **Install (4)**.

   ![](../Media/ch-3.6.png)

1. When the installation completes select **Manage**.

   ![](../Media/l8e3-15.png)

    >**Note:** The *Windows Security Events* solution installs both the *Windows Security Events via AMA* and the *Security Events via Legacy Agent* Data connectors, along with 2 Workbooks, 20 Analytic Rules, and 43 Hunting Queries.

1. Select the **Windows Security Events via AMA (1)** Data connector, and select **Open connector page (2)** on the connector information blade.

   ![](../Media/l8e3-14.png)
    
1. In the **Configuration section**, select the **Create data collection rule (1)**.
1. Enter **AZWINDCR (2)** for Rule Name, then select **Next: Resources (3)**.

   ![](../Media/ch-3.7.png)

1. Expand **RG-AZWIN01**, then select **AZWIN01**, and click on **Next: Collect**.

   ![](../Media/ch-3.8.png)


1. Review the different Security Event collection option. Keep *All Security Events* and then select **Next: Review + create**.

     ![](../Media/ch-3.9.png)

1. Select **Create** to save the Data Collection Rule.

    ![](../Media/ch-4.0.png)

1. Wait a minute and then select **Refresh** to see the new data collection rule listed.

## Task 5: Connect a non-Azure Windows Machine

In this task, you will add an Azure Arc connected, non-Azure Windows virtual machine to Microsoft Sentinel.  

   >**Note:** The *Windows Security Events via AMA* data connector requires Azure Arc for non-Azure devices.

1. Make sure you are in the **Windows Security Events via AMA** data connector configuration in your Microsoft Sentinel workspace.

1. Under the **Configuration** section, edit the **AZWINDCR** *data collection rule* by selecting the *pencil* icon.

   ![](../Media/l8e3-12.png)
    
1. Select **Next: Resources**, and expand your **Subscription** under **Scope** on the **Resources** tab.

1. Expand **RG-Defender** (or the Resource Group your created), then select both the **WIN-xxxxxxxxxx (1)**, click on **Next: Collect> (2)**.

    ![](../Media/ee9.png)

1. On the **Edit Data Collection Rule** page, then **Next: Review + create**.

   ![](../Media/l8e3-10.png)

1. Once the validation has passed, click on **Create**.

    ![](../Media/ch-4.2.png)

## Summary

In this lab, you have completed the following:

- Created a Windows Virtual Machine in Azure
- Installed Azure Arc on an On-Premises Server
- Connected an Azure Windows virtual machine
- Connected a non-Azure Windows Machine

### You have successfully completed the lab. Click on Next >> to procced with next Lab.
![](../Media/ch-5.9.2.png) 

