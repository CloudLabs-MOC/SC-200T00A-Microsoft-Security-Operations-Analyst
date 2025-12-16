# Exercise 1: Responding to Threats Using Automation

## Estimated Duration: 120 Minutes

## Overview

In this exercise, you will explore **Microsoft Sentinel's** advanced automation capabilities for responding to security threats. You will start by creating an analytics rule that detects new Azure CloudShell users, then create automation rules that automatically manage and respond to incidents based on predefined conditions. Next, you will design and build playbooks using Azure Logic Apps to orchestrate complex incident response workflows, including automated notifications, entity enrichment, and incident assignment. Finally, you will test the complete workflow by creating a new CloudShell user to trigger an actual alert. By completing this exercise, you will establish a proactive threat response infrastructure that reduces Mean Time to Respond (MTTR) and minimizes manual intervention in your security operations.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Create an Analytics Rule 
- Task 2: Create an Automation Rule for Incident Assignment
- Task 3: Create a Playbook for Automated Response
- Task 4: Link Playbooks to Automation Rules
- Task 5: Test Automated Response Workflows with Real CloudShell User Creation

### Task 1: Create an Analytics Rule  

In this task, you will create an analytics rule using a Microsoft-provided template that detects when a new user creates an Azure CloudShell session. This will serve as the trigger for your automation workflows.

1. Navigate to **Microsoft Defender Portal**

    ```
    https://security.microsoft.com/
    ```

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
    - Click **Next: Review**

1. Review the rule configuration:

    - **Rule name:** New CloudShell User Detection
    - **Status:** **Enabled** 
    - **Severity:** Medium
    - Click **Save (2)** to create the analytics rule

    ![Picture](./images1/Ex6-09-create.png)

1. The analytics rule is now created and active. You should see a success message (1).

1. The rule is now running and will generate alerts when a new user creates a CloudShell session. You can verify it's enabled by navigating to **Analytics** and seeing it in the list with **Status: Enabled (1)**.

    ![Picture](./images1/Ex6-11-verify.png)

### Task 2: Create an Automation Rule for Incident Assignment

In this task, you will create an automation rule that automatically assigns incidents to specific users or groups based on incident severity and other criteria.

1. Navigate to **Microsoft Sentinel (1)** > **Configuration (2)** > **Automation (3)**.

    ![Picture](./images1/Ex6-13-create.png)

1. Click on **+ Create (1)** and select **Automation rule (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-12-automation.png)

1. On the **Create automation rule** page, enter the following details:

    - **Automation rule name:** Enter **Auto-Assign Ḥigh Serverity Incidents (1)**
    - **Trigger:** Select **When incident is created (2)** from the dropdown menu

    ![Picture](./images1/Ex6-14-details.png)

1. Add a condition for severity. Click **+ Add** again:

    - **Property:** Select **Severity (2)**
    - **Operation:** Select **Equals (3)**
    - **Value:** Select **Medium (4)** and **High (5)**
    - Click **Add (6)**

    ![Picture](./images1/Ex6-16-condition2.png)

1. In the **Actions (1)** section, click **+ Add action (2)** and select **Assign owner** from the dropdown menu. In the **Assign owner (1)** action:

    - **Assigned to:** Select your Azure admin email address **(2)**
    - Click **Add (3)**

    ![Picture](./images1/Ex6-18-assign.png)

1. Add another action by clicking **Change status (1)** and select **New (2)** from the dropdown menu and then **Apply (3)**

    ![Picture](./images1/Ex6-19-tag.png)

1. The automation rule is now created. You should see it in the Automation rules list (1).

    ![Picture](./images1/Ex6-24-list.png)

### Task 3: Create a Playbook for Automated Response

In this task, you will create a playbook using Azure Logic Apps to automate incident response actions such as sending notifications and enriching incident data.

1. Still in the **Automation** section, click **+ Create (1)** and select **Playbook with incident trigger (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-25-playbook.png)

1. On the **Create playbook** page, enter the following details:

    - **Subscription:** Default subscription **(1)**
    - **Resource group:** Select **sentinel-rg (2)**
    - **Name:** Enter **Incident-Notification-Playbook (3)**
    - **Enable diagnostics logs in Log Analytics:** Checked **(4)**
    - **Log Analytics workspace:** uniquenameSentinel **(5)**
    - Click **Next:Connections>** **(6)**

    ![Picture](./images1/Ex6-26-create.png)

1. Click on Next, and then click and click on **Create playbook** and once the playbook is created click on Close and go to playbook

    ![Picture](./images1/Ex6-26-create-2.png)

1. Click **+ New step (1)** to add the first action in the workflow.

    ![Picture](../images1/Ex6-14-ex6.png)

1. Search for and select **Send an email (V2)** action from the Office 365 Outlook connector.

    ![Picture](../images1/Ex6-15-ex6.png)

1. On **Create connection** page click on Sign in and then select 
**<inject key="AzureAdUserEmail"></inject>** in the pop-up browser

    ![Picture](../images1/Ex6-15-ex6-2.png)

1. Enter the below details and click on **X**.
    - **To:** <inject key="AzureAdUserEmail"></inject>
    - **Subject:** Incident alert email
    - **Body:**
        ```
        Incident Name:@{item()}
        User details: @{triggerBody()?['incidentUpdates']?['updatedBy']?['name']}
        Source: @{triggerBody()?['incidentUpdates']?['updatedBy']?['source']}
        ```

1. Click **Save (1)** to save the playbook workflow.

    ![Picture](../images1/Ex6-19-ex6.png)

### Task 4: Link Playbooks to Automation Rules

In this task, you will create an automation rule that triggers your newly created playbook when CloudShell incidents are generated.

1. Navigate back to **Microsoft Sentinel (1)** > **Configuration (2)** > **Automation (3)**.

1. Click **+ Create (1)** and select **Automation rule (2)** from the dropdown menu.

    ![Picture](./images1/Ex6-38-create.png)

1. On the **Create automation rule** page, enter the following details:

    - **Automation rule name:** Enter **Trigger CloudShell Response Playbook (1)**
    - **Trigger:** Select **When incident is created (2)**
    - Status: Ensure **Enabled (3)** is selected

    ![Picture](./images1/Ex6-39-details.png)

1. In the **Conditions (1)** section, click **+ Add condition (2)**:

    - **If:** Select **Analytic rule name (3)**
    - **Operation:** Select **Contains (4)**
    - **Value:** Type **CloudShell (5)**
    - Click **Add (6)**

    ![Picture](./images1/Ex6-40-condition.png)

1. In the **Actions (1)** section, click **+ Add action (2)** and select **Run playbook (3)** from the dropdown menu.

    ![Picture](./images1/Ex6-41-action.png)

1. In the **Run playbook** action:

    - **Playbook:** Select **CloudShell-Incident-Response (1)** from the dropdown (the playbook you created in Task 3)
    - Click **Add (2)**

    ![Picture](./images1/Ex6-42-playbook.png)

1. Configure the rule settings:

    - **Rule expiration:** Leave as **Indefinite (1)**
    - **Order:** Enter **2 (2)** (this will run after the assignment rule)
    - Click **Apply (3)**

    ![Picture](./images1/Ex6-43-apply.png)

1. The automation rule is now created and linked to your playbook. Verify it appears in the automation rules list (1).

    ![Picture](./images1/Ex6-44-list.png)

### Task 5: Test Automated Response Workflows with Real CloudShell User Creation

In this task, you will test the complete automated response workflow by creating a new Azure CloudShell user, which will trigger the analytics rule, create an incident, and execute your automation rules and playbook.

#### Create a New CloudShell User in Azure

1. Open a new browser tab and navigate to **Azure Portal**:

    ```
    https://portal.azure.com/
    ```

1. Sign in with your Azure admin credentials if not already signed in.

    ![Picture](./images1/Ex6-45-azure.png)

1. At the top of the portal, click the **Cloud Shell icon (1)** (looks like a terminal/command prompt).

    ![Picture](./images1/Ex6-46-cloudshell-icon.png)

1. If this is the first time you're opening Cloud Shell, you will see a welcome message. Select your preferred shell environment:

    - **Bash (1)** or **PowerShell (2)**
    - For this exercise, select **Bash (1)**

    ![Picture](./images1/Ex6-47-shell-select.png)

1. The system will create a new storage account for Cloud Shell. Click **Create storage (1)** to proceed.

    ![Picture](./images1/Ex6-48-storage.png)

1. Wait for Cloud Shell to initialize. This will generate Azure Activity logs indicating a new user has accessed Cloud Shell.

    ![Picture](./images1/Ex6-49-init.png)

1. Once Cloud Shell is open, you can see the terminal is now active (1). This action creates an Azure Activity log entry for the new CloudShell user access.

    ![Picture](./images1/Ex6-50-terminal.png)

1. Type a simple command in Cloud Shell to generate more activity

    ```bash
    az account show
    ```

    ![Picture](./images1/Ex6-51-command.png)

1. Close Cloud Shell by clicking the **X (1)** on the Cloud Shell pane.

    ![Picture](./images1/Ex6-52-close.png)

#### Monitor Alert Generation in Sentinel

1. Go back to your **Microsoft Sentinel** browser tab.

    ![Picture](./images1/Ex6-53-sentinel.png)

1. Navigate to **Microsoft Sentinel (1)** > **Threat management (2)** > **Incidents (3)** to view generated incidents.

    ![Picture](./images1/Ex6-54-incidents.png)

1. **Wait for 5-10 minutes** for the analytics rule to execute and generate an alert. The analytics rule runs on a schedule (typically every 5 minutes).

    ![Picture](./images1/Ex6-55-wait.png)

1. After 5-10 minutes, refresh the **Incidents** page by clicking the **Refresh (1)** button or pressing **F5**.

    ![Picture](./images1/Ex6-56-refresh.png)

1. You should now see a **new incident titled "New CloudShell User" (1)** with:

    - **Severity:** Medium
    - **Status:** Assigned (from your automation rule)
    - **Owner:** Your admin email (assigned by your automation rule)

    Click on the incident to view details **(2)**.

    ![Picture](./images1/Ex6-57-incident.png)

1. In the incident details pane, you will see:

    - **Incident Title:** New CloudShell User
    - **Status:** Assigned
    - **Owner:** Your name/email
    - **Tags:** CloudShell-Detection (from your automation rule)
    - **Comments:** Automated response comment from your playbook

    Verify all automation rule actions were executed **(1)**.

    ![Picture](./images1/Ex6-58-details.png)

#### Verify Playbook Execution and Email Notification

1. Check your **email inbox** for the notification email sent by the **CloudShell-Incident-Response** playbook.

    ![Picture](./images1/Ex6-59-email.png)

1. Open the email and verify it contains:

    - **Subject:** CloudShell Incident Alert - New CloudShell User
    - **Body content:**
        - Incident Name
        - Incident Severity
        - Incident Status
        - Created Time
        - Alert Details
        - CloudShell User information
        - IP Address of the user

    This confirms your playbook executed successfully **(1)**.

    ![Picture](./images1/Ex6-60-email-content.png)

#### Verify Automation Rule Execution History

1. Navigate back to **Microsoft Sentinel (1)** > **Configuration (2)** > **Automation (3)**.

    ![Picture](./images1/Ex6-61-automation.png)

1. Click on the **"Trigger CloudShell Response Playbook" (1)** automation rule to view its execution history.

    ![Picture](./images1/Ex6-62-rule.png)

1. In the rule details, scroll down to see **Run history (1)** showing:

    - **Execution time:** When the rule triggered
    - **Status:** Succeeded/Failed
    - **Actions executed:** Playbook run status

    This confirms the automation rule triggered your playbook **(2)**.

    ![Picture](./images1/Ex6-63-history.png)

1. You can also navigate to **Logic Apps (1)** in the Azure portal to view the playbook execution details:

    - Go to https://portal.azure.com/
    - Search for **Logic Apps (2)**
    - Select **CloudShell-Incident-Response (3)**
    - View the **Runs (4)** to see execution details

    ![Picture](./images1/Ex6-64-logicapp.png)

## Summary

In this exercise, you successfully:

- **Created an analytics rule** that detects new Azure CloudShell users
- **Created automation rules** that automatically assign incidents and add tags
- **Designed a playbook** that sends email notifications and enriches incidents
- **Linked the playbook** to automation rules for automated triggering
- **Tested the complete workflow** by creating a real CloudShell user, which generated an alert that triggered the entire automated response chain

## You have successfully completed the exercise!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](./images/Next.png)