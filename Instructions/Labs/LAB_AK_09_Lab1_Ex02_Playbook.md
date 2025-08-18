# Lab 09 - Exercise 2: Create a Playbook in Microsoft Sentinel

## Lab Scenario

You're a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. Now, you want to respond and reMediate actions that can be run from Microsoft Sentinel as a routine.

With a playbook, you can help automate and orchestrate your threat response, integrate with other systems both internal and external, and can be set to run automatically in response to specific alerts or incidents, when triggered by an analytics rule or an automation rule, respectively.

>**Important:** The lab exercises for **Learning Path #9** are in a **standalone** environment. If you exit the lab before completing it, you will need to re-run the configurations upon re-entering.

## Lab Objectives
  
After completing this lab, you will be able to:
- Task 1: Create a Playbook in Microsoft Sentinel
- Task 2: Update a Playbook in Microsoft Sentinel
- Task 3: Create an Automation Rule

## Estimated Timing: 30 Minutes

## Architecture Diagram

  ![Lab overview.](../Media/archdialab9ex2.png)

### Task 1: Create a Playbook in Microsoft Sentinel

In this task, you'll create a Logic App that is used as a Playbook in Microsoft Sentinel.

1. In the Azure portal's search bar type **Microsoft sentinel (1)**, and select **Microsoft Sentinel (2)**.

   ![Picture 1](../Media/sc-200-19.png)

1. Select **uniquenameDefender** Microsoft Sentinel Workspace.

   ![Picture 1](../Media/ss7.png)   

1. On Microsoft Sentinel page, click on **Go to Content Hub**.

   ![Picture 1](../Media/l9-e1-2.png) 

   > **Note:** If you do not see **Content hub page** in the Microsoft Sentinel portal, try refreshing the browser.

1. Within the search bar, search for **Sentinel SOAR Essentials (1)**, press **Enter** then select **Sentinel SOAR Essentials (2)** and then click on **Install (3)**.

   ![](../Media/ss11.png)

1. Within the solution details, select **Manage**.

    ![](../Media/ss12.png)

1. Find the **Defender_XDR_Ransomware_Playbook_for_SecOps-Tasks** playbook and select the name.

   ![](../Media/4.png)

1. Select the **Incident tasks - Microsoft Defender XDR Ransomware Playbook for SecOps (1)** template. Then, in the details pane, select **Create playbook (2)**.

    ![](../Media/7.png)

1. For Resource Group, select **Create New (1)**, enter **RG-playbooks (2)** and select **OK (3)**.

   ![](../Media/ss13.png)

1. For the **Playbook name**, enter **Defender_XDR_Ransomware_Playbook_SecOps-Tasks (1)** (note that this would exceed the limit of 64 characters). Then, click on Select **Next:Connections (2)**.

   ![](../Media/ss14.png)

1. On the **Create playbook** page, select **Next: Review and create**.

    ![](../Media/9.png)

1. On the **Create playbook** page, select **Create Playbook**.

    ![](../Media/l9-e3-1.png)

    >**Note:** Wait for the deployment to finish before proceeding to the next task.

### Task 2: Update a Playbook in Microsoft Sentinel

In this task, you’ll update the new playbook you created with the proper connection information.

1. In the Azure portal's search bar type **Microsoft sentinel (1)**, and select **Microsoft Sentinel (2)**.

   ![Picture 1](../Media/sc-200-19.png)

1. Select **uniquenameDefender** Microsoft Sentinel Workspace.

   ![Picture 1](../Media/ss7.png)

1. Select **Automation (1)** under the **Configuration** area and then select the **Active Playbooks (2)** tab.

1. Select **Refresh** from the command bar in case you don’t see any playbooks. You should see the playbook created from the previous step.

1. Select the **Defender_XDR_Ransomware_Playbook_SecOps_Tasks (3)** playbook name.

   ![](../Media/ss15.png)

1. On the Logic App page for **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**, in the command menu, select Edit.

    ![](../Media/12.png)

    >**Note:** You may need to refresh the page.

1.  On the Microsoft Sentinel incident page, select the **first block**.

    ![](../Media/ss16.png)

1. Select the **Change connection** link.

    ![](../Media/l9-e3-2.png)

1. Select **Add new** and then select **Sign in**. 

    ![](../Media/l9-e3-3.png)

1. In the new window. Select your **Azure subscription (1)** then click on **Sign in (2)**.

   ![](../Media/l9-e3-4.png)

1. Select your **<inject key="AzureAdUserEmail"></inject>** Admin credentials when prompted.

    ![](../Media/l9-e3-5.png)

1. The last line of the block should now read **Connected to your-admin-username**.

    ![](../Media/l9-e3-6.png)

1. Select **Save** on the command bar. The Logic App will be used in a future lab.

    ![](../Media/21.png)

### Task 3: Create an Automation Rule

In this task, you will create an automation rule in Microsoft Sentinel that runs a playbook based on specific tactics.

1. Navigate back to **uniquenameDefender** Microsoft Sentinel Workspace.

1. Select **Automation (1)** under **Configuration**.

1. Select **+ Create (2)** and choose **Automation Rule (3)**.

   ![](../Media/l9-e3-7.png)

1. On the **Create new Automation Rule** page, provide the following details:

   - Give the rule a name as **myautomationrule<inject key="DeploymentID" enableCopy="false"/> (1)**

   - Select **Trigger** as ***When incident is created (2)** 
   - Leave the **incident provider** as **All (3)**

   - Leave the **Analytic rule** name as **All (4)** 

   - Click **+ Add (5)** and Select **Condition(And) (6)**

     ![](../Media/ss18.png)

      > **Note:** If the **Condition** section is not automatically created and the **Incident provider** option is not available, manually add it as shown in the image below. Configure the **Analytic rule name** conditions accordingly. 

      ![](../Media/l9-e3-8.png)

1. From the drop down, select **Tactics (1)**.

1. Select the **Contains (2)** operator from the dropdown.

1. Select the following tactics **(3)**:
    - Reconnaissance
    - Execution
    - Persistence
    - Command and Control
    - Exfiltration
    - PreAttack

      ![](../Media/19.png)

1. Under Actions, select **Run Playbook (1)**.

1. Select the link to **Manage playbook permissions (2)**.

   ![](../Media/ss19.png)

1. On the *Manage Permissions* page, select the **rg-playbook (1)** resource group you created in the previous lab, and select **Apply (2)**.

   ![](../Media/ss20.png)

1. From the drop down list, select the **Defender_XDR_Ransomware_Playbook_SecOps_Tasks (1)** playbook and then select **Apply (3)** at the bottom.

   ![](../Media/l9-e3-10.png)

From here, depending on your role, you will either continue doing more architect exercises or you will pivot to the analyst exercises.

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Hit the Validate button for the corresponding task. You can proceed to the next task if you receive a success message.
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

   <validation step="9a03fda7-3dc7-407d-bbea-d9650d728011" />

### Review
In this lab, you have completed the following:

- Created a Playbook in Microsoft Sentinel
- Updated a Playbook in Microsoft Sentinel
- Created an Automation Rule

## Select **Next** to continue to Exercise 3
