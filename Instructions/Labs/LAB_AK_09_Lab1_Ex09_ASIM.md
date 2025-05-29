# Module 9 - Lab 1 - Exercise 9 - Deploy ASIM parsers

## Lab Scenario

You're a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to model ASIM parsers for a specific User Management event. These parsers will be finalized at a later time following the [Advanced Security Information Model (ASIM) User Management Event normalization schema reference].

>**Important:** The lab exercises for Learning Path #9 are in a *standalone* environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will Understand following:

 - Task 1: Deploy the User Management Schema ASIM parsers

## Estimated Timing: 30 minutes

## Architecture Diagram

![Lab overview.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

### Task 1: Deploy the User Management Schema ASIM parsers

In this task, you'll review the User Management Schema parsers that are included with the Microsoft Sentinel deployment.

1. In the Azure portal's search bar type **Microsoft sentinel (1)**, and select **Microsoft Sentinel (2)**.

   ![Picture 1](../Media/sc-200-19.png)

1. Select your Microsoft Sentinel Workspace.

1. Select **Logs** under the *General* left menu.

1. Open the *Schema and Filter* blade by selecting **>>** if needed.

1. Select the **Functions** tab (next to the Tables and Queries tabs). **Hint:** You might need to select the ellipsis icon **(...)** to select the tab.

1. In the *Search* bar type **user**, and scroll down through the ASIM parser functions until you see the following **_ASim_UserManagement** for Microsoft Windows under the *Microsoft Sentinel* heading.

1. Hover over the **_ASim_UserManagement** ASIM function and then select **Load the function code** in the popup window.

   ![Lab overview.](../Media/asim1.png)

1. In *Logs* Open a New Query tab.

1. Go back to the *Schema and Filter* blade and now hover the **_ASim_UserManagement** ASIM filtering parser for Microsoft Windows Events and Security Events* and then select **Use in editor**.

   ![Lab overview.](../Media/asim2.png)

1. **Run** the ASIM function query. If you've completed the previous lab exercises you should see results and noerror messages.

## Review
In this lab, you have completed the following:

-  Deployed the User Management Schema ASIM parser 

## Proceed to Exercise 10
