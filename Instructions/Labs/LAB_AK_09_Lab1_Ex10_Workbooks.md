# Module 9 - Lab 1 - Exercise 10 - Create workbooks

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. Once you have connected your data sources to Microsoft Sentinel, you can visualize and monitor the data using the Microsoft Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards. 

Microsoft Sentinel allows you to create custom workbooks across your data and also comes with built-in workbook templates to allow you to quickly gain insights across your data as soon as you connect a data source.

>**Note:** An **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20workbooks)** is available that allows you to click through this lab at your own pace. You may find slight differences between the interactive simulation and the hosted lab, but the core concepts and ideas being demonstrated are the same.

>**Important:** The lab exercises for Learning Path #9 are in a *standalone* environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will Understand following:
 - Task 1: Explore workbook templates
 - Task 2: Save and modify a workbook template
 - Task 3: Create a Workbook

## Estimated Timing: 20 minutes

## Architecture Diagram

 ![Lab overview.](../Media/SC-200ex10upd.png)

### Task 1: Explore workbook templates

In this task, you will explore the Microsoft Sentinel workbook templates.

1. In the Azure portal's search bar type **Microsoft sentinel (1)**, and select **Microsoft Sentinel (2)**.

   ![Picture 1](../Media/sc-200-19.png)

1. Select your **uniquenameDefender** Microsoft Sentinel Workspace.

   ![Picture 1](../Media/ss7.png)

1. Select **Workbooks (1)** under the *Threat Management* left blade. Select the **Templates (2)** tab.

   ![Picture 1](../Media/ss88.png)

1. Search for **Azure Activity (1)** press **Enter**. Then select the **Azure Activity (2)** template workbook. In the right pane, scroll down and select the **View template (3)** button.

   ![Picture 1](../Media/ss89.png)

1. Review the contents of the workbook. It shows insights into your Azure subscription operations by collecting and analyzing the data from the Activity Log.

   ![Picture 1](../Media/ss90.png)

1. Close the workbook by selecting the **X** in the top-right corner.

### Task 2: Save and modify a workbook template

In this task, you will save a workbook template and modify it.

1. You should be back in the **Microsoft Sentinel - Workbooks - Templates** tab. Scroll down again and select the **Save** button for the *Azure Activity* workbook. 

   ![Picture 1](../Media/savedactivity.png)

1. Leave **East US** as the default value for *Region* and select **Yes**.

1. Select the **View saved workbook** button.

   ![Picture 1](../Media/savedworkbook.png)

1. Select **Edit** in the command bar to enable changes in the workbook.

   ![Picture 1](../Media/ss91.png)

1. Scroll down to the **Caller activities over time** area, look at the color of the *Activities* column since we are going to format those columns. Select the **Edit** button below the grid.

   ![Picture 1](../Media/editcallerupd.png)

1. Select the **Column Settings** button, it is located to the right of the *Run Query* command bar. **Hint:** This button only appears if there is data from the KQL query.

   ![Picture 1](../Media/ss92.png)

1. In the *Edit column settings* blade that appears, within *Columns* select **Activities (1)**.

   - Change the value for *Column renderer* to **Heatmap (2)**. For *Colour palette*, scroll down to select **32-color categorical (3)**.

   - Select **Apply (4)**, then **Save and Close (5)**. Notice the change in the *Activities* column.

     ![Picture 1](../Media/ss93.png)   

1. Select **Done Editing** at the bottom of the query (not the top menu).

   ![Picture 1](../Media/ss94.png)

1. Now select **Done Editing** at the top menu.

1. Then select the **Save** icon. 

   ![Picture 1](../Media/ss95.png)

1. Close the workbook by selecting the **X** in the top-right corner.

### Task 3: Create a Workbook

In this task, you will create a new workbook with advanced visualizations.

1. You should be back at the **Workbooks (1)** area of the Microsoft Sentinel portal.

1. Select **+ Add workbook (2)** to create a new workbook from scratch. 

   ![Picture 1](../Media/ss96.png)

    >**Note:** Although it is a new workbook, a startup template is used.

1. To edit the workbook, select **Edit** from the top bar.

1. Select the **Edit** button below the new workbook overview of the workbook.

   ![Picture 1](../Media/ss97.png)

1. Type **# My workbook (1)** in a new line on top of *## New workbook*.

1. Select **Done Editing (2)** on the bottom of this section, *Editing text item: text - 2*. Notice that your header increased in size and name changed.

   ![Picture 1](../Media/ss98.png)

1. Select **Edit** below the only visible bar chart graph.

   ![Picture 1](../Media/ss99.png)

1. Review the KQL statement that provides a *union* statement of counts across all tables **(1)**. Scroll down and select the **Done Editing (2)** on the bottom menu.

   ![Picture 1](../Media/ss100.png)

1. Select the ellipsis **... (1)** next to the *Edit* button of the barchart graph, then select **+ Add (2)**, then select **Add query (3)**.

   ![Picture 1](../Media/ss101.png)

1. Type **SecurityEvent (1)** into the query box.

   - Change the *Time Range* to **Last hour (2)**.

   - Change the *Visualization* to **Time chart (3)**.

     ![Picture 1](../Media/ss102.png)   

1. Select the **Style** tab from the query's command bar.

   ![Picture 1](../Media/ss103.png)

1. On the **Edit query item** dialog box,

   - Select the **Make this item a custom width (1)** box.

   - Set the *Percent width* to **25 (2)** and *Maximum width* to **25 (3)**.

   - Now select **Advanced Settings (3)** tab from the query's command bar.

     ![Picture 1](../Media/ss104.png)   

1. Select **Show refresh icon when not editing (1)** box. 

1. Scroll down and select **Done Editing (2)** on the bottom menu, for the new *Editing query item: query - 2*.

   ![Picture 1](../Media/ss105.png)

1. Scroll down and at the bottom of the workbook select **+ Add (1)**, then **Add query (2)**.

    ![Picture 1](../Media/addqueryupd.png)

1. Type **SecurityEvent** into the query box.

1. Change the *Time Range* to **Last hour (1)**.

1. Change the *Visualization* to **Grid (2)**.

   ![Picture 1](../Media/grid.png)

1. Select **Style** from the query's command bar.

1. On the **Edit query item** dialog  box,

   - Select **Make this item a custom width (1)** box.

   - Set the *Percent width* to **75 (2)** and *Maximum width* to **75 (3)**.

   - Scroll down and select **Done Editing (4)** on the bottom menu, for the new *Editing query item: query - 3*.   

     ![Picture 1](../Media/ss106.png)

1. Select **Done Editing** in Workbook's top command bar.

1. Select the **Save** icon.

1. On the **Save As** page,

   - Change the *Title* to **My Workbook (1)**.

   - Select the **RG-DEFENDER (2)** resource group if needed and leave other values as default.

   - Select **Save as (3)** to commit the changes. 

     ![Picture 1](../Media/ss107.png)   

1. Close the workbook by selecting the **X** at the top-right or select **Workbooks** in the Microsoft Sentinel portal.

1. Back in the **Workbooks (1)** page, select the **My workbooks (2)** tab.

1. Select the workbook you just created, **My workbook (3)**.

   ![Picture 1](../Media/ss108.png)

1. On the right pane, select **View saved workbook** to review your workbook.

   ![Picture 1](../Media/ss109.png)

## Review
In this lab, you have completed the following:

 - Explored workbook templates
 - Saved and modified a workbook template
 - Created a Workbook

## Click on **Next** to proceed to Exercise 11
