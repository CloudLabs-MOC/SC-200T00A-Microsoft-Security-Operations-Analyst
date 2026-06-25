# Lab 08 - Exercise 9: Create workbooks

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. Once you have connected your data sources to Microsoft Sentinel, you can visualize and monitor the data using the Microsoft Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards. 

Microsoft Sentinel allows you to create custom workbooks across your data and also comes with built-in workbook templates to allow you to quickly gain insights across your data as soon as you connect a data source.

>**Important:** The lab exercises for Learning Path #9 are in a **standalone** environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will Understand following:
 - Task 1: Explore workbook templates
 - Task 2: Save and modify a workbook template
 - Task 3: Create a Workbook

## Estimated Timing: 20 Minutes

## Architecture Diagram

 ![Lab overview.](../Media/SC-200ex10upd.png)

### Task 1: Explore workbook templates

In this task, you will explore the Microsoft Sentinel workbook templates.

1. In the **Microsoft Defender** portal, expand **Threat management (1)** under **Microsoft Sentinel**, and then select **Workbooks (2)**.

   ![Picture 1](../Media/lab9-ex9-1.png)

1. On the **Workbooks** page, select the **Templates (1)** tab, search for **Azure Activity (2)**, select **Azure Activity (3)** from the results, and then choose **View Template (4)**.

   ![Picture 1](../Media/lab9-ex9-2.png)

1. Review the contents of the workbook. It shows insights into your Azure subscription operations by collecting and analyzing the data from the Activity Log.

   ![Picture 1](../Media/lab9-ex9-3.png)

1. Navigate back to workbooks and select Azure Activity from templates

### Task 2: Save and modify a workbook template

In this task, you will save a workbook template and modify it.

1. You should be back in the **Microsoft Sentinel - Workbooks - Templates** tab. Scroll down again and select the **Save** button for the **Azure Activity** workbook. 

   ![Picture 1](../Media/lab9-ex9-4.png)

1. Leave **East US** as the default value for *Region* and select **Yes**.

1. Select the **View saved workbook** button.

   ![Picture 1](../Media/lab9-ex9-5.png)

1. Select **Edit** in the command bar to enable changes in the workbook.

   ![Picture 1](../Media/lab9-ex9-6.png)

1. Scroll down to the **Caller activities over time** area, look at the color of the **Activities** column since we are going to format those columns. Select the **Edit**.

   ![Picture 1](../Media/lab9-june26-p11t1p1.png)

1. In the workbook edit view, select **Visual Formatting**, expand **Column Settings (1)**, choose **Activitie (2)** under **Columns**, set **Column renderer (3)** to **Heatmap**, select **Categorical (4)** for **Color palette**,

    ![Picture 1](../Media/lab9-june26-p11t1p2.png)

1. Now select **Apply Changes** at the top menu.

1. Now select **Done Editing** at the top menu.

   ![Picture 1](../Media/lab9-june26-p11t1p3.png)

1. Then select the **Save** icon. 

   ![Picture 1](../Media/lab9-june26-p11t1p4.png)

1. Return to the the **Microsoft Sentinel | Threat management | Workbooks** page.

### Task 3: Create a Workbook

In this task, you will create a new workbook with advanced visualizations.

1. You should be back at the **Workbooks** area of the Microsoft Sentinel portal.

1. Select **+ Add workbook** to create a new workbook from scratch. 

   ![Picture 1](../Media/lab9-june26-p11t1p5.png)

    >**Note:** Although it is a new workbook, a startup template is used.

    >**Note:** If **Workbook** page is not loading try refreshing the browser.
    
1. To edit the workbook, select **Edit** from the top bar.

   ![Picture 1](../Media/lab9-ex9-11.png)

1. Select the **Edit** icon above the new workbook overview of the workbook.

   ![Picture 1](../Media/lab9-june26-p11t1p6.png)

1. Type **# My workbook (1)** in a new line on top of **## New workbook**.

1. Select **Apply Changes (2)** on the bottom of this section, **Editing text item: text - 2**. Notice that your header increased in size and name changed.

   ![Picture 1](../Media/lab9-june26-p11t1p7.png)

1. In the bar chart section, select **Edit**.

   ![Picture 1](../Media/lab9-june26-p11t1p8.png)

1. Review the KQL statement that provides a *union* statement of counts across all tables.Select the **Discard Changes**.

   ![Picture 1](../Media/lab9-june26-p11t1p9.png)

1. Select the ellipsis (...) **(1)** next to **Edit**, choose **Add (2)**, and then select **Add data source + visualization (3)**.

   ![Picture 1](../Media/lab9-june26-p11t1p10.png)

1. Type **SecurityEvent (1)** into the query box.

   - Change the **Time Range** to **Last hour (2)**.

   - Change the **Visualization** to **Time chart (3)**.

     ![Picture 1](../Media/lab9-ex9-16.png) 

1. Navigate to **Visual Formatting (1)** tab, expand **Size (2)**, select **Make this item a custom width (3)**, set **Percent width (4)** to `25`, set **Maximum width (5)** to `25`, and then close the editor.

    ![Picture 1](../Media/lab9-ex9-17.png)

1. Navigate to **Step Settings (1)** tab, ensure **Refresh (2)** is selected under *Toolbar items*, and then select **Done Editing (3)**.

   ![Picture 1](../Media/lab9-ex9-18.png)

1. Select the drop-down arrow **(1)** next to **Edit**, choose **Add (2)**, and then select **Add data source + visualization (3)**.

   ![Picture 1](../Media/lab9-june26-p11t1p11.png)

1. Type **SecurityEvent (1)** into the query box.

1. Change the **Time Range** to **Last hour (2)**.

1. Change the **Visualization** to **Grid (3)**.

   ![Picture 1](../Media/lab9-ex9-20.png)

1. In the **Visual Formatting (4)** tab, expand **Size**, select **Make this item a custom width (1)**, set **Percent width (2)** to `75`, set **Maximum width (3)** to `75`, and then select **Done Editing (4)**.

    ![Picture 1](../Media/lab9-ex9-21.png)

1. Select **Done Editing** in Workbook's top command bar.

   ![Picture 1](../Media/lab9-june26-p11t1p12.png)

1. Select the **Save (1)** icon.

1. On the **Save Workbook** page,

   - Change the **Title** to **My Workbook (2)**.

   - Select **Save (3)** to commit the changes. 

     ![Picture 1](../Media/lab9-june26-p11t1p13.png)

1. Back in the **Workbooks (1)** page, select the **My workbooks (2)** tab.

1. Select the workbook you just created, **My workbook (3)**.

   ![Picture 1](../Media/lab9-ex9-24.png)

1. On the right pane, select **View saved workbook** to review your workbook.

   ![Picture 1](../Media/lab9-ex9-25.png)

## Review
In this lab, you have completed the following:

 - Explored workbook templates
 - Saved and modified a workbook template
 - Created a Workbook

## Click on **Next** to proceed to Exercise 10
