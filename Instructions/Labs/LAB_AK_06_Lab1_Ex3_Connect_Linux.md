# Lab 05: Connect Linux hosts to Microsoft Sentinel using data connectors

### Estimated Duration: 40 Minutes

## Lab scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data is Linux virtual machines using the Common Event Formatting (CEF) via Legacy Agent and Syslog connectors.

>**Important:** There are steps within the next Tasks that are done in different virtual machines. Look for the Virtual Machine name references.

## Lab objectives
In this lab, you will perform the following: 
- Task 1: Connect a Linux Host using the Common Event Format connector
- Task 2: Connect a Linux host using the Syslog connector
- Task 3: Configure the facilities you want to collect and their severities for the Syslog connector

## Architecture Diagram

  ![](../Media/SC200-Lab_Diagrams_Mod6_L1_Ex3-1.png)

## Task 1: Connect a Linux Host using the Common Event Format connector

In this task, you will connect a Linux host to Microsoft Sentinel with the Common Event Format (CEF) connector.

   > **Note:** Ensure you are logged into Azure from the SmartHotelHost VM (Lab VM).

1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/ee6.png)

1. Click on the **uniquenameDefender (1)** workspace that we created earlier. Select **Content Hub (2)** under Content management from the left pane.
1. Search for **Common Event Format (3)** and select it.
1. Click on **Install (4)**.

   ![](../Media/ch-4.4.png)

1. Once the **Common Event Format** is installed. Click on **Data connectors (1)** present under Configuration in the left pane.
1. From the Data Connectors tab, select **Common Event Format (CEF) via AMA (2)** connector from the list.
1. Select the **Open connector page (3)** on the connector information blade.

   ![](../Media/upd-1.png)

1. Under configuration, copy the command shown in **Run the following command to install and apply the CEF collector** and paste it in a Notepad.

   ![](../Media/upd-2.png)

1. In the Search bar, type **Virtual machines (1)** and select **Virtual machines (2)**.

   ![](../Media/ee3.png)

1. Click on **LIN1** Linux virtual machine.

   ![](../Media/lab6-4.png)  

1. Click on **Connect (1)** from the left navigation pane, scroll down to the Native SSH ,copy the **SSH command (2)** and paste it into the notepad.
   
   ![](../Media/ee10.png)  

1. Go back to the WIN1 virtual machine.
1. Launch Windows PowerShell as Administrator by right clicking the Start menu icon and selecting **Windows PowerShell (Admin)**.
1. Paste the command which we copied from the Native SSH window
1. Enter **yes** to confirm the connection and then type the user's **password provided under Resource group: LIN1** in the Environment tab and press **enter**. Your screen should look something like this:

   ![linux login](../Media/ch-4.5.png)

1. Paste the **1.2 Install the CEF collector on the Linux machine** from the earlier step. 

   ![ConnectorScript](../Media/ConnectorScriptupdated.png)

1. The script will run against your Linux server remotely. When the script processes properly it should look like this screen:

   ![ConnectorScript](../Media/LinuxConnectedupd.png)
   
1. Close the Powershell Window.

## Task 2: Connect a Linux host using the Syslog connector

   > **Note:** Perform this task from the SmartHotelHost VM (Lab VM).

In this task, you will connect a Linux host to Microsoft Sentinel with the Syslog connector.

1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/ee6.png) 

1. Click on the **uniquenameDefender (1)** workspace that we created earlier.
1. Select **Content Hub (2)** under Content management from the left pane.
1. Search for **Syslog (3)** and select it. Once selected, click on **Install (4)**.

   ![](../Media/ch-4.6.png)  

1. Click on **Data connectors (1)** present under Configuration in the left pane. Select **Syslog via Legacy Agent (2)** connector from the list.

   > **Note:** Refresh if the connector is not visible.

1. Select the **Open connector page (3)** on the connector information blade.

   ![](../Media/ch-4.7.png)  

1. Under **Configuration**, open the **Install agent on a non-Azure Linux Machine (1)** section. Select the link for **Download & install agent for non-Azure Linux machine (2)**. 

   ![](../Media/ch-4.8.png)  

   >**Note:** Your Log Analytics workspace should show **2 0r 3 Windows computers connected**. This corresponds to WIN2 and AZWIN01 virtual machines connected earlier.

1. Select the tab for **Linux servers (1)**.

    >**Note:** Your Log Analytics workspace should show **0 Linux computers connected**. This corresponds to the LIN1 (ubuntu1) virtual machine connected earlier with the CEF connector.

1. Select **Log Analytics agent instructions**. Copy the command in the **Download and onboard agent for Linux (2)** area to the clipboard and paste it into the notepad.

   ![](../Media/ch-4.9.png)  
   
1. Click on **LIN2** Linux virtual machine.

   ![](../Media/ch-5.0.png)  

1. Click on **Connect (1)** from the left navigation pane, scroll down to Native SSH ,copy the **SSH command (2)** and paste it into the notepad.

   ![](../Media/ee11.png)  

1. Navigate back to the **WIN1** virtual machine.

1. Launch a NEW Windows PowerShell as Administrator by right-clicking the Start menu icon and selecting **Windows PowerShell (Admin)**. 

1. Paste the command which we copied from the Native SSH window.
   
1. Enter **yes** to confirm the connection and then type the user's **password provided under Resource group: LIN2** in the Environment tab and press enter. Your screen should look something like this:

   ![linux login](../Media/ch-5.2.png)

1. Paste the **Download and onboard agent for Linux** from the earlier step. 
1. Once the script is pasted in press enter. The script will run against your Linux server remotely. 
1. Close the Powershell Window.

## Task 3: Configure the facilities you want to collect and their severities for the Syslog connector

   > **Note:** Perform this task from the SmartHotelHost VM (Lab VM).

In this task, you will configure the Syslog collection facilities.

1. In the Search bar of the Azure portal, type **Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/ee6.png) 

1. Click on the **uniquenameDefender (1)** workspace. Click on **Settings (2)** and select **Workspace Settings (3)**.

   ![](../Media/ch-5.3.png) 

1. From the left menu, select **Legacy agents management (1)** under the **Classic** area.
1. Click on the **Syslog (2)** tab.
1. Click on the **+ Add facility (3)** button.
1. Select **auth** from the drop-down menu for **Facility name**.

      ![](../Media/ch-5.5.png) 

1. Select the **+ Add facility (1)** button again.
1. Select **authpriv (2)** from the drop-down menu for **Facility name**.
1. Click on **Apply**.

   ![](../Media/azz122.png)    

## Review 
In this lab, you have completed the following:
- Connected a Linux Host using the Common Event Format connector
- Connected a Linux host using the Syslog connector
- Configured the facilities you want to collect and their severities for the Syslog connector

### You have successfully completed this lab!

By completing this lab **Secure Windows Servers with Azure Arc & Microsoft Defender**, you gained hands-on experience in strengthening hybrid cloud environments using Microsoft security and monitoring tools. You began by onboarding on-premises Windows Servers to Azure Arc, enabling centralized governance and management across hybrid infrastructures. You then configured Microsoft Defender for Cloud to monitor workloads, assess compliance, and mitigate threats through actionable security alerts. Moving further, you connected Windows and Linux machines to Microsoft Sentinel using data connectors such as CEF and Syslog, integrating diverse log sources for advanced threat detection and response. Through this process, you built a unified security architecture that leverages AI-driven intelligence, automated incident handling, and comprehensive visibility to safeguard both on-premises and cloud resources.
