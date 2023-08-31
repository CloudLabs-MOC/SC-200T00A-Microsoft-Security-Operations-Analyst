# Module 2 - Lab 1 - Exercise 2 - Mitigate Attacks with Microsoft Defender for Endpoint

## Lab scenario

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

To explore the Defender for Endpoint attack mitigation capabilities, you will run two simulated attacks.

>**Important:** Please wait until WIN1 appears in the Devices page before you continue. Otherwise, you might need to repeat this task to see the alerts that will be generated later.

## Lab objectives
 In this lab, you will perform the following:
- Run Simulated Attacks
- Investigate the Attacks

## Estimated time: 60 minutes

## Architecture Diagram

  ![Picture 1](../Media/SC200-Lab_Diagrams_Mod2_L1_Ex2.png)

### Task 1: Simulated Attacks

In this task, you will run two simulated attacks to explore the capabilities of Microsoft Defender for Endpoint.

1. If you are not already at the Microsoft 365 Defender portal in your Microsoft Edge browser, go to (https://security.microsoft.com). 

1. In the **Sign in** dialog box, copy and paste * Email/Username: <inject key="AzureAdUserEmail"></inject> and then select Next.

1. In the **Enter password** dialog box, copy and paste * Password: <inject key="AzureAdUserPassword"></inject> and then select **Sign in**.

1. From the menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button. 

1. After downloading the file,  open the file with **Microsoft word** and enter the password as `WDATP!diy#`.

1. In the Sign in dialog box, click on **Sign in** and copy and paste in the Username and password provided in the environment details page and select next.	

1. Click **Enable Editing** if the document opens inProtectedView. If you see a subsequent security warning about macros being disabled.	

1. To unblock the document, navigate to its location in File Explorer. In File Explorer, right-click the document, select Properties. In the General tab, mark the Unblock option under Security.	

   ![Picture 1](../Media/SC-200-img21.png)	

1. Close the **Microsoft word** and re-open from the File Explorer and enter the password as `WDATP!diy#` and after re-opening click on **Enable Content** and click on **OK**.	

1. In the Command prompt pop-up press any key to close.	
   
   
    >**Note:** **Congrats – you’re done running the attack!** The attack simulation ends here. A real attacker, if successful, would likely continue to scan for information, send collected reconnaissance information to a command-and-control (C&C) server, and use this information to move laterally and pursue other attractive targets.Next, let’s review and investigate the Defender for Endpoint alerts that surfaced the simulated attack. **Note:** Alerts should start to appear 15-30 minutes after the simulated backdoor is launched.	

1. Go back to the portal and in *Automated investigation (fileless attack)* click on **Copy simulation script**.

1. Right-click the Windows Start button and select **Windows PowerShell (Admin)**.	

    ![Picture 1](../Media/SC-200-module6-ex2-img5.png).	


1. At the Windows PowerShell, paste and run the provided script. A few seconds later, notepad.exe is started and the simulated attack code is injected into it. The simulated attack code attempts communication to an external IP address simulating the C&C server.

### Task 2: Investigate the Attacks

1. In the Microsoft 365 Defender portal select **Incidents & alerts** from the left menu bar, then select **Incidents**.

1. A new incident called "Multi-stage incident..." is in the right pane. Click the incident name to load its details.

1. Select the **Manage incident** button and a new window blade appears. 

1. Under **Incident tags** type "Tutorial" and select **Tutorial (Create new)** to create a new tag. 

1. Select the toggle **Assign to**  and add your user account (Me) as the owner of the incident. 

1. Under **Classification**, expand the drop-down menu. 

1. Under **Informational, expected activity**, select **Security testing**. 

1. Add any comments if desired and click **Save** to finish.

1. Review the contents of the Alerts, Devices, Users, Investigations, Evidence, Response, and Graph tabs. **Hint:** Some tabs might be hidden due to the size of your display. Select the ellipsis tab (...) to make them appear.

>**Warning:** The simulations and tutorials here are an excellent source of learning through practice.  Simulations and tutorials are being added and edited regularly in the portal.  However, some of these simulations & tutorials may interfere with the performance of the labs designed for this training course.  Only perform the simulations and tutorials recommended in the instructions provided for this lab when using the course provided Azure tenant.  You may perform the other simulations and tutorials *after* this training course is complete with this tenant.

   >**Congratulations** on completing the lab! Now, it's time to validate it. Here are the steps:
   > - Navigate to the Lab Validation tab, from the upper right corner in the lab guide section.
   > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

### Review
In this lab, you have completed the following:
- Ran Simulated Attacks
- Investigated the Attacks

## You have successfully completed the lab.
