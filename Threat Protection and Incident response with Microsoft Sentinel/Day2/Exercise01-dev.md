# Exercise 1: Responding to Threats Using Automation

## Estimated Duration: 60 Minutes

## Overview

In this exercise, you will explore **Microsoft Sentinel's** advanced automation capabilities for responding to security threats. You will start by creating an analytics rule that detects new Azure CloudShell users, then create automation rules that automatically manage and respond to incidents based on predefined conditions. Next, you will design and build playbooks using Azure Logic Apps to orchestrate complex incident response workflows, including automated notifications, entity enrichment, and incident assignment. Finally, you will test the complete workflow by creating a new CloudShell user to trigger an actual alert. By completing this exercise, you will establish a proactive threat response infrastructure that reduces Mean Time to Respond (MTTR) and minimizes manual intervention in your security operations.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Create a Log Analytics Workspace
- Task 2: Deploy Microsoft Sentinel to a workspace
- Task 3: Connect the Azure Activity connector
- Task 4: Create an Analytics Rule
- Task 5: Create an Automation Rule for Incident Assignment
- Task 6: Create a Playbook for Automated Response
- Task 7: Link Playbooks to Automation Rules

### Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Log Analytics workspaces (1)**, then select **Log Analytics workspaces (2)**.

    ![](../Day1/images/Ex1-00.png)

1. Select **+ Create** from the command bar.

    ![](../Day1/images/Ex1-01.png)

1. To create a **log analytics workspaces**, follow these steps:

    - Leave the **Subscription (1)** as default.
    - Select **sentinel-rg (2),** for Resource group.
    - For the Name, enter **uniquenameSentinel (3)**.
    - Leave the **Region (4)** as default.
    - Select **Review + Create (5)**.

      ![Picture 1](../Day1/images/Ex1-02.png)

1. Once the workspace validation has passed, select **Create**.

    ![](../Day1/images/Ex1-03.png)

1. Wait for the new workspace to be provisioned, this may take a few minutes.
   
    ![](../Day1/images/Ex1-04.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="cdac5534-9c7d-41c9-bfa7-e147839de7f0" />

### Task 2 : Deploy Microsoft Sentinel to a workspace

In this task, you will deploy Microsoft Sentinel to an existing Log Analytics workspace, enabling it to collect, detect, and respond to security threats.

1. In the Search bar of the Azure portal, type **Microsoft Sentinel (1)**, then select **Microsoft Sentinel (2)**.

    ![](../Day1/images/Ex1-05-Az.png)

1. Select **+ Create** from the command bar.

    ![](../Day1/images/Ex1-06.png)

1. Select the newly created workspace named **uniquenameSentinel (1)** and click on **Add (2)**.
  
    ![](../Day1/images/Ex1-07.png)

1. In the **Microsoft Sentinel free trial activated** tab, select **Ok** to activate the free trial.

    ![](../Day1/images/Ex1-08.png)

1. Now you will see the **Getting started** page for Microsoft Sentinel.

    ![](../Day1/images/p1t2s5.png)

### Task 3: Connect the Azure Activity connector

In this task, you will connect the Azure Activity connector.

 1. Navigate to **Microsoft Defender Portal**

      ```
      https://security.microsoft.com/
      ```

1. On the left side menu, select **Microsoft Sentinel (1)** > **Content management (2)** and select **Content hub (3)** under the Configuration.

   ![Picture 1](../Day1/images/p1t3s1.png)

1. You will notice a message may appear advising that new spaces are being created, as this may take up to 10 minutes.

    ![Image](../Day1/images/e2t3s2.png)

1. On **Content hub** page, search for **Azure Activity (1)** and select **Azure Activity (2)** Data connector from the list,  and click on **Install (3)** to install it.

   ![Picture](../Day1/images/p1t3s4.png)

   >**Note:** If it doesn’t complete after a few minutes, you may be redirected to **Settings → Microsoft Sentinel**. Just **sign out** of all browser sessions and **sign in** again 2-3 times.  

1. Now, navigate to **Data connectors (1)** page, select the **Azure Activity (2)** Data connector, and select the **Open connector page (3)** on the connector information blade.

   ![Picture](../Day1/images/p1t3s5.png)

1. In the Configuration area, scroll down and under "2. Connect your subscriptions..." select **Launch Azure Policy Assignment wizard>**.

   ![Picture](../Day1/images/Ex2-07.png)

1. In the **Basics** tab, select the ellipsis button **(...) (1)** under **Scope** and select your **subscription (2)** from the drop-down list and click **Select (3)**.

   ![Picture](../Day1/images/Ex2-08.png)

1. In the **Parameters** tab, click the ellipsis button **(...) (1)** next to **Primary Log Analytics workspace** and select your **workspace (2)** from the drop-down list and click **Select (3)**.

   ![Picture](../Day1/images/Ex2-09.png)

1. Select the **Remediation** tab and select the **Create a remediation task (1)** checkbox. This action will apply the policy to existing Azure resources.

1. Select the **Review + Create (2)** button to review the configuration.

   ![Picture](../Day1/images/Ex2-10.png)

1. On **Review + create**, select **Create** to finish. 

   ![Picture](../Day1/images/Ex2-11.png)

    > **Note:** It may take **15–20 minutes** for the **Azure Activity** data connector to show a **Connected** status after configuration.

### Task 4: Create an Analytics Rule  

In this task, you will create an analytics rule using a Microsoft-provided template that detects when a new user creates an Azure CloudShell session. This will serve as the trigger for your automation workflows.

1. On the left side menu, select **Microsoft Sentinel (1)** > **Configuration (2)** > **Analytics (3)**.

    ![Picture](./images1/Ex6-01-analytics.png)

1. Click on **Rule templates (1)** and in the **Search** box, type **New CloudShell User (2)** and select the **New CloudShell User (1)** template from the results and click on **Create rule (4)**

    ![Picture](./images1/Ex6-03-search.png)

1. In the rule creation wizard, change the Severity to **Medium (1)** and click **Next: Set rule logic (2)**.

    ![Picture](./images1/Ex6-05-template-review.png)

1. On the **Set rule logic** page, review the detection query:

    ```KQL
    let match_window = 3m;
    AzureActivity
    | where ResourceGroup has "cloud-shell"
    | where (OperationNameValue =~ "Microsoft.Storage/storageAccounts/listKeys/action")
    | where ActivityStatusValue =~ "Success"
    | extend TimeKey = bin(TimeGenerated, match_window), AzureIP = CallerIpAddress
    | join kind = inner
    (AzureActivity
    | where ResourceGroup has "cloud-shell"
    | where (OperationNameValue =~ "Microsoft.Storage/storageAccounts/write")
    | extend TimeKey = bin(TimeGenerated, match_window), UserIP = CallerIpAddress
    ) on Caller, TimeKey
    | summarize count() by TimeKey, Caller, ResourceGroup, SubscriptionId, TenantId, AzureIP, UserIP, HTTPRequest, Type, Properties, CategoryValue, OperationList = strcat(OperationNameValue, ' , ', OperationNameValue1)
    | extend Name = tostring(split(Caller,'@',0)[0]), UPNSuffix = tostring(split(Caller,'@',1)[0])
    ```

    This query looks for new CloudShell session activities in Azure Activity logs.

    Click **Next: Incident settings**.

    ![Picture](./images1/Ex6-06-query.png)

1. On the **Incident settings** page, configure the incident settings:

    - **Incident settings:** Ensure **Create incidents from alerts triggered by this detection rule (1)** is **Enabled**
    - Group related alerts, triggered by this analytics rule, into incidents is **Enabled (2)**
    - **Alert grouping:** Select **Group all alerts into a single incident (3)** for this template
    - **Lookback period:** Leave as default

    Click **Next: Automated response (4)**.

    ![Picture](./images1/Ex6-07-incident.png)

1. On the **Automated response** page:

    - **Alert automation rules:** Leave empty for now (you'll link playbooks via automation rules in later tasks)
    - Click **Next: Review + Create**

        ![Picture](./images1/Ex6-09-create-00.png)

1. Review the rule configuration:

    - **Rule name:** New CloudShell User Detection
    - **Status:** **Enabled** 
    - **Severity:** Medium
    - Click **Save (2)** to create the analytics rule

        ![Picture](./images1/Ex6-09-create.png)

1. The analytics rule is now created and active. You should see a success message.

1. The rule is now running and will generate alerts when a new user creates a CloudShell session. You can verify it's enabled by navigating to **Analytics** and seeing it in the list with **Status: Enabled (1)**.

    ![Picture](./images1/Ex6-11-verify.png)

### Task 5: Create an Automation Rule for Incident Assignment

In this task, you will create an automation rule that automatically assigns incidents to specific users or groups based on incident severity and other criteria.

1. Navigate to **Microsoft Sentinel (1)** > **Configuration (2)** > **Automation (3)**.

    ![Picture](./images1/Ex6-13-create.png)

1. Click on **+ Create (1)** and select **Automation rule (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-12-automation.png)

1. On the **Create automation rule** page, enter the following details:

    - **Automation rule name:** Enter **Auto-Assign Ḥigh Severity Incidents (1)**
    - **Trigger:** Select **When incident is created (2)** from the dropdown menu

        ![Picture](./images1/Ex6-03-ex6.png)

1. Add a condition for severity. Click **+ Add (1)** and then select **Condition (And) (2)**:

    - **Incident property:** Select **Severity (3)**
    - **Operation:** Select **Equals (4)**
    - **Value:** Select **Low**, **Medium** and **High** **(5)**

        ![Picture](./images1/Ex6-14-details-2.png)

1. In the **Actions** section, select **Assign owner (1)** from the dropdown menu. In the **Assign owner (1)** action:

    - **Assigned to:** <inject key="AzureAdUserEmail"></inject> (2)
        
        ![Picture](./images1/Ex6-18-assign-2.png)

1. Add another action by clicking **Change status (1)** and select **New (2)** from the dropdown menu and then **Apply (3)**

    ![Picture](./images1/Ex6-19-tag.png)

1. The automation rule is now created. You should see it in the Automation rules list.

    ![Picture](./images1/Ex6-18-assign-2-a.png).

### Task 6: Create a Playbook for Automated Response

In this task, you will create a playbook using Azure Logic Apps to automate incident response actions such as sending notifications and enriching incident data.

1. Still in the **Automation** section, click **+ Create (1)** and select **Playbook with incident trigger (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-25-playbook.png)

1. On the **Create playbook** page, enter the following details:

    - **Subscription:** Default subscription **(1)**
    - **Resource group:** Select **sentinel-rg (2)**
    - **Name:** Enter **Incident-Notification-Playbook (3)**
    - **Enable diagnostics logs in Log Analytics:** Checked **(4)**
    - **Log Analytics workspace:** **uniquenameSentinel** **(5)**
    - Click **Next: Connections>** **(6)**

        ![Picture](./images1/Ex6-26-create.png)

1. Click on Next, and then click and click on **Create playbook** and once the playbook is created click on **Close and go to playbook**

    ![Picture](./images1/Ex6-26-create-2-a.png)

    ![Picture](./images1/Ex6-26-create-2.png)

1. Click **+ New step (1)** to add the first action in the workflow.

    ![Picture](./images1/Ex6-14-ex6.png)

1. Search for and select **Send an email (V2)** action from the **Office 365 Outlook** connector.

    ![Picture](./images1/Ex6-15-ex6.png)

1. On **Create connection** page click on Sign in and then select **<inject key="AzureAdUserEmail"></inject>** in the pop-up browser

    ![Picture](./images1/Ex6-15-ex6-2.png)

    ![Picture](./images1/Ex6-15-ex6-3.png)

   >**Note:** If you see an error as pop-ups blocked by browser, follow the steps from the below image

    ![Picture](./images1/Ex6-15-ex6-3-b.png) 

7. Enter the below details and click on **X**.
    - **To:** <inject key="AzureAdUserEmail"></inject>

    - **Subject:** Incident alert email

    - **Body:**

        ```
        Incident Name:@{item()}
        User details: @{triggerBody()?['incidentUpdates']?['updatedBy']?['name']}
        Source: @{triggerBody()?['incidentUpdates']?['updatedBy']?['source']}
        ```
        
        ![Picture](./images1/Ex6-19-ex6-0.png)

1. Click **Save (1)** to save the playbook workflow.

    ![Picture](./images1/Ex6-19-ex6.png)

### Task 7: Link Playbooks to Automation Rules

In this task, you will create an automation rule that triggers your newly created playbook when CloudShell incidents are generated.

1. Navigate back to **Microsoft Sentinel (1)** > **Configuration (2)** > **Automation (3)**.

1. Click **+ Create (1)** and select **Automation rule (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-38-create.png)

1. On the **Create automation rule** page, enter the following details:

    - **Automation rule name:** Enter **Trigger Notification Playbook (1)**
    - **Trigger:** Select **When incident is created (2)**

      ![Picture](./images1/Ex6-39-details.png)

1. In the **Conditions** section, click **+ Add condition (1)**:

    - **If:** Select **Analytic rule name (2)**
    - **Operation:** Select **Contains (3)**
    - **Value:** Type **New CloudShell user (4)**

      ![Picture](./images1/Ex6-40-condition.png)

1. You will see an error message **Only playbooks configured for the incident trigger can be selected. If a playbook appears unavailable, it means Microsoft Sentinel does not have explicit permissions to run it**, click on **Manage playbook permissions.**

    ![Picture](./images1/Ex6-40-sentinel-rg1.png)

1. On the **Manage permissions** page, select **sentinel-rg (1)** and click on **Apply (2)**

    ![Picture](./images1/Ex6-40-sentinel-rg.png)

1. Now, create the Automation rule again follow from step 2 in the same task and select the same options.

1. In the **Actions** section, click **+ Add action** and select **Run playbook** from the dropdown menu.
 In the **Run playbook** action:
    - **Playbook:** Select **Incident-Notification-Playbook** from the dropdown
    - Click **Add**

      ![Picture](./images1/Ex6-42-playbook.png)

1. Configure the rule settings:

    - **Rule expiration:** Leave as **Indefinite**
    - **Order:** Enter **2** (this will run after the assignment rule)
    - Click **Apply**

      ![Picture](./images1/Ex6-42-playbook.png)

1. The automation rule is now created and linked to your playbook. Verify it appears in the automation rules list (1).

    ![Picture](./images1/Ex6-44-list.png)

1. Navigate to Azure Portal and click on **Cloudshell.**

    ![Picture](./images1/322.png)

1. Select **PowerShell** in **Welcome to Azure Cloud Shell** box.

    ![Picture](./images1/323.png)

1. In **Getting started** pane select **Mount storage account (1)**, then select your current subscription in **Storage account and subscription (2)** and **Apply (3)**.

    ![Picture](./images1/324.1.png)

1. Select **We will create a storage account for you** and click on **Next.**

    ![Picture](./images1/325.1.png)

1. Wait for until deployment get finished.

    ![Picture](./images1/326.png)

1. Once Cloud Shell starts working, navigate to **Incidents** under **Incidents & alerts** in the **Microsoft Defender** portal. You will notice an incident named **New CloudShell user**.
    
    > **Note:** It may take up to 12 hours for the incident to be triggered, as there can be a delay before it appears.

    ![Picture](./images1/2121.png)

1. Navigate to the Outlook portal using the link below and click on **sign in.**

    ```
    https://www.microsoft.com/en-us/microsoft-365/outlook/log-in
    ```

    ![Image](./images/900.png "Enter Email")

1. On the **Sign in** tab you will see the login screen, in that enter the following email/username, and click on **Next (2)**. 

   * **Email/Username**: <inject key="AzureAdUserEmail"></inject> **(1)**
   
      ![Image](./images/901.png "Enter Email")
     
1. Now enter the following Temporary Access Pass and click on **Sign in (2)**.
   
   * **Temporary Access Pass**: <inject key="AzureAdUserPassword"></inject> **(1)**

      ![](../Day1/images/GS-0.png)

1. If you see the pop-up **Stay Signed in?**, select **No**.

   ![Image](./images/GettingStarted-07.png)
    
1. You will receive an email in **Outlook.**

    > **Note:** It may take up to 12 hours for the incident to be triggered. Since the incident is what activates the playbook that sends the email, you may not receive it immediately. If you do not see the email, you can still proceed to the next task.

    ![Picture](./images1/1212.png)

## Summary

In this exercise, you successfully:

- **Created an analytics rule** that detects new Azure CloudShell users
- **Created automation rules** that automatically assign incidents and add tags
- **Designed a playbook** that sends email notifications and enriches incidents
- **Linked the playbook** to automation rules for automated triggering

## You have successfully completed the exercise!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](./images/Next.png)