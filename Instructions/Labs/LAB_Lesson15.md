# LAB PREREQUISITES

### Estimated Timing: 60 Minutes

## Prerequisites to be completed before proceeding to further exercises

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Connect a non-Azure Windows Machine
- Task 2: Persistence Attack with Registry Key Add
- Task 3: Command and Control Attack with DNS
- Task 4: Privilege Elevation Attack with User Add

## Task 1: Connect a non-Azure Windows Machine

In this task, you will install Azure Arc and connect a non-Azure Windows virtual machine to Microsoft Sentinel.

> **Important:** The next steps are done on a different machine than the one you were previously working on. Look for the Virtual Machine name references.

> **Important:** The **Windows Security Events via AMA** data connector requires Azure Arc for non-Azure devices.

1. In the lab virtual machine, Select **WINserver** from the desktop.

   ![Picture 1](../Media/lab9-s1.png)

1. If **Connect to WINServer** prompted, click **Connect.**

   ![Picture 1](../Media/lab9-s2.png)

1. Enter the **Password** as `Password.1!!` when prompted.

   ![Picture 1](../Media/lab9-s3.png)

1. Open the Microsoft Edge browser inside **WINSERVER**.

1. On your virtual machine, click on the **Azure Portal** icon as shown below:

   ![Launch Azure Portal](../Media/lab9-s4.png)

1. You'll see the **Sign into Microsoft Azure** tab. Here, enter your credentials:
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

     ![Enter Your Username](../Media/sc900-image-1.png)

1. Next, provide your password:
   - **Password:** <inject key="AzureAdUserPassword"></inject>

     ![Enter Your Username](../Media/lab9-s5.png)

1. If prompted to stay signed in, you can click **No**.

   ![](../Media/AZ-500-staysignedin.png)

   > **Note:** If you are not able to copy-paste the username and password then:
   >
   > - Go to Hyper-V manager.
   > - On the left-right click on **WINSERVER**.
   > - Click on Hyper-V settings.
   > - From there click on allow enhanced mode policy Under **Server** and enable the option.
   > - Again, click on allow enhanced mode under **User** and enable the option. Restart the WINSERVER machine once to reflect the changes.

   > **Note:** If the copy-paste function is still not working, first copy the required content. Then, in the top navigation pane of the WINSERVER Hyper-V VM, click on **Clipboard** and select **Type Clipboard Text** to paste it.

   > ![Picture 1](../Media/x0.png)

1. In the Search bar of the Azure portal, type **Azure Arc (1)**, then select **Azure Arc (2)**.

   ![](../Media/lab8-s25.png)

1. On the left side navigation pane under **Azure Arc resources** select **Machines (1)** and then click on **+ Onboard/Create (2)** drop dowm and then click on **Onboard existing machines (3)**.

   ![](../Media/lab8-s26.png)

1. First, select the **East US** region.

1. Then, create a new resource group by clicking on **Create New (1)** with the name **RG-DEFENDER (2)** then click **OK (3)**

   ![Picture 1](../Media/lab9-s6.png)

1. Review the **Server details** and **Connectivity method** options. Keep the default values and select **Next: Tags>** to get to the Tags tab.

   ![Picture 1](../Media/lab9-june26-p2t1p1.png)

1. Select **Next: Download and run script >** to get to the Download and run script tab.

1. Scroll down and select the **Download** button. **Hint:** If your browser blocks the download, take action in the browser to allow it.

   ![Picture 1](../Media/lab9-s8.png)

1. In Microsoft Edge Browser, select the ellipsis button (...) **(1)** if needed and then select **Keep (2)**.

   ![](../Media/lab8-s29.png)

1. Right-click the Windows Start **(1)** button and select **Windows PowerShell (Admin) (2)**.

   ![](../Media/lab8-s30.1.png)

1. In case you get a UAC prompt, enter **Administrator** for "Username" and **Passw0rd!** for "Password", else skip to the next step.

1. Enter the below command.

   ```CommandPrompt
   cd C:\Users\Administrator\Downloads
   ```

   > **Note:** If you are not able to copy the content, then copy the required content to a notepad file using the Clipboard functionality in the top navigation pane of the Hyper V VM in the lab VM and paste it into the Powershell window.

1. Enter the below command and press enter.

   ```CommandPrompt
   Set-ExecutionPolicy -ExecutionPolicy Unrestricted
   ```

1. Enter **A** for Yes to All and press enter.

   ![Picture 1](../Media/lab9-s9.png)

1. Type `.\OnboardingScript.ps1` and press enter.

   > **Important:** If you get the error **"The term .\OnboardingScript.ps1 is not recognized..."**, make sure you are doing the steps for Task 3 on the WINSERVER virtual machine. Another issue might be that the name of the file changed due to multiple downloads, search for **".\OnboardingScript (1).ps1"** or other file numbers in the running directory.

   ![](../Media/lab9-s10.png)

1. Enter **R** to Run once and press enter (this may take a couple of minutes).

   ![Picture 1](../Media/lab9-s11.png)

1. The setup process will open a new Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message "Authentication complete" and then go back to the Windows PowerShell window.

   ![](../Media/lab8-s33.png)

1. When the installation finishes,you will get a output like this in the powershell.

   ![Picture 1](../Media/lab9-s12.png)

1. Then go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Servers** page.

1. Select **Refresh** until **WIN-xxxxxxxxxxx** name appears.

   > **Note:** This could take a few minutes.

   > **Note:** **xxxxxxxxxxx** will be a random suffix of the **WIN-**, as demonstrated in the below image.

   ![Picture 1](../Media/lab9-s13.png)

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. Close the **Meet your improved security center** pop-up using **X**.

   ![](../Media/lab9-june26-p2t1p2.png)

1. In the left navigation pane, click **Show navigation (1)** to expand the menu if it is collapsed. Next, expand **Microsoft Sentinel (2)**, then expand **Content management (3)**, and select **Content hub (4)**.

   ![](../Media/lab9-june26-p2t1p3.png)

   > **Note:** If workspace is not connected, click on Connect workspace to connect.

1. On the **Content hub** page, search for **Windows Security Events (1)**, press **Enter** and select **Windows Security Events (2)** and click on **Install (3)**.

   ![Picture 1](../Media/lab9-s14.png)

   > **Note:** If the page does not appear after waiting for 5-10 minutes, sign out of the portal and sign back in. If the issue persists, open the same page in an InPrivate or Incognito browser window.

1. Once the installation is completed, go to the **Data connector (1)** page and refresh you should find **Windows Security Events via AMA**.

1. Select the **Windows Security Events via AMA (2)** connector and click on **Open connector page (3)** on the connector information blade.

   ![Picture 1](../Media/lab9-s16.png)

1. Scroll down and in the **Configuration** section, select the **+Create data collection rule**.

   ![Picture 1](../Media/lab9-s17.png)

1. Enter **WINSERVER (1)** for Rule Name, select **RG-DEFENDER (2)** for the resource group, and then select **Next: Resources (3)**.

   ![Picture 1](<../Media/lab9-s18(1).png>)

1. Expand the **Subscription (1)** and the **RG-DEFENDER (2)** (or the Resource Group you have created), then select **WIN-xxxx (3)**. Then select **Next: Collect (4)**.

   ![Picture 1](../Media/lab9-s19.png)

1. Then click **Next: Review + Create**.

   ![Picture 1](../Media/lab9-s20.png)

1. On the **Create data Collection Rule** page, Select **Create**.

1. Wait a few minutes and then select **Refresh (1)** to see the new data collection rule listed **(2)**.

   ![Picture 1](../Media/lab9-s21.png)

## Task 2: Persistence Attack with Registry Key Add

In this task, you will simulate a persistence attack by adding a registry key that ensures a program runs each time the system starts.

1. Click **Start (1)** on the **WINServer** Windows taskbar, select **Power (2)**, and then choose **Restart (3)**.

   ![Lab overview.](../Media/ss50.png)

   > **Note**: Choose **Others(Planned)** and then **Continue**.

   ![Lab overview.](../Media/l9e6-1.png)

1. Once the system restarts, log back into **WINServer** from the desktop.

   ![Picture 1](../Media/46.png)

1. If prompted, provide the Password `Password.1!!`.

   ![Picture 1](../Media/sc-200-4.png)

1. In the search of the task bar, enter **Command (1)**. Command Prompt will be displayed in the search results. Right-click on the Command Prompt and select **Run as Administrator (2)**. Select **Yes** in the User Account Control window that appears to allow the app to run.

   ![Lab overview.](../Media/ss51.png)

1. In the Command Prompt, create a Temp folder in the root directory. Remember to press Enter after the last row:

   ```CommandPrompt
   cd \
   mkdir temp
   cd temp
   ```

1. Copy and run this command to simulate program persistence:

   ```CommandPrompt
   REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
   ```

   ![Lab overview.](../Media/lab9-s77.png)

## Task 3: Privilege Elevation Attack with User Add

In this task, you will simulate a privilege elevation attack by creating a new admin user on the system. This exercise demonstrates how an attacker could escalate their privileges on a machine by adding a new user to the Administrators group.

1. Copy and run this command to simulate the creation of an Admin account. Remember to press Enter after the last row:

   ```CommandPrompt
   net user theusernametoadd /add
   net user theusernametoadd ThePassword1!
   net localgroup administrators theusernametoadd /add
   ```

   ![Lab overview.](../Media/lab9-s78.png)

   > **Note:** If you encounter any issues while copying and pasting, try copying the prompt into **Notepad** first, then paste it into the **Command Prompt (CMD)**.

## Task 4: Privilege Elevation Attack with User Add

In this task, you will simulate a DNS-based Command and Control (C2) attack by creating a PowerShell script. This simulated attack will continuously generate DNS queries to a C2 server.

1. Copy and run this command to create a script that will simulate a DNS query to a C2 server:

   ```CommandPrompt
   notepad c2.ps1
   ```

1. Select **Yes** to create a new file and copy the following PowerShell script into **c2.ps1**.

   ![Lab overview.](<../Media/lab9-s18(2).png>)

   > **Note:** When pasting into the virtual machine file, the full script length might not be visible. Ensure that the script matches the instructions in the **c2.ps1** file before proceeding.

   ```PowerShell
   param(
       [string]$Domain = "microsoft.com",
       [string]$Subdomain = "subdomain",
       [string]$Sub2domain = "sub2domain",
       [string]$Sub3domain = "sub3domain",
       [string]$QueryType = "TXT",
       [int]$C2Interval = 8,
       [int]$C2Jitter = 20,
       [int]$RunTime = 240
   )
   $RunStart = Get-Date
   $RunEnd = $RunStart.addminutes($RunTime)
   $x2 = 1
   $x3 = 1
   Do {
       $TimeNow = Get-Date
       Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
       if ($x2 -eq 3 )
       {
           Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
           $x2 = 1
       }
       else
       {
           $x2 = $x2 + 1
       }
       if ($x3 -eq 7 )
       {
           Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
           $x3 = 1
       }
       else
       {
           $x3 = $x3 + 1
       }
       $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
       Start-Sleep -Seconds $Jitter
   }
   Until ($TimeNow -ge $RunEnd)
   ```

1. In the Notepad menu, select **File (1)** and then **Save (2)**.

   ![Lab overview.](../Media/ss54.png)

1. Go back to the Command Prompt window, enter the following command and press Enter.

   > **Note:** You may encounter **DNS resolve errors**, which is expected behavior.

   ```CommandPrompt
   Start PowerShell.exe -file c2.ps1
   ```

   > **Important:** Keep these windows open and let the **PowerShell script** run in the background. The command needs to generate **log entries** for a few hours. You can continue with the next tasks and exercises while it runs. The data created here will be used later in the **Threat Hunting lab**. This process will not generate a significant amount of data or processing load.

## Review

- Connected a non-Azure Windows Machine
- Persistence Attack with Registry Key Add
- Command and Control Attack with DNS
- Privileged Elevation Attack with User Add

## PROCEED TO THE NEXT EXERCISE
