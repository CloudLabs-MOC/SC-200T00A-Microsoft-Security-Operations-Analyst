---
lab:
    title: 'Exercise 02 - Connect Windows devices to Microsoft Sentinel using data connectors'
    module: 'Learning Path 6 - Connect logs to Microsoft Sentinel'
---

# Learning Path 6 - Lab 1 - Exercise 02 - Connect Windows devices to Microsoft Sentinel using data connectors

## Lab scenario

![Lab overview.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Windows virtual machines inside and outside of Azure, like On-Premises environments or other Public Clouds.


### Task 1: Create a Windows Virtual Machine in Azure

In this task, you will create a Windows virtual machine in Azure.

1. Login to **WIN1** virtual machine as Admin with the password: **Pa55w.rd**.  

1. In the Edge browser, navigate to the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy, and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. Select **+ Create a Resource**. **Hint:** If you were already in the Azure Portal, you might need to select *Microsoft Azure* from the top bar to go Home.

1. In the **Search services and marketplace** box, enter *Windows 10* and select **Microsoft Window 10** from the drop-down list.

1. Select the box for **Microsoft Window 10**.

1. Open the *Plan* drop-down list and select **Windows 10 Enterprise, version 22H2**.

1. Select **Start with a pre-set configuration** to continue.

1. Select **Dev/Test** and then select **Continue to create a VM**.

1. Select **Create new** for *Resource group*, enter RG-AZWIN01 as Name and select **OK**.

    >**Note:** This will be a new resource group for tracking purposes. 

1. In *Virtual machine name*, enter AZWIN01.

1. Leave **(US) East US** as the default value for *Region*.

1. Scroll down and review the *Image* for the virtual machine. If it appears empty, select **Windows 10 Enterprise, version 22H2**.

1. Review the *Size* for the virtual machine. If it appears empty, select **See all sizes**, choose the first VM size under *Most used by Azure users* and click **Select**.

1. Scroll down and enter a *Username* of your choosing. **Hint:** Avoid reserved words like admin or root.

1. Enter a *Password* of your choosing. **Hint:** It might be easier to re-use your tenant password. It can be found in the resources tab.

1. Scroll down to the bottom of the page and select the checkbox below *Licensing* to confirm you have the eligible license.

1. Select **Review + create** and wait until the validation is passed.

1. Select **Create**. Wait for the Resource to be created, this may take a few minutes.


### Task 2: Connect an Azure Windows virtual machine

In this task, you will connect an Azure Windows virtual machine to Microsoft Sentinel.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. From the Data Connectors Tab, search for the **Windows Security Events via AMA** connector and select it from the list.

1. Select **Open connector page** on the connector information blade.

1. In the *Configuration* section, select the **Create data collection rule**.

1. Enter **AZWIN01DCR** for Rule Name, then select **Next: Resources**.

1. Select **+Add resource(s)** to select the Virtual Machine we just created.

1. Expand **RG-AZWIN01**, then select **AZWIN01**.

1. Select **Apply** and then select **Next: Collect**.

1. Review the different Security Event collection option. Keep *All Security Events* and then select **Next: Review + create**.

1. Select **Create** to save the Data Collection Rule.

1. Wait a minute and then select **Refresh** to see the new data collection rule listed.


### Task 3: Connect a non-Azure Windows Machine

In this task, you will install Azure Arc and connect a non-Azure Windows virtual machine to Microsoft Sentinel.  

>**Important:** The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

>**Important:** The *Windows Security Events via AMA* data connector requires Azure Arc for non-Azure devices. 

1. Login to **WIN2** virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the Microsoft Edge browser.

1. Open a browser and log into the Azure Portal at https://portal.azure.com with the credentials you have been using in the previous labs.

1. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Arc*, then select **Azure Arc**.

1. In the navigation pane under **Infrastructure** select **Servers**.

    >**Note:** You should see WINServer in this view. If that is not the case, you probably onboarded WIN1 instead. Make sure you are in WIN2 for this exercise since we will need this Virtual Machine later.

1. Select **+ Add**.

1. Select **Generate script** in the "Add a single server" section.

1. In the *Add a server with Azure Arc* page, select a Resource group you created earlier under *Project details*. **Hint:** *RG-Defender*

    >**Note:** If you haven't already created a resource group, open another tab and create the resource group and start over.

1. Review the *Server details* and *Connectivity method* options. Keep the default values and select **Next** to get to the Tags tab.

1. Review the default available tags. Select **Next** to get to the Download and run script tab.

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select **Keep**. 

1. Right-click the Windows Start button and select **Windows PowerShell (Admin)**.

    >**Note:** You may need to search for **Windows PowerShell**. In the search box type in **PowerShell**. You should see the **Windows PowerShell App** appear. Select the **Run as Administrator** option.

1. In case you get a UAC prompt, enter *Administrator* for "Username" and *Passw0rd!* for "Password", else skip to next step.

1. Enter: cd C:\Users\Admin\Downloads

1. Type *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* and press enter.

1. Enter **A** for Yes to All and press enter.

1. Type *.\OnboardingScript.ps1* and press enter.  

    >**Important:** If you get the error *"The term .\OnboardingScript.ps1 is not recognized..."*, make sure you are doing the steps for Task 3 on the WIN2 virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for *".\OnboardingScript (1).ps1"* or other file numbers in the running directory.

1. Enter **R** to Run once and press enter (this may take a couple minutes).

1. The setup process will open a new Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message "Authentication complete" and then go back to the Windows PowerShell window.

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. 

1. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Servers** page.

1. Select **Refresh** until **WIN2**  name appears.

    >**Note:** This could take a minute to appear.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. Select *Data connectors* from the Configuration area, search for the **Windows Security Events via AMA** connector and select it from the list.

1. Select **Open connector page** on the connector information blade.

1. In the *Configuration* section, select the **Create data collection rule**.

1. Enter **WIN2** for Rule Name, then select **Next: Resources**.

1. Select **+Add resource(s)**.

1. Expand **RG-Defender** (or the Resource Group your created), then select **WIN2**.

1. Select **Apply**.

1. Select **Next: Collect**, then **Next: Review + create**.

1. Select **Create**.

1. Wait a minute and then select **Refresh** to see the new data collection rule listed.


## Proceed to Exercise 3
