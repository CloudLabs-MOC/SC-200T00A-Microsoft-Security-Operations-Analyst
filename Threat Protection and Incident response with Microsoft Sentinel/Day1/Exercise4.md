
# Exercise 4 - UEBA with Microsoft Sentinel

## Estimated Duration: 20 Minutes

## Lab Scenario 

You need to configure Microsoft Sentinel to perform Entity Behavior Analytics to discover anomalies and provide entity analytic pages.

>**Note:** An **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Explore%20entity%20behavior%20analytics)** is available that allows you to click through this lab at your own pace. You may find slight differences between the interactive simulation and the hosted lab, but the core concepts and ideas being demonstrated are the same. 

## Lab objectives
 In this lab, you will perform the following:

- Task 1: Explore Entity Behavior 
- Task 2: Confirm and review Anomalies rules

## Architecture Diagram

  ![Picture 1](./images/SC200-Lab_Diagrams_Mod7_L1_Ex4.png)

### Task 1: Explore Entity Behavior 

In this task, you will explore Entity behavior analytics in Microsoft Sentinel.

1. In the Search bar of the Azure portal, type **Microsoft Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](./images/Ex1-05.png)

1. Select the **Microsoft Sentinel Workspace** you created earlier.

   ![](./images/Ex4-00.png)

1. On the **Microsoft Sentinel Workspace**, select **Entity behavior (1)** from the left hand pane. 

1. On the popup **Enable UEBA** from *Entity behavior settings*, select **Set UEBA (2)**.

    ![](./images/Ex4-12.png)

1. On the *Settings* tab under *Entity behaviour analytics*, scroll down the *Anomalies* section and verify read through the paragraph, and verify that the *switch* is **On (1)**.

1. Select the **Go to analytics in oder to configure the anomalies (2)** link.

   ![](./images/Ex4-13.png)

### Task 2: Confirm and review Anomalies rules

In this task, you will confirm Anomalies analytics rules are enabled.

1. You should be now at the **Analytics Rules** page. On **Anomalies (1)** tab, confirm **Status is Enabled (2)** for all the rules.

   ![](./images/Ex4-01.png)

1. Select any **Rule (1)**, then click on the **ellipsis (...) (2)** and select **Edit (3)** from the menu.

   ![](./images/Ex4-02.png)

1. Review the **General** tab information. Notice the *Status* is set to **Enabled (1)** *Mode* is **Production (2)** and then select **Next: Configuration> (3)**.

   ![](./images/Ex4-03.png)

1. Review the *Configuration* tab information. Notice that you cannot change the **Anomaly score threshold (1)**, then select **X (2)** in the top right corner to exit the **Analytics rule wizard**.

    ![](./images/Ex4-04.png)

1. Select any **Rule (1)**, then click on the **ellipsis (...) (2)** and select **Duplicate (3)** from the menu.

    ![](./images/Ex4-05.png)

1. Now, review and select the new rule with the **FLGT (1)** tab at the beginning of the name, then click on the **ellipsis (...) (2)** and select **Edit (3)** from the menu.

   ![](./images/Ex4-06.png)

1. Review the *General* tab information. Notice the *Status* is set to **Disabled (1)** *Mode* is **Flighting (2)** and then select **Next: Configuration> (3)**.

   ![](./images/Ex4-07.png)

1. Review the *Configuration* tab information. Notice that you can now change the **Anomaly score threshold**, then set the value to **1 (1)** and select **Next: Submit Feedback> (2)**.

   ![](./images/Ex4-08.png)

1. On Submit feedback page, leave all options as Default, then select **Next: Review and Create>**.

   ![](./images/Ex4-09.png)

1. Once the validation pass,then click **Save** to update the rule.

   ![](./images/Ex4-10.png)
    

    >**Note:** You can upgrade the Mode of the rule from **Flighting** to **Production** by changing the the *General* tab settings for therule and save the changes following the previous steps. The **Production** rule will become the **Flighting** rule afterwards.

     ![](./images/Ex4-11.png)

## Summary

### Now, click on **Next** from the lower right corner to move on to the next page.

   ![](./images/Next.png)