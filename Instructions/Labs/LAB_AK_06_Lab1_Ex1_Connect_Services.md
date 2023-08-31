# Module 6 - Lab 1 - Exercise 1 - Connect data to Microsoft Sentinel using data connectors

## Lab scenario


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The organization has data from Microsoft 365, Microsoft 365 Defender, Azure resources, non-azure virtual machines, and network appliances.

You plan on using the Microsoft Sentinel data connectors to integrate the log data from various sources. You need to write a connector plan for management that maps each of the organization's data sources to the proper Microsoft Sentinel data connector.

## Lab objective

After completing this lab, you will be able to integrate log data from various data sources within the organization into Microsoft Sentinel using appropriate data connectors.

## Estimated time: 30 minutes

## Architecture Diagram

  ![Picture 1](../Media/SC200-Lab_Diagrams_Mod6_L1_Ex1.png)

### Task 1: Access the Microsoft Sentinel Workspace

 In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud and you will access your Microsoft Sentinel workspace.  

 1. Open the Microsoft Edge browser.

 1. In the Edge browser, navigate to the Azure portal at https://portal.azure.com.

 1. In the **Sign in** dialog box, copy and paste * Email/Username: <inject key="AzureAdUserEmail"></inject> and then select Next.

 1. In the **Enter password** dialog box, copy and paste * Password: <inject key="AzureAdUserPassword"></inject> and then select **Sign in**.

 1. On the **Stay signed in?** dialog box, select the Don’t show this again check box and then select **No**.

 1. In the Search bar of the Azure portal, type **Log Analytics**, then select **Log Analytics workspaces**.

 1. Select **+Create** from the command bar.

 1. Select Resouce Group **RG-Defender**  from the drop down.

 1. For the Name, enter **uniquenameDefender** 

 1. Select **Review + Create**.

 1. Once the workspace validation has passed, select **Create**. Wait for the new workspace to be provisioned, this may take a few minutes
 
 1. In the Search bar of the Azure portal, type **Sentinel**, then select **Microsoft Sentinel**.

 1. select the newly created workspace and click on **Add**


### Task 2: Connect the Azure Active Directory connector

 In this task, you will connect the Azure Active Directory connector to Microsoft Sentinel.

 1. On the left side menu, In the Configuration area select **Data connectors**.
 
 1. In the Data Connectors page, click on content hub and search for **Azure Active Directory** and select and install it
   
 1. Go back to data connector page and search for the **Azure Active Directory** connector and select it from the list.

 1. Select the **Open connector page** on the connector information blade.

 1. Check and click on the **Sign-in Logs** and **Audit Logs** options from the Configuration area, then select **Apply Changes**.

### Task 3: Connect the Azure Active Directory Identity Protection connector

 In this task, you will connect the Azure Active Directory Identity Protection connector to Microsoft Sentinel.

 1. In the Data Connectors page, click on content hub and search for **Azure Active Directory Identity Protection** and select and install it
 
 1. From the Data Connectors Tab, search for the **Azure Active Directory Identity Protection** connector and select it from the list.

 1. Select the **Open connector page** on the connector information blade.

 1. From the **Configuration** area select the **Connect** button.


### Task 4: Connect the Microsoft Defender for Cloud connector

 In this task, you will connect the Microsoft Defender for Cloud connector.
 
 1. In the Data Connectors page, click on content hub and search for **Microsoft Defender for Cloud** and select and install it
 
 1. From the Data Connectors tab, search for the **Microsoft Defender for Cloud** connector and select it from the list.

 1. Select the **Open connector page** on the connector information blade.

 1. In the **Configuration** area, under Subscription, select the checkbox for the available subscription and slide the **Status** option to the right to indicate **Connected**.

1. The **Status** should be now **Connected** and **"Bi-directional sync"** should be **Enabled**.

1. Scroll down and under the **"Create incidents - Recommended!"** area, select **Enable**. This option creates an Analytics rule automatically for this service. You can manually add it later if not enabled here or change its configuration within the **Analytics** blade.


### Task 5: Connect the Microsoft Defender for Cloud Apps connector

In this task, you will connect the Microsoft Defender for Cloud Apps connector.

1. From the Data Connectors Tab, search for the **Microsoft 365 Defender** connector and select it from the list.

1. Select the **Open connector page** on the connector information blade.

1. From the Configuration area select **Connect Incident and Alerts**. 

1. Under **Connect Events**, select the **Name** checkbox to select all the checkboxes for **Microsoft Defender for Endpoint**.

1. Repeat the same for **Microsoft Defender for Office 365**

1. Scroll to the bottom of the page and select **Apply Changes**.

   >**Note:** If you see **No Permission** under **Connect incidents & alerts** that means **License** and Permissions is not reflected on the Odl_user. it will take 1-2 hours to reflect the license on the odl user, meanwhile you can perform the next task, exercise 2 and exercise 3. After 1-2 hrs come back and refresh the page to re-perform the task 5 again.

### Task 6: Connect the Azure Activity connector

In this task, you will connect the Azure Activity connector.
1. In the Data Connectors page, click on content hub and search for **Azure Activity** and select and install it

1. From the Data Connectors Tab, search for the **Azure Activity** connector and select it from the list.

1. Select the **Open connector page** on the connector information blade.

1. In the Configuration area, scroll down and under "2. Connect your subscriptions..." select **Launch Azure Policy Assignment Wizard>**.

1. In the **Basics** tab, select the button with the three dots under **Scope** to select your subscription from the drop-down list and click **Select**.

1. Select the **Parameters** tab, choose your Microsoft Sentinel workspace from the **Primary Log Analytics workspace** drop-down list.

1. Select the **Remediation** tab and mark the **Create a remediation task** checkbox.

1. Select the **Review + Create** button to review the configuration.

1. Select **Create** to finish.

### Review
In this lab, you have integrated log data from various data sources within the organization into Microsoft Sentinel using appropriate data connectors

## Proceed to Exercise 2
