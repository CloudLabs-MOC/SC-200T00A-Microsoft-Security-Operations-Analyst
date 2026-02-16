# Lab 08 - Exercise 3: Connect Linux hosts to Microsoft Sentinel using data connectors

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data is Linux virtual machines using the Common Event Format (CEF) via Legacy Agent and Syslog connectors.

## Lab Objectives
 In this lab, you will perform the following: 
- Task 1: Access the Microsoft Sentinel Workspace
- Task 2: Connect a Linux Host using the Common Event Format connector
- Task 3: Connect a Linux host using the Syslog connector

## Estimated Timing: 60 Minutes

## Architecture Diagram

  ![](../Media/SC200-Lab_Diagrams_Mod6_L1_Ex3.png)

### Task 1: Access the Microsoft Sentinel Workspace

In this task, you will access your Microsoft Sentinel workspace.

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. In the Microsoft Defender **Microsoft Sentinel (1)** navigation menu, scroll down to the **Content management (2)** section and select **Content Hub (3)**.

     ![](../Media/lab8-s1.png)

### Task 2: Connect a Linux Host using the Common Event Format connector

In this task, you will connect a Linux host to Microsoft Sentinel with the Common Event Format (CEF) connector.

1. In **content hub** and search **Common Event Format (2)** and select **Common Event Format (3)** from list and click on **install (4)**.

   ![](../Media/lab8-s45.png)

1. After the solution is installed, select **Manage** to configure the **Common Event Format** solution.

    ![](../Media/lab8-s46.png)

1. From the Data Connectors tab, search for the **Common Event Format (CEF) via AMA (1)** connector and select it from the list.

1. Select the **Open connector page (2)** on the connector information blade.

   ![](../Media/lab8-s47.png)

1. Under configuration, **copy the command** shown to install and apply the CEF connector and paste it into Notepad.

   ![](../Media/lab8-s48.png)

1. Back to the Azure portal, in the Search bar of the Azure portal, type **virtual machine (1)**, then select **Virtual machine (2)**.

   ![](../Media/14-8-25-l4e-3.png)

1. Open **LIN1 (1)** Linux virtual machine and copy the **Public IP address (2)** of LIN1 from the **overview** and paste on the notepad.

   ![](../Media/lab8-s49.png)

   ![](../Media/lab8-s50.png)

1. Go back to the WIN1 virtual machine. Launch Windows PowerShell as Administrator by right-clicking the **Start (1)** menu icon and selecting **Windows PowerShell (Admin) (2)**. Select **Yes** to allow the app to run in the User Account Control window that appears.

   ![](../Media/lab8-s30.1.png)

1. Enter the following PowerShell command, adjusting for your specific Linux server information, and press Enter:

    ```PowerShell
    ssh insert your linux-IP-address-here -l insert-linux-user-name-here
    ```
    
     >**Note:** Replace **insert your linux IP address here** with pasted on the notepad Public Ip address of **LIN1** and **insert linux username here** with **Admin Username:** **cloudlabs** provided under Resource group: **LIN1** in the **Environment Details** page of the lab guide.

1. Enter **yes** to confirm the connection and then type the user's **password provided under Resource group: LIN1** in the Environment tab and press **enter**. Your screen should look something like this:

   ![](../Media/lab8-s51.png)

   - **password/LIN1: <inject key="Admin Password"></inject>**

1. You are now ready to paste in the command that we copied from the earlier step. Make sure that the script from Azure is in the clipboard. In PowerShell, right-click the top bar and choose **Edit** and then **Paste**. Once pasted add a **3** to the word *python* as shown below:

   ![](../Media/lab8-s52.1.png)
   
    >**Note:** You can also copy from the notepad you have pasted earlier.

1. Once the script is pasted in and adjusted, press Enter. The script will run against your Linux server remotely. When the script processes properly, it should look like this screen:

   ![](../Media/lab8-s52.png)

1. Navigate to **Microsoft Defender** portal, in the Microsoft Sentinel left navigation menu, scroll down to the **Content management** section and select **Content Hub (1)**.

1. In the **Content hub**, search for the **Common Event Format (2)** solution and select **Common Event Format (3)** from the list.

    ![](../Media/lab8-s53.png)

1. On the **Common Event Format** solution page select **Manage**.

    >**Note:** The **Common Event Format** solution installs both the **Common Events Format (CEF) via AMA** and the **Common Events Format (CEF) via Legacy Agent** Data connectors.

   ![](../Media/lab8-s54.png)

1. Select the **Back** arrow to view the content items and access the connector page.

1. Select the **Common Events Format (CEF) via AMA (1)** Data connector, and select **Open connector page (2)** on the connector information blade.

   ![](../Media/lab8-s55.png)

1. In the **Configuration** section, select the **+ Create data collection rule** button.

1. On the **Create data collection rule** page, *Basic* tab, enter **AZLINDCR (1)** for Rule Name, then select **Next: Resources (2)**.

   ![](../Media/lab8-s56.png)

1. On the **Resources** tab, expand your **MOC Subscription (1)** under **Scope**.

1. Expand **LIN1 (2)** resource group, then select **LIN1 (3)**.

   ![](../Media/lab8-s57.png)

    >**Note:** You're **LIN1** virtual machine may appear with a different name, like ubuntuxxx.

1. Select **Next: Collect**. In the **Collect** tab, select the  **LOG_ALERT** drop-down menu, and select **LOG_WARNING (1)**.

   ![](../Media/lab8-s58.png)

1. Select **Next: Review + create (2)**, and select **Create**. Wait for the deployment to finish.

   ![](../Media/lab8-s59.png)

    >**Note:** You may need to refresh the page.

1. The **Common Event Format (CEF) via AMA** Data connector should now show **Connected**.

   ![](../Media/lab8-s60.png)

1. The data collection rule installs the Azure Monitor Agent (AMA), and the **CEF collector** install commands were pre-deployed on the LIN1 machine to install the CEF collector.

1. Return to the **PowerShell Command Prompt** window. You should still be connected to the LIN1 virtual machine.

1. At the Linux prompt, type the following command, and press Enter:

    ```cmd
    netstat -lnptv
    ```

1. You should see the rsyslog (or syslog-ng) daemon listening on port 514.

1. Type **exit** to close the remote shell connection to LIN1.

### Task 3: Connect a Linux host using the Syslog connector

In this task, you will connect a Linux host to Microsoft Sentinel with the Syslog connector.

1. Go back to the Microsoft Defender portak. 

1. Go to the **Content hub (1)** in the data connector window, search for **Syslog (2)**, select **Syslog (3)** from the list and click on **Install**.

   ![](../Media/lab8-s61.png)

   ![](../Media/lab8-s62.png)

1. Select **Manage** to configure the **Syslog** solution.

    ![](../Media/lab8-s63.png)

1. From the **Data Connectors tab**, search for the **Syslog via AMA (1)** connector and select it from the list.

1. Select the **Open connector page (2)** on the connector information blade.

   ![](../Media/lab8-s64.png)

1. Under **Configuration**, select **+Create data collection rule**.

    ![](../Media/lab8-s65.png)

1. On the Create data collection rule page, Basic tab, enter **AZLINDCR2 (1)** for Rule Name, then select **Next: Resources (2)**.

    ![](../Media/lab8-s66.png)

1. On the **Resources** tab, expand your **MOC Subscription** under *Scope*.

    >**Hint:** You can expand the whole *Scope* hierarchy by selecting the ">" before the *Scope* column.

1. Expand **defender-RG (1)**, then select **LIN2 (2)**.

   ![](../Media/lab8-s67.png)

    >**Note:** You're *LIN2* virtual machine may appear with a different name, like ubuntuxxx.

1. Select **Next: Collect (3)**. In the *Collect* tab, select the  *LOG_ALERT* drop-down menu, and select **LOG_WARNING (1)**.

1. Select **Next: Review + create (2)**, and select **Create**. Wait for the deployment to finish.

    ![](../Media/lab8-s68.png)

1. Next, in the **Configuration** section, **copy** the script to install the AMA Forwarder by using the "Copy to clipboard" icon.

    ![](../Media/lab8-s69.png)

1. Go to the LIN2 Linux virtual machine in the Azure portal and copy the Public IP address of **LIN2** and paste it into a notepad.

    ![](../Media/lab8-s70.png)

1. Go back to the LabVM virtual machine, and launch a NEW Windows PowerShell as Administrator by right-clicking the **Start (1)** menu icon and selecting **Windows PowerShell (Admin) (2)**. Select **Yes** to allow the app to run in the User Account Control window that appears.
   
   ![](../Media/lab8-s30.1.png)
   
   >**Note:** You can reuse the Windows PowerShell window if the **Installation completed** for the last task by entering **exit** to close the connection to LIN1.

1. Enter the following PowerShell command, adjusting for your specific Linux server information, and press Enter:

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

    >**Note**: Replace **insert your linux IP address here** with pasted on the notepad Public Ip address of **LIN2** and **insert linux username here** with **Admin Username:** **cloudlabs** provided under Resource group: **LIN2** in the Environment tab
   
1. Enter **yes** to confirm the connection and then type the user's **password provided under Resource group: LIN2** in the Environment tab and press Enter. Your screen should look something like this:

   ![linux login](../Media/lab8-s86.png)

   - **password/LIN2: <inject key="Admin Password"></inject>**

1. At the linux prompt, paste the AMA Forwarder installation script you copied in the previous step.

    ![](../Media/lab8-s71.png)

    >**Note:** You can also copy from the notepad you have pasted earlier.

1. You will need to edit the script for the correct *Python* version installed on your LIN2 machine.

1. Change the script section that contains the *python Forwarder_AMA_installer.py* commands to *python3 Forwarder_AMA_installer.py*.

1. Press **Enter** to run the script

1. You should see the *Installation completed successfully* message.

1. At the linux prompt, type the following command, and press enter:

    ```cmd
    netstat -lnptv
    ```

1. You should see the rsyslog (or syslog-ng) daemon listening on port 514.

    >**Note:** You can query the *Syslog* table for Syslog events.

1. Type **exit** to close the remote shell connection to LIN1.

## Review 
In this lab, you have completed the following:

- Accessed the Microsoft Sentinel Workspace
- Connected a Linux Host using the Common Event Format connector
- Connected a Linux host using the Syslog connector

