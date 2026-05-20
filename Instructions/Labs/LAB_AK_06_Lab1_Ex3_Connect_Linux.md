# Lab 05: Connect Linux hosts to Microsoft Sentinel using data connectors

### Estimated Duration: 60 Minutes

## Overview

In this lab, you will learn how to connect Linux hosts to Microsoft Sentinel using the Common Event Format (CEF) and Syslog connectors. You will also configure the facilities for the Syslog connector.

>**Important:** There are steps within the next Tasks that are done in different virtual machines. Look for the Virtual Machine name references.

## Objectives

In this lab, you will perform the following tasks: 

- Task 1: Connect a Linux Host using the Common Event Format connector
- Task 2: Connect a Linux host using the Syslog connector
- Task 3: Configure Syslog facilities and severities using Data Collection Rules

## Architecture Diagram

  ![](../Media/SC200-Lab_Diagrams_Mod6_L1_Ex3-1.png)

### Task 1: Connect a Linux Host using the Common Event Format connector

In this task, you will connect a Linux host to Microsoft Sentinel with the Common Event Format (CEF) connector.

   > **Note:** Ensure you are logged into Azure from the SmartHotelHost VM (Lab VM).

   > **Note:** While accessing Sentinel workspace if you see an error that the page was moved to Defender portal, click on the link on the top left side of the page to access the old experience and refresh your browser page. 

   ![](../Media/sentinel-error-1401.png) 

1. Close the **Windows Security Events via AMA** connector page if it is still open.

1. In the **Sentinel** workspace, under **Content hub**, Search for **Common Event Format (1)** and select it.

1. Select the **Common Event Format (2)** and click on **Install (3)**.

   ![](../Media/L5T1S3-1301.png)

1. Once the **Common Event Format** is installed, click on **Manage**.

1. Select **Common Event Format (CEF) via AMA (1)** connector from the list, and click on **Open connector page (2)**.

   ![](../Media/L5T1S5-1301.png)

1. Under configuration, copy the command shown in **Run the following command to install and apply the CEF collector** and paste it in a Notepad.

   ![](../Media/upd-2.png)

1. In the Search bar, type **Virtual machines (1)** and select **Virtual machines (2)**.

   ![](../Media/ee3.png)

1. Click on **LIN1** Linux virtual machine.

   ![](../Media/L5T1S10-2810.png)  

1. Click on **Connect (1)** from the left navigation pane, scroll down to the Native SSH ,copy the **SSH command (2)** and paste it into the notepad.
   
   ![](../Media/ee10.png)  

1. Go back to the WIN1 virtual machine.

1. Right-click the Windows Start **(1)** button and select **Windows PowerShell (Admin) (2)**.

   ![](../Media/l8e1-11.png)

1. Paste the command which we copied from the Native SSH window in step 9.

1. Enter **yes** to confirm the connection and then type the user's **password provided under Resource group: LIN1** in the Environment tab of Lab Guide and press **enter**. Your screen should look something like this:

   ![linux login](../Media/ch-4.5.png)

   > **Note**: When a command prompts for a password, the characters are hidden for security. You can simply type your password and press Enter, even though nothing appears on the screen.

1. Paste command to **Install the CEF collector on the Linux machine** you have copied in step 6. 

   ![ConnectorScript](../Media/ConnectorScriptupdated.png)

1. The script will run against your Linux server remotely. When the script processes properly it should look like this screen:

   ![ConnectorScript](../Media/LinuxConnectedupd.png)
   
1. Close the Powershell Window.

### Task 2: Connect a Linux host using the Syslog connector

   > **Note:** Perform this task from the SmartHotelHost VM (Lab VM).

In this task, you will connect a Linux host to Microsoft Sentinel with the Syslog connector.

1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/ee6.png) 

1. Click on the **workspace-<inject key="DeploymentID" enableCopy="false" />** that we created earlier.

   > **Note:** If you see an error that the page was moved to Defender portal, click on the link on the left top side to access the old experience and refresh the browser page. 

      ![](../Media/sentinel-error-1401.png) 

1. Select **Content Hub (1)** under Content management from the left pane.

1. Search for **Syslog (2)** and select **(3)** it. Once selected, click on **Install (4)**.

   ![](../Media/L5T2S4-1301.png)  

1. Once the **Syslog** connector is installed, click on **Manage**.

1. Select the **Syslog via AMA (1)** from the list and click on **Open connector page (2)**.

   ![](../Media/L5T2S6.1-1301.png)  

1. Under **Configuration**, click on **+ Create data collection rule**.

   ![](../Media/L5T2S7-1301.png)  

1. On the Create Data Collection Rule page, for the **Name**, enter **WINDCR2 (1)** and click on **Next: Resources (2)**.

   ![](../Media/L5T2S8-1301.png)

1. On the **Resources** page, select the Lin-2 VM under the Lin-2 resource group, and click on **Next: Collect (2)**.

   ![](../Media/L5T2S9-1301.png)

1. On the **Collect** page, keep everything as default and click on **Next: Review + create**.

1. On the **Review + create** page, review the settings and click on **Create**.

   ![](../Media/L5T2S10-1301.png)

1. Once the Data Collection Rule is created, you will be redirected back to the Syslog connector page.

    ![](../Media/L5T2S11-1301.png)  

### Task 3: Configure Syslog facilities and severities using Data Collection Rules

   > **Note:** Perform this task from the SmartHotelHost VM (Lab VM).

In this task, you will update the **Data Collection Rule (DCR)** created in the previous task to specify the **Syslog facilities** and severity levels to be collected from Linux machines and sent to Microsoft Sentinel.

1. On the search bar, search for **Data collection rule (1)** and select it **(2)**.

   ![](../Media/L5T3S1-1301.png)


1. Select the **WINDCR2** data collection rule from the list.

    ![](../Media/L5T3S2.1-1301.png)  

1. Under **Configurations**, click on **Data sources (1)**, and select the **Linux Syslog (2)** data source.

   ![](../Media/L5T3S3-1301.png)

1. In the Add data source page, select the following **(1)** facilities and click on **Save (2)**:
   - LOG_AUTH
   - LOG_AUTHPRIV

       ![](../Media/L5T3S4-1301.png)

   >**Note:** You can also select Minimum log level for both facilities.

## Summary 

In this lab, you learned how to connect Linux hosts to Microsoft Sentinel using the Common Event Format (CEF) and Syslog connectors. You also configured the facilities for the Syslog connector.

### You have successfully completed this lab!

By completing this lab **Secure Windows Servers with Azure Arc & Microsoft Defender**, you gained hands-on experience in strengthening hybrid cloud environments using Microsoft security and monitoring tools. You began by onboarding on-premises Windows Servers to Azure Arc, enabling centralized governance and management across hybrid infrastructures. You then configured Microsoft Defender for Cloud to monitor workloads, assess compliance, and mitigate threats through actionable security alerts. Moving further, you connected Windows and Linux machines to Microsoft Sentinel using data connectors such as CEF and Syslog, integrating diverse log sources for advanced threat detection and response. Through this process, you built a unified security architecture that leverages AI-driven intelligence, automated incident handling, and comprehensive visibility to safeguard both on-premises and cloud resources.
