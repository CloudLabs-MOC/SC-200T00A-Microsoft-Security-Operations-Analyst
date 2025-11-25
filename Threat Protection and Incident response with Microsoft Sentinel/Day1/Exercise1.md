
# Exercise 1 - Microsoft Sentinel Deployment

## Estimated Duration: 30 Minutes

## Overview

In this exercise, you will set up the foundational components required for Microsoft Sentinel. First, you will create a Log Analytics Workspace, it is a central repository where your security data will be collected, stored, and queried. This workspace serves as the backbone for Sentinel’s analytics and threat detection capabilities.

Next, you will deploy Microsoft Sentinel to the newly created workspace. Deploying Sentinel integrates advanced security analytics, threat intelligence, and incident response features into your environment. By completing this exercise, you will establish the core infrastructure that enables you to monitor security events, detect potential threats, and investigate incidents in subsequent exercises.

## Lab Objectives
 In this lab, you will perform the following:

- Task 1: Create a Log Analytics Workspace
- Task 2: Deploy Microsoft Sentinel to a workspace

### Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type **Log Analytics workspaces (1)**, then select **Log Analytics workspaces (2)**.

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

    ![](./images/Ex1-05-Az.png)

1. Select **+ Create** from the command bar.

    ![](./images/Ex1-06.png)

1. Select the newly created workspace named **uniquenameSentinel (1)** and click on **Add (2)**.
  
    ![](./images/Ex1-07.png)

1. In the **Microsoft Sentinel free trial activated** tab, select **Ok** to activate the free trial.

    ![](./images/Ex1-08.png)

1. Now you will see the **Getting started** page for Microsoft Sentinel.   

## Summary
In this lab, you have completed the following:

- Created a Log Analytics Workspace
- Deployed Microsoft Sentinel to a workspace

## You have successfully completed the exercise!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](./images/Next.png)