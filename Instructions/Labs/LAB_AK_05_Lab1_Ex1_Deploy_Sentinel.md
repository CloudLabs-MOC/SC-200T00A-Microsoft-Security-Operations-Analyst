# Module 5 - Lab 1 - Exercise 1 - Configure your Microsoft Sentinel environment

## Lab scenario

You're a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You're responsible for setting up the Microsoft Sentinel environment to meet the company requirement to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.

### Task 1: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. Log in to WIN1 virtual machine as Azureuser Admin with the password provided in the Environment tab.  

1. Open the Edge browser.

1. In the Edge browser, navigate to the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Username** provided in the environment details page (odl_user_DID@xxxxx.onmicrosoft.com) and then select Next.

1. In the **Enter password** dialog box, copy and paste in the Password and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Log Analytics workspaces*, then select the same service name.

1. Select **+Create** from the command bar.

1. Select **Create new** for the Resource group.

1. Enter *RG-Defender* and select **Ok**.

1. For the Name, enter *uniquenameDefender*.

1. Select **Review + Create**.

1. Once the workspace validation has passed, select **Create**. Wait for the new workspace to be provisioned, this may take a few minutes.

### Task 2: Initialize the Microsoft Sentinel Workspace.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select **+ Create**.

1. Next, In Add Microsoft Sentinel to a workspace page.

1. Select your existing workspace that was created in the previous lab, then select **Add**. This could take a few minutes.

1. Navigate around the newly created Microsoft Sentinel workspace to become familiar with the user interface options.


### Task 3: Create a Watchlist.

In this task, you will create a watchlist in Microsoft Sentinel.

1. In the search box at the bottom of the Windows 10 screen, enter *Notepad*. Select **Notepad** from the results.

1. Type *Hostname* then enter for a new line.

1. From row 2 of the notepad, copy the following hostnames, each one in a different line:

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, **File - Save As**, Name the file *HighValue.csv*, change the file type to **All files(*.*)** and select **Save**. **Hint:** The file can be saved in the *Documents* folder.

1. Close Notepad.

1. In Microsoft Sentinel, select the **Watchlist** option under the Configuration area.

1. Select **+ Add new** from the command bar.

1. In the Watchlist wizard, enter the following:

    |General setting|Value|
    |---|---|
    |Name|**HighValueHosts**|
    |Description|**High Value Hosts**|
    |Watchlist alias|**HighValueHosts**|

1. Select, **Next: Source >**.

1. Select **Browse for files** under *Upload file* and browse for the *HighValue.csv* file you just created.

1. In the *SearchKey field* select **Hostname**.

1. Select **Next: Review and Create >**.

1. Review the settings you entered and select **Create**.

1. The screen returns to the Watchlist page.

1. Select the *HighValueHosts* watchlist and on the right pane, select **View in logs**.

    >**Important:** It could take up to ten minutes for the watchlist to appear. **Please continue to with the following task and run this command on the next lab**.
    
    >**Note:** You can now use the _GetWatchlist('HighValueHosts') in your own KQL statements to access the list. The column to reference would be *Hostname*.

1. Close the *Logs* window by selecting the 'x' in the top-right and select **OK** to discard the unsaved edits.

### Task 4: Create a Threat Indicator.

In this task, you will create an indicator in Microsoft Sentinel.

1. In Microsoft Sentinel, select the **Threat intelligence** option in the Threat management area.

1. Select **+ Add New** from the command bar.

1. Review the different indicator types available in the *Types* dropdown. Select the **domain-name**. Enter your initials in the Domain box. An example would be *onmicrosoft.com*.

1. For the *Threat types*, add **malicious-activity** and select **OK**.

1. For the *Name*, enter the same value used for the Domain. An example would be *onmicrosoft.com*.

1. Set the *Valid from* field to today's date.

1. Select **Apply**.

    **Note:** It could take a couple of minutes for the indicator to appear.

1. Select the **Logs** option in the General area. You may need to disable the "Always show queries" option and close the *Queries* window to get run the statements.

1. Run the following KQL statement.

   ```KQL
   ThreatIntelligenceIndicator
   ```
   **Note:** You may need to wait for 20 minutes to get the expected output.

   Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.  

   ```KQL
   ThreatIntelligenceIndicator
   | project DomainName
   ```

   ![Picture 1](../Media/SC-200-img50.png)

## You have completed the lab.
