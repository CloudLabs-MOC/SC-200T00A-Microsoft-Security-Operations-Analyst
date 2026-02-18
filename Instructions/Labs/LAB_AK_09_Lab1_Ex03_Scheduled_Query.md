# Lab 09 - Exercise 2: Create a Scheduled Query from a template

## Lab Scenario

You're a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. After connecting your data sources to Microsoft Sentinel, you create custom analytics rules to help discover threats and anomalous behaviors in your environment.

Analytics rules search for specific events or sets of events across your environment, alert you when certain event thresholds or conditions are reached, generate incidents for your SOC to triage and investigate, and respond to threats with automated tracking and reMediation processes.

>**Important:** The lab exercises for Learning Path #9 are in a **standalone** environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab objectives
 In this lab, you will perform the following:

- Task 1: Create a Scheduled Query
- Task 2: Edit your new rule
- Task 3: Test your new rule

## Estimated Timing: 40 Minutes

## Architecture Diagram

  ![Picture 1](../Media/archdialab9ex3.png)

### Task 1: Create a Scheduled Query.

In this task, you will create a scheduled query and connect it to the Teams channel you created in the previous exercise.

1. Navigate back to Microsoft Defender portal, **Microsoft Sentinel** navigation menu.

1. In the Microsoft Sentinel left menus, scroll down to the **Content management** section and select **Content Hub**.

1. In the **Content hub**, search for the **Azure Activity (1)** solution, press **Enter** then select it from the list **(2)**. On the Azure Activity solution page ,select **Install (3)**.

   ![Picture 1](../Media/lab9-s38.png)

    > **Note:** If you do not see **Content hub page** in the Microsoft Sentinel portal, try refreshing the browser. Wait 5 minutes and refresh again until it appears.

1. When the installation completes, go to **Data connectors (1)** page under **Configuration** in Microsoft Sentinel. The **Azure Activity** solution installs the **Azure Activity (2)** Data connector, 12 Analytic rules, 14 Hunting queries and 1 Workbook.

   ![Picture 1](../Media/lab9-s39.png)

1. Select the **Azure Activity (1)** Data connector and select **Open connector page (2)**.

   ![Picture 1](../Media/lab9-s40.png)

1. In the **Configuration** area under the **Instructions** tab, scroll down to **2. Connect your subscriptions...**, and select **Launch Azure Policy Assignment Wizard>**.

   ![Picture 1](../Media/lab9-s41.png)

1. In the **Basics** tab, select the ellipsis button **(...) (1)** under **Scope** and select your subscription from the drop-down list **(2)** and click **Select (3)**.

   ![Picture 1](../Media/lab9-s42.png)

1. Select the **Parameters (1)** tab, choose **uniquenameDefender (2)** workspace from the **Primary Log Analytics workspace** drop-down list and then click **Select (3)**. This action will apply the subscription configuration to send the information to the Log Analytics workspace.
    
   ![Picture 1](../Media/ss28.png)

1. Select the **Remediation** tab and select the **Create a remediation task (1)** checkbox. This action will apply the policy to existing Azure resources. Select the **Review + Create (2)** button to review the configuration.

   ![Picture 1](../Media/lab9-s43.png)

1. Select **Create** to finish.

1. Please wait for the Azure Activity data connector to display a Connected status before proceeding to the next task. This process may take approximately **15-30** minutes. **If the status does not update, try refreshing the page**.

   ![Picture 1](../Media/lab9-s44.png)

1. Navigate back to **Analytics (1)** from the **Configuration** area.

   - Make sure that you are in the **Rule templates (2)** tab in the command bar and search for the **New CloudShell User (3)** rule

   - Select **New CloudShell User (4)** ,from the rule summary blade, make sure you're receiving data by reviewing the green icon under **Data sources: Azure Activity (5)**.

     ![Picture 1](../Media/lab9-s45.png)
    
1. Click on the **Elipses (...) (1)** from the right and then select **Create rule (2)** to continue under Rule templates in the Analytics tab.

   ![](../Media/lab9-s46.png)

1. In the Analytics rule wizard, on the **General** tab, change the *Severity* to **Medium (1)** and then select **Next: Set rule logic > (2)** button:

   ![](../Media/lab9-s47.png)

1. For the rule query, select **View query results**. You shouldn't receive any results nor any errors.

   ![](../Media/lab9-s48.png)

1. Close the **Logs** window by selecting the upper right **X** and select **OK** to discard to save changes to go back to the wizard.

1. Scroll down and under **Query scheduling** set the following:

    |Setting|Value|
    |---|---|
    |Run Query every|**5 minutes (1)**|
    |Lookup data from the last|**1 Days (3)**|

    ![](../Media/lab9-s49.png)

    >**Note:** We are purposely generating many incidents for the same data. This enables the lab to use these alerts.

1. Under the **Alert threshold** area, leave the value unchanged since we want the alert to register every event.

1. Under the **Event grouping** area, leave the **Group all events into a single alert** as the selected option since we want to generate a single alert every time it runs, as long as the query returns more results than the specified alert threshold above.

1. Select the **Next: Incident settings > (5)** button.

1. On the **Incident settings** tab, review the default options.

1. Select the **Next: Automated response >** button.

1. On the **Automated response** page, select the **Next: Review and create >** button.

   ![Picture 1](../Media/lab9-s50.png)

1. Then select **Save**.

   ![Picture 1](../Media/lab9-s51.png)

### Task 2: Edit your new rule

In this task, you will modify the New CloudShell User rule in Microsoft Sentinel by configuring automated responses.

1. Select **Analytics** from the Configuration area.

1. Make sure that you are in the **Active rules** tab in the command bar and select the **New CloudShell User** rule.

   > **Note:** If you do not see **Analytics page** in the Microsoft Sentinel portal, try refreshing the browser. Wait 5 minutes and refresh again until it appears.

1. Right click the rule and select **Edit** from the **pop-up** menu.

   ![](../Media/lab9-s52.png)

1. Select the **Next: Set rule logic >** button.

1. Select the **Next: Incident settings >** button.

1. Select the **Next: Automated response >** button.

1. On the Automated response tab under **Automation rules**, select **+ Add new**.

   ![](../Media/lab9-s53.png)

1. On the **Create new Automation rule** page, provide the following details:   

   - For the **Automation rule name**, enter **Tier 2 (1)**

   - For **Trigger**, choose the **When incident is created (2)**

   - For the **Actions**, select **Assign owner (3)**

   - On the **Create new automation rule** page,select **<inject key="AzureAdUserEmail"></inject> (4)**

   - Then select **Apply (5)**

     ![](../Media/lab9-s54.png)

1. On the **Automation response** tab, select the **Next: Review and create >** button.

   ![](../Media/lab9-s55.png)
  
1. On the Analytics rule wizard, Select **Save**.

### Task 3: Test your new rule

In this task, you test your new scheduled query rule.

1. In the top bar of the Azure portal, select the icon **>_ (1)** that corresponds to the Cloud Shell. You might need to select the ellipsis icon first **(...)** if your display resolution is too low.

1. In the **Welcome to Azure Cloud Shell** window, select **Powershell (2)**.

   ![](../Media/lab9-s56.png)

1. On the **Getting started** page, select **Mount storage account (1)**, and then select your **Subscription (2)** from the **storage account subscription** drop-down menu item and select the **Apply (3)** button.

    ![](../Media/lab9-s57.png)

    >**Important:** Do not select the **No storage account required** radio button option. This will cause the incident creation to fail.

1. On the **Mount storage account** page, select **We will create a storage account for you (1)**, and then select **Next (2)**.

   ![](../Media/lab9-s59.png)

1. Wait until the Cloud Shell is **provisioned**, then **close** the Azure Cloud Shell window.

1. In the Search bar of the **Azure portal**, type **Activity Log (1)** and then select **Activity Log (2)**.

    ![](../Media/lab9-s60.png)

1. Make sure the following **Operation name** items appear: **List Storage Account Keys (1)** and **Update Storage Account Create (2)**. These are the operations that the KQL query you reviewed earlier will match to generate the alert. **Hint:** You might need to select **Refresh** to update the list.

    ![](../Media/lab9-s61.png)

1. Navigate to **Microsoft Defender** portal, expand **Investigation & response (1)**, expand **Incidents & alerts (2)**, and then select **Incidents (3)**.

   ![](../Media/lab9-s62.png)

1. You can not see the newly created Incident right now. As it takes some time.

1. The event that triggers the incident may take **5+ minutes** to process. Continue with the next exercise, and you will come back to this view later. You can check this **2-3 hrs** later after completing some of the labs.

    ![](../Media/lab9-s63.png)

    > **Note:** If you do not see **Incidents page** in the Microsoft Sentinel portal, try refreshing the browser. Wait 5 minutes and refresh again until it appears.

1. Select the Incident and review the information in the right blade.


### Review
In this lab, you have completed the following:

- Created a Scheduled Query.
- Edited the Scheduled Query
- Tested the new rule. 

## Select **Next** to continue to Exercise 4
