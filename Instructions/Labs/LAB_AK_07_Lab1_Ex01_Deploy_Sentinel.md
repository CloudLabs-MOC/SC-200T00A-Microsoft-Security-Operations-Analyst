# Lab 07 - Exercise 1: Configure your Microsoft Sentinel environment

## Lab Scenario

You're a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You're responsible for setting up the Microsoft Sentinel environment to meet the company requirements to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.

>**Important:** The lab exercises for Learning Path #7 are in a **standalone** environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will perform the following:

- Task 1: Create a Log Analytics Workspace
- Task 2: Deploy Microsoft Sentinel to a workspace
- Task 3: Configure data retention
- Task 4: Create a Watchlist
- Task 5: Create a Threat Indicator
- Task 6: Configure log retention

## Estimated Timing: 60 Minutes

## Architecture Diagram

  ![Picture 1](../Media/SC200-Lab_Diagrams_Mod5_L1_Ex1.png)

### Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Log Analytics (1)**, then select **Log Analytics workspaces (2)**.

   ![](../Media/lab6-s1.png)

1. Select **+ Create** from the command bar.

   ![](../Media/lab6-s2.png)

1. To create a **log analytics workspace**, follow these steps:

     - Subscription **Accept default subscription (1)**
    - Select **rg-defender (2)**, for Resource group.
    - For the Name, enter **uniquenameDefender (3)**.
    - Leave the **default Region (4)**.
    - Select **Review + Create (5)**.

      ![Picture 1](../Media/lab7-s1.png)

1. Once the workspace validation has passed, select **Create**.

   ![](../Media/lab7-s2.png)

1. Wait for the new workspace to be provisioned, this may take a few minutes.

### Task 2 : Deploy Microsoft Sentinel to a workspace

In this task, you will deploy Microsoft Sentinel to an existing Log Analytics workspace, enabling it to collect, detect, and respond to security threats.

1. In the Search bar of the Azure portal, type **microsoft sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/lab6-s5.png)

1. Select **+ Create** from the command bar.

   ![](../Media/lab6-s6.png)

1. Select the newly created **uniquenameDefender (1)** workspace and click on **Add (2)**.
  
   ![](../Media/lab6-s7.png)

1. In the Microsoft Sentinel free trial activated tab, select **Ok**.

   ![](../Media/lab6-s8.png)

### Task 3 : Configure data retention

In this task, you will configure the data retention in the Log analytics workspace.

1. In the Search bar of the Azure portal, type **Log Analytics (1)**, then select **Log Analytics workspaces (2)**. 

   ![](../Media/lab6-s1.png)

1. Select **uniquenameDefender** Log Analytics workspaces. 

   ![](../Media/lab7-s3.png)

1. Expand the **Settings** section in the navigation menu and select **Usage and estimated costs (1)** then Select **Data retention (2)**.

   ![](../Media/lab7-s4.png)

1. Change data retention period to **180 days (1)** then Select **OK (2)**.

   ![](../Media/lab7-s5.png)

### Task 4: Create a Watchlist

In this task, you will create a watchlist in Microsoft Sentinel.

1. In the search box of your Labvm, enter **Notepad (1)**. Select **Notepad (2)** from the results.

   ![](../Media/lab7-s6.png)

1. Type **Hostname** then enter for a new line.

1. From row 2 of the notepad, copy the following hostnames, each one in a different line:

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

    ![](../Media/lab7-s7.png)

1. From the menu select, **File (1) - Save As (2)**.

   ![](../Media/lab7-s8.png)

1. Name the file **HighValue.csv (1)**, change the file type to **All files (2)** and select **Save (3)**. 

   ![](../Media/lab7-s9.png)

   >**Hint:** The file can be saved in the **Documents** folder.

1. **Close** the Notepad.

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. In the left pane, expand **Microsoft Sentinel (1)** → **Configuration (2)** → select **Watchlist (3)**.

    ![](../Media/lab7-s10.png)

1. In the **Microsoft Defender portal**, on the **Workspaces** page, select **Connect workspace**.

    ![](../Media/lab7-s11.png)

    > **Note:** After opening the **Microsoft Defender portal**, it may take **5–10 minutes** for the **Microsoft Sentinel workspace** to appear in the **Workspaces** list. If no workspace is displayed initially, try refreshing the page using **Ctrl + F5**, signing out by selecting the circle with your initials in the top-right corner and choosing **Sign out**, and then signing back in using your **Tenant Email** credentials. You can also try opening the portal in **InPrivate/Incognito mode**. If the workspace is **already connected**, please **proceed to the next step**. 

    >**Note:** If the option is still not visible after trying these steps, it may be an issue with the Defender portal. In that case, please contact Cloudlabs-Support@spektrasystems.com for assistance.

    > **Important:** The total lab duration already includes any waiting time required for deployments, data connectors, or services (such as the **5–10 minutes** mentioned above). Please do not worry if certain steps take additional time to complete, and plan your activities accordingly while performing the lab.

1. On the **Choose a workspace** page, select the workspace **uniquenameDefender (1)**, and then click **Next (2)**.

    ![](../Media/lab7-s12.png)

1. On the **Set a primary workspace** page, verify **uniquenameDefender (1)** is selected, and then click **Next (2)**.

    ![](../Media/lab7-s13.png)

1. On the **Review and finish** page, select **Connect**.

    ![](../Media/lab7-s14.png)

1. In the **You're about to connect a workspace** confirmation dialog, select **Connect**.

    ![](../Media/lab7-s15.png)

1. On the **Workspace successfully connected** page, select **Close**.

1. In Microsoft Sentinel, On the left menu, select the **Watchlist (1)** option under the **Configuration** area then Select **+ New (2)** from the command bar.

   ![](../Media/lab7-s17.png)

   > **Note:** If the **Watchlist** page does not load, refresh the browser until it appears.  

1. In the Watchlist wizard, enter the following then Select **Next: Source > (4)**:

    |General setting|Value|
    |---|---|
    |Name|**HighValueHosts (1)**|
    |Description|**High Value Hosts (2)**|
    |Alias|**HighValueHosts (3)**|

    ![](../Media/lab7-s18.png)

1. Select **Browse for files** under **Upload file** and browse for the **HighValue.csv (1)** file you just created.

    ![](../Media/lab7-s19.png)

1. In the **SearchKey field** select **Hostname (2)**.

1. Select **Next: Review + Create >**.

    ![](../Media/lab7-s20.png)

    ![](../Media/lab7-s21.png)

1. Review the settings you entered and select **Create**.

    ![](../Media/lab7-s22.png)

1. The screen returns to the Watchlist page.

1. Select the **HighValueHosts (1)** watchlist and on the right pane, select **View in logs (2)**.

     ![](../Media/lab7-s23.png)

     ![](../Media/lab7-s24.png)

      >**Important:** It could take up to ten minutes for the watchlist to appear. **Please continue with the following task and run this command in the next lab**.
     
      >**Note:** You can now use the `_GetWatchlist('HighValueHosts')` in your own KQL statements to access the list. The column to reference would be **Hostname**.

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Hit the Validate button for the corresponding task. You can proceed to the next task if you receive a success message.
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

  <validation step="53b31791-6d4b-4f83-a56e-b7136bbba6a7" />
  
### Task 5: Create a Threat Indicator

In this task, you will create an indicator in Microsoft Sentinel.

1. In the **Microsoft Sentinel** portal, in the left navigation pane, expand **Threat management (1)**, select **Threat intelligence (2)**, and then click **Open intel management (3)**.

     ![](../Media/lab7-s24.1.png)

2. In the **Microsoft Defender** portal, on the **Intel management** page, select **+ New (1)**, and then click **TI object (2)**.

     ![](../Media/lab7-s24.2.png)

4. From the **Object type** dropdown, select **Indicator (1)**.

5. Select the **+ New observable** dropdown and select **Domain name (2)**.

     ![](../Media/lab7-s25.png)

6. For Domain, enter a domain name, for example, type **contoso.com (3)**.

7. In the **Name** field, enter the same value (4) used for the Domain.

8. In the **Indicator types**, select **malicious-activity (5)**.

9. Set the **Valid from (6)** field to today's date.

     ![](../Media/lab7-s26.png)

10. Scroll down to the **Description** and enter **This domain is known to be malicious (7)**.

11. Select **Add (8)**.

12. Navigate to **Microsoft Sentinel** in azure portal, open the **uniquenamedefender (1)** workspace, expand the **General** section and select **Logs (2)** from the navigation menu and close the Log Analytics video pop-up window that appears **(3)**.

      ![](../Media/lab6-s14.png)

1. Close the **Queries hub**.

     ![](../Media/lab6-s15.png)

1. From the mode dropdown, switch from **Simple mode (1)** to **KQL mode (2)**.

     ![](../Media/lab6-s16.png)

1. Run the following KQL statement.

     ```KQL
     ThreatIntelIndicators
     ```  

     ![](../Media/output.png)

     > **Note:** It could take up to 5 minutes for the indicator to appear.

1. Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.

     ```KQL
     ThreatIntelIndicators
     | project ObservableValue
     ```

     ![](../Media/lab7-s28.png)

### Task 6: Configure log retention

In this task, you will change the retention period for the SecurityEvent table.

1. In Microsoft Sentinel, select the **Settings (1)** option under the **Configuration** area then select **Workspace settings (2)**.

     ![](../Media/lab7-s29.png)

1. In Log Analytics workspace, select the **Tables (1)** option under the **Settings** area.

1. Search and select the table **SecurityEvent (2)**, and then right click on **Security Event (3)** table.

     ![](../Media/lab7-s30.png)

1. Select **Manage Table (4)**.

1. Change the **Analytics retention** to **90 days (1)**.

1. Reset the **Total retention** to **180 days (2)** (if needed). Notice that **Long term retention** is set now set to **90 days**, because **Azure Monitor** automatically treats the remaining 90 days of total retention as low-cost, long-term retention.

1. Select **Save (3)** to apply the changes.

     ![](../Media/lab7-s27.png)

## Review
In this lab, you have completed the following:

- Created a Log Analytics Workspace
- Deployed Microsoft Sentinel to a workspace
- Configured data retention
- Created a Watchlist
- Created a Threat Indicator
- Configured log retention

## You have successfully completed the lab
