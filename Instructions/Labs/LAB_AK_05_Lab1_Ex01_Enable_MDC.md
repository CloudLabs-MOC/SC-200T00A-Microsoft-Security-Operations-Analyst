# Lab 05 - Exercise 1: Enable Microsoft Defender for Cloud

## Lab Scenario

You're a Security Operations Analyst working at a company that is implementing cloud workload protections with Microsoft Defender for Cloud. In this lab, you enable Microsoft Defender for Cloud.

>**Important:** The lab exercises for Learning Path #5 are conducted in a *standalone* environment. If you exit the lab before completion, you will need to re-run the configurations.

## Lab Objectives

 In this lab, you will perform the following:
- Task 1: Enable Microsoft Defender for Cloud
- Task 2: Understanding the Microsoft Defender for Cloud Dashboard
- Task 3: Install Azure Arc on an On-Premises Server

### Estimated Timing: 25 minutes

## Architecture Diagram

  ![Picture 1](../Media/Mod5_L1_Ex1.png)

### Task 1: Enable Microsoft Defender for Cloud

In this task, you'll enable and configure Microsoft Defender for Cloud.

1. In the Search bar of the Microsoft Azure portal, type **Defender for Cloud (1)**, then select **Microsoft Defender for Cloud (2)**.

   ![Picture 1](../Media/lab5-8.png)

1. In the left navigation menu for Microsoft Defender for Cloud, expand the *Management* section , and select **Environment settings**.

   ![Picture 1](../Media/lab5-9.png)

1. Select the **Expand all** button to view all subscriptions and resources.

1. Select the your subscription (or equivalent name in your Language).

   ![Picture 1](../Media/lab5-3.png)

1. Review the Azure resources that are now protected with the Defender for Cloud plans.

    >**Important:** If all Defender plans are *Off*, click **Enable all plans**. Then, select the *$200/month Microsoft Defender for APIs Plan 1* and click **Save**. Finally, click **Save** again at the top of the page and wait for the notification *"Defender plans (for your) subscription were saved successfully!"* to appear.

1. Review the **Azure resources** that are currently protected under the **Defender for Cloud plans**.

1. In the **Cloud Security Posture Management (CSPM)** section, set **Defender CSPM** to **On (1)**.

   ![Picture 1](../Media/lab5y1.png)

1. In the **Cloud Workload Protection (CWP)** section, set **Servers Plan 2 (2)** to **On (3)**.

1. Click the **Save (4)** button at the top of the page.

1. Select the **Settings & monitoring** tab from the Settings area (next to Save).

   ![Picture 1](../Media/lab5-10.png)

1. Review the monitoring extensions. It includes configurations for **Virtual Machines, Containers, and Storage Accounts**.

1. Close the "Settings & monitoring" page by selecting the **X** on the upper right of the page.

   ![Picture 1](../Media/lab5-11.png)

1. Close the settings page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**.

### Task 2: Understanding the Microsoft Defender for Cloud Dashboard

In this task, you will explore the Microsoft Defender for Cloud dashboard to familiarize yourself with its interface, features, and how it provides insights into your cloud environment's security posture.

1. In the Search bar of the Microsoft Azure portal, type **Defender for Cloud (1)**, then select **Microsoft Defender for Cloud (2)**.

   ![Picture 1](../Media/lab5-8.png)

1. In the left navigation menu for Microsoft Defender for Cloud, under the *General* section, select **Overview**.

   ![Picture 1](../Media/lab5-12.png)

1. The **Overview blade** offers a unified view of the **security posture** and includes multiple independent **cloud security pillars**, such as **Security posture**, **Regulatory compliance**, **Workload protections**, **Firewall Manager**, **Inventory**, and **Information Protection (preview)**. Each pillar also has its own dedicated dashboard, providing **deeper insights** and **actions** for that area, ensuring **easy access** and **better visibility** for security professionals.

    >**Note:** The top menu bar features a **Subscriptions** button, enabling you to view and filter subscriptions; in this lab, we will use just one subscription, but selecting different or additional subscriptions will update the interface to reflect the **security posture** of the selected subscriptions.

1. Click on the **What’s new** icon link – a new tab opens with the latest release notes where you can stay current on the new features, bug fixes, and more.

    ![Picture 1](../Media/lab5-13.png)

    >**Note:** The high-level numbers in the top menu provide a summary of your subscriptions, active recommendations, security alerts, and connected cloud accounts.

1. From the top menu bar, select **Azure subscriptions**. This will bring you into the environment settings where you can select from the available subscriptions.

   ![Picture 1](../Media/lab5-14.png)

1. Return to the **Overview** page, and review the **Security posture** tile. You can see your current **Secure score** along with the number of completed controls and recommendations. Selecting this tile will redirect you to a drill-down view across subscriptions.

1. On the **Regulatory compliance** tile, you can gain insights into your compliance posture through the continuous assessment of both **Azure** and **hybrid cloud environments**. This tile displays standards such as the **Microsoft Cloud Security benchmark** and the **Lowest compliance regulatory standard**. To view the data, you must first add **Security policies**.

   ![Picture 1](../Media/lab5-16.png)

1. Selecting this tile will redirect you to the **Regulatory compliance** dashboard – where you can add additional standards and explore the current ones.

1. We will continue exploring *Microsoft Defender for Cloud* **Security posture** and **Regulatory compliance** in the next exercise.

### Task 3: Install Azure Arc on an On-Premises Server

In this task, you install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps will be performed on a different machine than the one you were previously using. Be sure to check the Virtual Machine name references. 

>**Important:** The *Windows Security Events via AMA* data connector requires Azure Arc for non-Azure devices. 

1. In the lab virtual machine, Select **WINserver** from the desktop.

   ![Picture 1](../Media/46.png)

1. If **Connect to WINServer** prompted, click **Connect.**

   ![](../Media/l8e1-14.png)

1. Enter the **Password** as `Password.1!!` when prompted then hit on **Enter**.

   ![](../Media/l8e3-16.png)

1. In the **WINserver**, click on the Azure Portal icon as shown below:
 
   ![Launch Azure Portal](../Media/sc900-image(1).png)

1. In the **Sign in** dialog box, copy and paste **Email/Username: <inject key="AzureAdUserEmail"></inject>** and then select Next.

1. In the **Enter password** dialog box, copy and paste **Password: <inject key="AzureAdUserPassword"></inject>** and then select **Sign in**.

1. In the Search bar of the Azure portal, type **Azure arc (1)**, then select **Azure Arc (2)**.

   ![](../Media/l8e1-15.png)

1. In the navigation pane under **Azure Arc resources** select **Machines (1)**.

1. Select **+ Add/Create (2)**, then select **Add a machine (3)**.

   ![](../Media/l8e1-16.png)

1. Select **Generate script** from the "Add a single server" section.

   ![](../Media/l8e1-17.png)

1. In the **Add a server with Azure Arc** page, select the **RG-Defender (2)** Resource group under Project details.
 
1. For *Region*, select **(US) East Us (3)** from the drop-down list.

   ![](../Media/l8e118.png)

1. Review the **Server details** and **Connectivity method** options, keep the default values, and click **Next** to proceed to the **Tags** tab.

1. Review the default available tags. Select **Next** to get to the **Download and run script** tab.

   ![](../Media/l8e119.png)

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it.

   ![](../Media/l8e120.png)

1. Click on the downloaded file in the Edge download bar **(1)**, or select the ellipsis button (...) and choose **Keep (2)** to open it.

   ![](../Media/l8e121.png)
    
1. Right-click the Windows Start **(1)** button and select **Windows PowerShell (Admin) (2)**.

   ![](../Media/l8e1-11.png)

1. Enter *Administrator* for "Username" and *Password.1!!* for "Password" if you get a UAC prompt.

1. Enter: cd C:\Users\Administrator\Downloads

   ![](../Media/l8e122.png)

   >**Important:** If you do not have this directory, it most likely means you're on the wrong machine. Go back to the beginning of Task 4, switch to WINServer, and start over.

1. Type `Set-ExecutionPolicy -ExecutionPolicy Unrestricted` and press Enter.

1. Enter **A** for Yes to All and press enter.

   ![](../Media/l8e123.png)

1. Type **.\OnboardingScript.ps1** and press enter. 

   ![](../Media/l8e124.png)

   >**Important:** If you get the error **"The term .\OnboardingScript.ps1 is not recognized..."**, ensure you're following the steps for Task 4 in the WINServer virtual machine. Another issue could be that the file name changed due to multiple downloads; try searching for *".\OnboardingScript (1).ps1"* or other numbered versions in the current directory.

1. Enter **R** to Run once and press enter (this may take a couple minutes).

   ![](../Media/l8e125.png)

1. The setup process opens a new Microsoft Edge browser tab to authenticate the Azure Arc agent. Select **<inject key="AzureAdUserEmail"></inject>** account, wait for the message **Authentication complete** and then go back to the Windows PowerShell window.

    ![](../Media/l8e126.png)

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Machines** page.

    ![](../Media/l8e127.png)

1. Select **Refresh** until WINServer server name appears and the Status is *Connected*.
  
   ![](../Media/l8e128.png)

   >**Note:** **WINServer** may take a couple of minutes to appear.

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Hit the Validate button for the corresponding task. You can proceed to the next task if you receive a success message.
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

   <validation step="18d5bcdd-1127-45e5-a67e-66311175135e" />

## Review

In this lab, you have completed the following:

- Enabled Microsoft Defender for Cloud
- Explored the Microsoft Defender for Cloud Dashboard
- Installed Azure Arc on an On-Premises Server

## Select **Next** to continue to Lab 2
