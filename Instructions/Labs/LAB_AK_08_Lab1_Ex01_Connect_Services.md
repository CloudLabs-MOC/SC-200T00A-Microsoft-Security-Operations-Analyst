# Lab 08 - Exercise 1: Connect data to Microsoft Sentinel using data connectors

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The organization has data from Microsoft 365, Microsoft 365 Defender, Azure resources, non-Azure virtual machines, etc. You start connecting the Microsoft sources first.

## Lab Objectives
 In this lab, you will perform the following:
- Task 1: Create the Microsoft Sentinel Workspace
- Task 2: Connect the Microsoft Defender for Cloud data connector
- Task 3: Connect the Azure Activity data connector

### Estimated Timing: 20 Minutes

## Architecture Diagram

  ![Picture 1](../Media/mod8arch.png)

### Task 1: Create the Microsoft Sentinel Workspace

In this task, you will access your Microsoft Sentinel workspace.

1. In the Search bar of the Azure portal, type **Log Analytics workspaces (1)**, then select **Log Analytics workspaces (2)**.

    ![](../Media/lab6-s1.png)

1. Select **+ Create** from the command bar.

   ![](../Media/lab6-s2.png)

1. To create a **log analytics workspace**, follow these steps:

    - Subscription **Accept default subscription (1)**
    - Select **rg-defender (2)** for the Resource group.
    - For the Name, enter **uniquenameDefender (3)**.
    - Leave the **default Region (4)**.
    - Select **Review + Create (5)**.

      ![Picture 1](../Media/lab7-s1.png)

1. Once the workspace validation has passed, select **Create**.

    ![](../Media/lab7-s2.png)

1. Wait for the new workspace to be provisioned, this may take a few minutes.
 
1. In the Search bar of the Azure portal, type **microsoft sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](../Media/lab6-s5.png)

1. Select **+ Create** from the command bar.

    ![](../Media/lab6-s6.png)

 1. Select the newly created workspace **uniquenameDefender (1)** and click on **Add (1)**.
  
    ![](../Media/lab6-s7.png)

1. In the Microsoft Sentinel free trial activated tab, select **Ok**.

   ![](../Media/lab6-s8.png)

### Task 2: Connect the Microsoft Defender for Cloud data connector

In this task, you will connect the Microsoft Defender for Cloud data connector.

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. In the Microsoft Defender **Microsoft Sentinel (1)** navigation menu, scroll down to the **Content management (2)** section and select **Content Hub (3)**.

     ![](../Media/lab8-s1.png)

     > **Note:** If workspace is not connected, click on Connect workspace to connect. 

1.  In the **Content hub**, search for the **Microsoft Defender for Cloud (1)** solution and select **Microsoft Defender for Cloud (2)** from the list.

1. On the **Microsoft Defender for Cloud** solution details page select **Install (3)**.

   ![](../Media/lab8-s2.png)

    > **Note:** If the **Content hub** page does not load, refresh the browser until it appears.  

1. When the installation completes,  search for the **Microsoft Defender for Cloud** solution and select it.

1. On the **Microsoft Defender for Cloud** solution details page select **Manage**.

    ![](../Media/lab8-s3.png)

    >**Note:** The **Microsoft Defender for Cloud** solution installs the **Subscription-based Microsoft Defender for Cloud (Legacy)** Data connector, the **Tenant-based Microsoft Defender for Cloud (Preview)** Data connector, and an **Analytics rule**. The **Tenant-based Microsoft Defender for Cloud** Data connector is used when a tenant has multiple subscriptions.

1. Select the **Back** arrow to view the content items and access the connector page.

     ![](../Media/lab8-s6.1.png)

1. Select the **Tenant-based Microsoft Defender for Cloud (1)** Data connector check-box, and select **Open connector page (2)**.

   ![](../Media/lab8-s5.png)

1. Verify that the **Tenant-based Microsoft Defender** for Cloud connector status shows **Connected**.

     ![](../Media/lab8-s6.png)


### Task 3: Connect the Azure Activity data connector

In this task, you will connect the **Azure Activity** data connector.

1. In the Microsoft Sentinel left menus, scroll down to the **Content management** section and select **Content Hub**.

1. In the **Content hub**, search for the **Azure Activity (1)** solution and select **Azure Activity (2)** from the list.

1. On the **Azure Activity** solution page select **Install (3)**.

   ![](../Media/lab8-s7.png)

    > **Note:** If the **Content hub** page does not load, refresh the browser until it appears.  

1. Select the **Back** arrow to view the content items and access the connector page.

     ![](../Media/lab8-s8.png)

1. When the installation completes select **Manage**.

    ![](../Media/lab8-s7.1.png)

    >**Note:** The **Azure Activity** solution installs the **Azure Activity** Data connector, 12 **Analytics rules**, 14 **Hunting queries**, and 1 **Workbook**.

1. Select the **Azure Activity (1)** Data connector and select **Open connector page (2)**.

    ![](../Media/lab8-s9.png)

1. In the **Configuration** area under the **Instructions** tab, scroll down to "2. Connect your subscriptions through diagnostic settings new pipeline", and select **Launch Azure Policy Assignment Wizard>**.

    ![](../Media/lab8-s10.png)

1. It will open in new tab, in the **Basics** tab, select the ellipsis button **(...) (1)** under **Scope** and select your **subscription (2)** from the drop-down list and click **Select (3)**.

    ![](../Media/lab8-s11.png)

1. Select **Parameters (1)**, click the workspace picker **(2)** for **Primary Log Analytics workspace**, choose **uniquenameDefender (3)**, and then select **Select (4)**.

    ![](../Media/lab8-s12.png)

1. Select the **Remediation (1)** tab and select the **Create a remediation task (2)** checkbox. This action will apply the policy to existing Azure resources.

1. Select the **Review + Create (3)** button to review the configuration.

     ![](../Media/lab8-s13.png)

1. Select **Create** to finish.

   ![](../Media/lab8-s14.png)

## Review
In this lab, you have completed the following:

- Created and accessed the Microsoft Sentinel Workspace
- Connected the Microsoft Defender for Cloud data connector
- Connected the Azure Activity data connector

## Select **Next** to continue to Exercise 2
