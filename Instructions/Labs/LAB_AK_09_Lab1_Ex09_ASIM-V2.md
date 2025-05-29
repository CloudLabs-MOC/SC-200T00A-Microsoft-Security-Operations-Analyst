# Module 9 - Lab 1 - Exercise 9 - Deploy ASIM parsers

## Lab Scenario

You're a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to model ASIM parsers for a specific Windows registry event. These parsers will be finalized at a later time following the [Advanced Security Information Model (ASIM) Registry Event normalization schema reference](https://docs.microsoft.com/azure/sentinel/registry-event-normalization-schema).

>**Important:** The lab exercises for Learning Path #9 are in a *standalone* environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will Understand following:

 - Task 1: Deploy the Registry Schema ASIM parsers

## Estimated Timing: 30 minutes

## Architecture Diagram

![Lab overview.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

### Task 1: Deploy the Registry Schema ASIM parsers

In this task, you'll review the Registry Schema parsers that are included with the Microsoft Sentinel deployment.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select **uniquenameDefender** Microsoft Sentinel Workspace.

<!--- 1. In the Edge browser, open a new tab (Ctrl+T) and navigate to the Microsoft Sentinel GitHub ASIM page <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>.

 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel).

    >**Note:** In the **ASIM** folder you can deploy templates that contain all ASIM parsers, but we will only focus on the Registry Schema.

1. Scroll down and next to **Registry Event**, select the **Deploy to Azure** button.

1. For *Resource Group*, select **RG-Defender** where your Sentinel workspace resides.

1. For *Workspace*, type your Sentinel workspace name, like *uniquenameDefender*.

1. Leave the other default values and select **Review + create**.

1. Select **Create** to deploy the template. Notice the Names of the different resources. 

1. After the deployment completes return to the *Microsoft Sentinel* tab. --->

1. Select **Logs** under the *General* left menu.

1. Open the *Schema and Filter* blade by selecting **>>** if needed.

1. Select the **Functions** tab (next to the Tables and Queries tabs). **Hint:** You might need to select the ellipsis icon **(...)** to select the tab.

1. In the *Search* bar type **registry**, and scroll down through the ASIM parser functions until you see the following **_Im_RegistryEvent_MicrosoftWindowsEventxxx** for Microsoft Windows under the *Microsoft Sentinel* heading.

    >**Note:** We're using the xxx in the ASIM parser function name to account for version changes. At the time this lab was updated the function was **_Im_RegistryEvent_MicrosoftWindowsEventV02**.

1. Hover over the **_Im_RegistryEvent_MicrosoftWindowsEventxxx** ASIM function and then select **Load the function code** in the popup window.

   ![Lab overview.](../Media/3.png)

1. Review the KQL that is parsing the Event ID 4657 to simplifying your analysis of the data in the Microsoft Sentinel workspace.

    >**Hint:** Typing ctrl+f in the code window brings up *Find* and makes searching for *EventID: 4657* much easier.

     ![Lab overview.](../Media/1.png)

1. In *Logs* Open a New Query tab.

1. Go back to the *Schema and Filter* blade and now hover the **_Im_RegistryEvent_MicrosoftWindowsEventxxx** *Registry Event ASIM filtering parser for Microsoft Windows Events and Security Events* and then select **Use in editor**.

   ![Lab overview.](../Media/2.png)

1. **Run** the ASIM function query. If you've completed the previous lab exercises you should see results and noerror messages.

## Review
In this lab, you have completed the following:
-  Deployed the Registry Schema ASIM parser. 

## Proceed to Exercise 10
