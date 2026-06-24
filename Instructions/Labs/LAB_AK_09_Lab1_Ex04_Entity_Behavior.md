# Lab 09 - Exercise 3: Explore Entity Behavior Analytics

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules. 

You need to configure Microsoft Sentinel to perform Entity Behavior Analytics to discover anomalies and provide entity analytic pages.

>**Important:** The lab exercises for Learning Path #9 are in a **standalone** environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will perform the following:
- Task 1: Explore Entity Behavior 
- Task 2: Confirm and review Anomalies rules

## Estimated Timing: 20 Minutes

## Architecture Diagram

  ![Picture 1](../Media/archdialab9ex4.png)

### Task 1: Explore Entity Behavior 

In this task, you will explore Entity behavior analytics in Microsoft Sentinel.

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. In the **Microsoft Defender** portal, expand **System (1)**, select **Settings (2)**, and then choose **Microsoft Sentinel (3)**.

     ![Lab overview.](../Media/lab9-s64.png)

1. In **Workspaces**, select the **defender (uniquenameDefender) (1)** workspace, expand **Entity behavior analytics (2)**, and then choose **Configure UEBA (3)**.

    ![Lab overview.](../Media/lab9-s65.png)

1. On the **UEBA (User and Entity Behavior Analytics)** page, turn on **Turn on UEBA feature (1)**, verify **Microsoft Entra ID (2)** is enabled, and then select **Connect available data sources (3)**.

    ![Lab overview.](../Media/lab9-s67.png)

1. At the top of the Microsoft Sentinel settings menu, SIEM workspaces and select **Workspaces**, select the **defender** workspace, expand **Anomalies (1)**, and then choose **Configure anomalies in analytics (2)**.

     ![Lab overview.](../Media/lab9-s68.png)

### Task 2: Confirm and review Anomalies rules

In this task, you will confirm Anomalies analytics rules are enabled.

1. You should be now at the **Analytics** page, **Anomalies (1)** tab.

1. Confirm status column of the rules is **Enabled (2)**.

    ![Lab overview.](../Media/lab9-s69.png)

1. Select any rule **(1)** then select **ellipsis (...) (2)** icon at the right of the rule and then click **Edit (3)**.

    ![](../Media/lab9-s70.png)

    >**Note:** If you are not able to select the edit option, please refresh the page. Navigate to other tabs then come back to the **Anomalies** tab.

1. Review the **General** tab information. Notice the **Mode** is **Production (1)** and then select **Next: Configuration (2)**.

    ![](../Media/lab9-s71.png)

1. Review the **Configuration** tab information. Notice that you cannot change the **Anomaly score threshold**.

    ![](../Media/lab9-s72.png)

1. Then select **Cancel** to exit the Analytics rule wizard.

1. Scroll right to the analytics rule you selected until see and select the ellipsis **(...)** icon.

1. Select **Duplicate**.

    ![](../Media/lab9-s73.png)

1. Scroll left to review the new rule with the **FLGT** tab at the beginning of the name.

1. Select **FLGT (1)** rule and then select **Edit (2)** on the rule blade.

    ![Lab overview.](../Media/lab9-s74.png)

1. Review the **General** tab information. Notice the **Mode** is **Flighting (1)** and then select **Next: Configuration (2)**.

    ![Lab overview.](../Media/lab9-s75.png)

1. Review the **Configuration** tab information. Notice that you can now change the **Anomaly score threshold**.

1. Set the value to **1 (1)** and then select **Next: Submit Feedback (2)**.

    ![](../Media/lab9-s76.png)

1. Select **Next: Review + Create>** and then **Save** to update the rule.

    >**Note:** You can upgrade the **Flighting** rule to **Production** by modifying the setting on this rule and saving the changes. The existing **Production** rule will then become the new **Flighting** rule.
    
### Review
In this lab, you completed follwing tasks:

- Explored Entity Behavior 
- Confirmed and reviewed Anomalies rules

## Select **Next** to continue to Exercise 4
