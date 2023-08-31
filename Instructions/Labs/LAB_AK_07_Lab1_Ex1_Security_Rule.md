# Module 7 - Lab 1 - Exercise 1 - Activate a Microsoft Security rule

## Lab scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel.  You need to enable alerts from other Microsoft 365 and Azure services.  

## Lab objective
 In this lab, you will be able to activate a Microsoft Security Rule

## Estimated time:  minutes

## Architecture Diagram

  ![Picture 1](../Media/SC200-Lab_Diagrams_Mod7_L1_Ex1.png)
  
### Task 1: Activate a Microsoft Security Rule

In this task, you will activate a Microsoft Security rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the **Sign in** dialog box, copy and paste * Email/Username: <inject key="AzureAdUserEmail"></inject> and then select Next.

1. In the **Enter password** dialog box, copy and paste * Password: <inject key="AzureAdUserPassword"></inject> and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select the Microsoft Sentinel Workspace you created in the previous labs.

 > **NOTE**: If not created follow the below steps:

    1. In the Search bar of the Azure portal, type *Log Analytics workspaces*, then select the same service name.
    1. Click on Create
    1. Select WIN-1 for the Resource group drop-down.
    1. For the Name, enter **uniquenameDefender**
    1. Select Review + Create.
    1. Once the workspace validation has passed, select Create. Wait for the new workspace to be provisioned, this may take a few minutes.
    1. Go to sentinel and click on create select the created workspace and click on add
        
1. Select **Analytics** from the Configuration area. By default, you will see the *Active rules*.

1. Select the + Create button from the command bar and select the Microsoft incident creation rule.

1. Under Name, enter Create incidents based on Defender for Endpoint.

1. Scroll down and under Microsoft security service select Microsoft Defender for Endpoint. 

1. Scroll down the page and under "Analytics rule logic - Filter by Severity", select the *Custom* drop-down list.

1. Under Filter by Severity, select the Custom option select Low, Medium, and High for the severity level, and go back to the rule.

1. Select the **Next: Automated response** button and then select **Next: Review + create** button.

1. Click on save

### Review
In this lab, you have activated a Microsoft Security Rule

## Proceed to Exercise 2
