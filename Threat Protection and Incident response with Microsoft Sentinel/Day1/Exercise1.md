
# Exercise 1 - Microsoft Sentinal Deployment

## Estimated Duration: 60 Minutes

## Lab Scenario

You're a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You're responsible for setting up the Microsoft Sentinel environment to meet the company requirements to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.


## Lab Objectives
 In this lab, you will perform the following:

- Task 1: Create a Log Analytics Workspace
- Task 2: Deploy Microsoft Sentinel to a workspace

## Architecture Diagram

  ![Picture 1](./images/SC200-Lab_Diagrams_Mod5_L1_Ex1.png)

### Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Log Analytics (1)**, then select **Log Analytics workspaces (2)**.

   ![](./images/Ex1-00.png)

1. Select **+ Create** from the command bar.

   ![](./images/Ex1-01.png)

1. To create a **log analytics workspaces**, follow these steps:

    - Leave the **Subscription (1)** as default.
    - Select **sentinel-rg (2),** for Resource group.
    - For the Name, enter **uniquenameSentinel (3)**.
    - Leave the **Region (4)** as default.
    - Select **Review + Create (5)**.

      ![Picture 1](./images/Ex1-02.png)

1. Once the workspace validation has passed, select **Create**.

   ![](./images/Ex1-03.png)

1. Wait for the new workspace to be provisioned, this may take a few minutes.
   
   ![](./images/Ex1-04.png)

### Task 2 : Deploy Microsoft Sentinel to a workspace

In this task, you will deploy Microsoft Sentinel to an existing Log Analytics workspace, enabling it to collect, detect, and respond to security threats.

1. In the Search bar of the Azure portal, type **Microsoft Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](./images/Ex1-05.png)

1. Select **+ Create** from the command bar.

   ![](./images/Ex1-06.png)

1. Select the newly created workspace named **uniquenameSentinel (1)** and click on **Add (2)**.
  
   ![](./images/Ex1-07.png)

1. In the **Microsoft Sentinel free trial activated** tab, select **Ok**.

   ![](./images/Ex1-08.png)


## Summary
In this lab, you have completed the following:

- Created a Log Analytics Workspace
- Deployed Microsoft Sentinel to a workspace

## You have successfully completed the lab

### Now, click on **Next** from the lower right corner to move on to the next page.

   ![](./images/Next.png)