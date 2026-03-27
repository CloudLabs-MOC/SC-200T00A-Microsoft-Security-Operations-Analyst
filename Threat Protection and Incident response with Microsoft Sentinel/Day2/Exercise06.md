# Exercise 6: Exploring Microsoft Sentinel Advanced Features

## Estimated Duration: 20 Minutes

## Overview

In this exercise, you will explore **Microsoft Sentinel’s** advanced capabilities for enhancing security monitoring and visualization. You will start by connecting the Threat Intelligence data connector to enrich your environment with actionable threat indicators. Next, you will explore available workbook templates, customize a selected template, and create a new workbook to present security insights in a meaningful and interactive way.

## Lab Objectives

 In this lab, you will perform the following:

- Task 1: Connect the Threat Intelligence connector
- Task 2: Save a Workbook template
- Task 2:  Create a Workbook

### Task 1: Connect the Threat Intelligence connector

In this task, you will connect the Threat Intelligence data connector in Microsoft Sentinel by installing it from the Content Hub to create threat indicators for analysis.

 1. Navigate to **Microsoft Defender Portal**

      ```
      https://security.microsoft.com/
      ```

 1. On the left side menu, select **Microsoft Sentinel (1)** > **Content management (2)** and select **Content hub (3)** under the Configuration.

     ![Picture 1](../Day1/images/Ex1.png)

1. In the search bar, type **Threat intelligence (1)**, select **Threat intelligence (2)** from the list, then click on **Install (3)**. 

   ![](./images/Ex3-25.png)

1. Navigate to Defender Portal, expand **Threat intelligence (1)** from the left hand menu and select **Intel management (2)**. 

1. On **Intel management** page, click on **+ New (3)** under Indicator, then select **TI object (4)**.

   ![](../Day1/images/Ex3-00.png)

1. Review the different indicator types available in the ***Types*** dropdown. Select the **domain-name**. Enter your initials in the Domain box. You can use **onmicrosoft.com**.
1. On the **New TI objects** pane, enter the following details:

    - **Object type:** Select **Indicator (1)** from the dropdown menu.

    - Click on **+ New observable (2)**, select **Domain name** from the drop down.

    - **Domain name value:** Enter **onmicrosoft.com (3)**.

    - **Name:** provide **Indicator-test (4)**.

    - **Indicator types:** Select **Malicious activity (5)** from the dropdown menu.

    - **Valid from:** Keep **today's date (6)**.

    - **Valid untill:** Keep date of **next day (7)**.

    - **Source:** Should be **Microsoft Sentinel (8)**.

    - Then click on **Add (9)**.

      ![](../Day1/images/Ex3-01.png)

      **Note:** It could take a couple of minutes for the indicator to appear.

1. From the left hand pane in Defender portal, click on **Workbooks (1)** under **Threat management (2)**.

   ![Picture](./images/Ex3-07-def.png)

1. Select the *Templates* tab, and search for and select the **Threat Intelligence (1)** template workbook.

1. In the right details pane, scroll down and select the **View template (2)** button.

   ![Picture](./images/Ex3-10.png)

1. In the Threat Intelligence section, select the **Indicators Search** tab to view and analyze observed threat indicators and related logs.

   ![Picture](./images1/Ex3-08a.png)

### Task 2: Save a Workbook template

In this task, you will save a workbook template and modify it.

1. You should be back in the **Templates** tab with the **Threat Intelligence** workbook still selected.

1. Scroll down again and select the **Save (2)** button in the **Threat Intelligence (1)** workbook details pane.

    ![Picture](./images/Ex3-11.png)

1. Leave the default value for **Region (1)** and select **Yes (2)**.

   ![Picture](./images/Ex3-01.png)

1. Select the **Threat Intelligence (1)** workbook, then select the **View saved workbook (2)** button.

   >**Note:** It could take a couple of minutes for the indicator to appear.

   ![Picture](./images/Ex3-09.png)

1. Close the workbook.

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="52ef16d4-4132-4324-94b1-49f57a5593ec" />

### Task 3: Create a Workbook

In this task, you will create a new workbook with advanced visualizations.

1. You should be back at the **Workbooks** area of the Microsoft Sentinel portal.

1. Select **+ Add workbook** to create a new workbook from scratch. 

    ![Picture](./images/Ex3-12.png)

    >**Note:** Although it is a new workbook, a startup template is used.

1. A New Workbook template will open. Click on **Edit** to edit the workbook.

    >**Note:** The screenshot may differ from the actual lab experience, as some resources can take additional time to appear.

    ![Picture](./images/Wb-3.png)

1. Select the **Edit** button below the first paragraph of the workbook.

    ![Picture](./images/Wb-8.png)

1. Type **# My workbook (1)** in a new line on top of **## New workbook**, then scroll a bit to click **Done Editing (2)**.

    ![Picture](./images/Wb-0.png)

1. Select **Edit** visible next to the barchart.

    ![Picture](./images/Wb-2.png)

1. Review the KQL statement that provides a *union* statement of counts across all tables.

1. Scroll down and select the **X Cancel** on the bottom menu.

    ![Picture](./images/Wb-1.png)

1. Select the **+ Add (1)** below the barchart, then select **Add data source + visualization (2)**.

    ![Picture](./images/Wb-5.png)

1. Type **Heartbeat (1)** into the query box.

1. Change the *Time Range* to **Last 4 hours (2)**.

1. Change the *Visualization* to **Time Chart (3)**.

1. Change the *Size* to **Small (4)**.

1. Click on **Run Query (5)** and see the output.

1. Scroll down and select **Done Editing (6)** on the bottom menu.

    ![Picture](./images/Wb-6.png)

1. Select the **+ Add (1)** below the barchart, then select **Add data source + visualization (2)**.

    ![Picture](./images/Wb-5.png)

1. Type **SecurityAlert (1)** into the query box.

1. Change the *Time Range* to **Last 4 hours (2)**.

1. Change the *Visualization* to **Grid (3)**.

1. Change the *Size* to **Small (4)**.

1. Click on **Run Query (5)** and see the output.

1. Scroll down and select **Done Editing (6)** on the bottom menu, for the new *Editing query item: query - 3*.

    ![Picture](./images/Wb-7.png)

1. Select **Done Editing** in the Workbook's top command bar.

    ![Picture](./images/Wb-9.png)

1. Select the **Save** icon in the Workbook's top command bar.

    ![Picture](./images/Wb-10.png)

1. On the **Save Workbook** pop-up, enter the following details:

    - Change the *Title* to **My Workbook (1)**.
    - Keep the **Location (2)** as default region.
    - Click on **Save (3)**.

        ![Picture](./images/Wb-11.png)

1. Navigate back to the **Workbooks (1)** page in Defender potal, under **My Workbooks** tab, select the workbook you just created, **My Workbook (2)**.

1. On the right pane, select **View saved workbook (3)** to review your workbook.

    ![Picture](./images/Wb-12.png)

1. Now, you will see the newly created workbook.    

    ![Picture](./images/Wb-13.png)


### Summary
In this exercise, you connected the Threat Intelligence data connector, explored workbook templates, customized an existing template, and created a new workbook. These steps equipped you with the skills to enhance security data visualization and leverage enriched threat intelligence within Microsoft Sentinel. 

## You have successfully completed the exercise!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](./images/Next.png)
