# Lab 09 - Exercise 6: Create Detections

## Lab Scenario

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You are going to work with Log Analytics KQL queries and from there, you will create custom analytics rules to help discover threats and anomalous behaviors in your environment.

Analytics rules search for specific events or sets of events across your environment, alert you when certain event thresholds or conditions are reached, generate incidents for your SOC to triage and investigate, and respond to threats with automated tracking and reMediation processes.

>**Important:** The lab exercises for Learning Path #9 are in a **standalone** environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

## Lab Objectives
 In this lab, you will Understand following:
- Task 1: Persistence Attack Detection
- Task 2: Privilege Elevation Attack Detection

## Estimated Timing: 30 Minutes

## Architecture Diagram

  ![Lab overview.](../Media/sc200ex7upd.png)

### Task 1: Persistence Attack Detection

>**Important:** The next steps are done on a different machine than the one you were previously working on. Look for the Virtual Machine name references.

In this task, you will create a detection for the first attack of the previous exercise.

1. On a new tab in the browser, go to **https://security.microsoft.com**

1. In the **Microsoft Defender** portal, expand **Investigation & response (1)**, expand **Hunting (2)**, and then select **Advanced hunting (3)**.

    ![Picture 1](../Media/lab9-ex7-1.png)

1. Close the **Introducing Copilot Threat Hunting Agent** pop-up window.

    ![Lab overview.](../Media/lab9-june26-p2t1p21.png)

1. Provide the following KQL Statement again to recall the tables where we have this data **(1)**:

    ```KQL
    search "temp\\startup.bat"
    ```    

1. **Run query(2)** the query, result with the event might take up to **5-10 minutes** to appear **(3)**.

   ![Picture 1](../Media/lab9-ex7-2.png)

1. The table *SecurityEvent* looks to have the data already normalized and easy for us to query. Expand the row to see all the columns related to the record.

1. From the results, we now know that the Threat Actor is using reg.exe to add keys to the Registry key and the program is located in C:\temp. **Run** the following statement to replace the *search* operator with the *where* operator in our query:

    ```KQL
    SecurityEvent 
    | where Activity startswith "4688" 
    | where Process == "reg.exe" 
    | where CommandLine startswith "REG" 
    ```

1. It is important to help the Security Operations Center Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph. **Run query** the following query:

    ```KQL
    SecurityEvent 
    | where Activity startswith "4688" 
    | where Process == "reg.exe" 
    | where CommandLine startswith "REG" 
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = SubjectUserName
    ```

     ![Picture 1](../Media/lab9-ex7-3.png)    

1. In **Advanced hunting**, select a result **(1)**, choose **Create detection rule (2)**, and then select **Create analytics rule instead** to continue with the unified experience.

   ![Picture 1](../Media/lab9-june26-p2t1p23.png) 

   ![Picture 1](../Media/lab9-june26-p2t1p24.png) 

1. This starts the "Analytics rule wizard". For the **General** tab type:

    |Setting|Value|
    |---|---|
    |Name|**Startup RegKey (1)**|
    |Description|**Startup RegKey in c:\temp (2)**|
    |Severity|**High (3)**|
    |MITRE ATT&CK|**Persistence (4)**|
 
1. Select **Next: Set rule logic > (5)** button.

   ![Picture 1](../Media/lab9-ex7-6.png) 

1. On the **Set rule logic** tab, the **Rule query** should be populated already with you KQL query, as well as the entities under **Alert enrichment - Entity mapping (1)**, click on **+ Add new entity (2)**. Add it manually with the below details.

    |Entity|Identifier|Data Field|
    |:----|:----|:----|
    |Host|Hostname|HostCustomEntity|

    ![Picture 1](../Media/lab9-ex7-7.png)  

    ![Picture 1](../Media/lab9-june26-p2t1p27.png) 

1. In the *Custom details* section, enter a key-value pair as follows:

    |Key|Parameter|
    |:----|:----|
    |Activity|EventID|

    ![Picture 1](../Media/lab9-june26-p2t1p28.png)

    ![Picture 1](../Media/lab9-june26-p2t1p29.png) 

1. On the *Alert settings* page, in the *Alert details* section, enter the following:
    
    |Setting|Value|
    |---|---|
    |Alert title|**Alert from {{Computer}}**|
    |Description|**Alert from {{Process}} at {{TimeGenerated}}**|

    ![Picture 1](../Media/lab9-june26-p2t1p30.png) 
 
1. For **Query scheduling** set the following:

    |Setting|Value|
    |---|---|
    |Run Query every|5 minutes|
    |Lookup data from the last|1 Days|

    >**Note:** We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

    ![Picture 1](../Media/lab9-june26-p2t1p31.png) 

1. Leave the rest of the options with the defaults. Select **Next: Incident settings >** button.

1. For the **Incident settings** tab, leave the default values and select **Next: Automated response >** button.

1. On the **Automated response** tab under **Automation rules**, select **+ Add new**.

   ![Picture 1](../Media/lab9-ex7-10.png) 

    >**Note:** If you are unable to add a new Automation Rule, follow these steps:  
    > 1. Open a new tab and navigate to your **Sentinel workspace**.  
    > 2. Go to the **Automation** section and click on **+ Create**, then select **Automation Rule**.  
    > 3. Enter the required details as specified from Step 14 to Step 15.  
    > 4. Once completed, return to the previously open page and click **Refresh**.
    > 5. Now fill the details again from Step 7.  
    > 5. You should now see the newly created Automation Rule under **Automated Response**.

1. Use the settings in the table to configure the automation rule and then click on **Apply (5)**:

    |Setting|Value|
    |:----|:----|
    |Automation rule name|Startup RegKey **(1)**|
    |Trigger|When incident is created **(2)**|
    |Actions |Run playbook **(3)**|
    |playbook |Defender_XDR_Ransomware_Playbook_for_SecOps-Tasks **(4)**|

    ![Picture 1](../Media/lab9-ex7-11.png) 

     >**Note:** You have already assigned permissions to the playbook, so it will be available.

1. Select the **Next: Review + Create >** button.
  
1. On the **Review and create** tab, select the **Save** button to create the new Scheduled Analytics rule.

     ![Picture 1](../Media/lab9-ex7-12.png) 

### Task 2: Privilege Elevation Attack Detection

In this task, you will create a detection for the second attack of the previous exercise.

1. In the Defender portal, select **Advanced hunting** from the Hunting section in case you navigated away from this page.

1. **Run** the following KQL Statement to identify any entry that refers to administrators:

    ```KQL
    search "administrators" 
    | summarize count() by $table
    ```

    ![Picture 1](../Media/lab9-june26-p2t1p32.png) 

1. The result might show events from different tables.

   ![Picture 1](../Media/lab9-ex7-13.png)

1. But in our case, we want to investigate the SecurityEvent table. The EventID and Event that we are looking is **4732 - A member was added to a security-enabled local group**. With this, we will identify adding a member to a privileged group. **Run** the following KQL query to confirm:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

    ![Picture 1](../Media/lab9-ex7-14.png)   

1. Expand the row to see all the columns related to the record. The username of the account added as Administrator does not show. The issue is that instead of storing the username, we have the Security IDentifier (SID). **Run** the following KQL to match the SID to the username that was added to the Administrators group:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    ```

    ![Picture 1](../Media/lab9-ex7-15.png) 

1. Extend the row to show the resulting columns, in the last one, we see the name of the added user under the **UserName1** column we **project** within the KQL query. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph. **Run** the following query:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName1
    ```
    ![Picture 1](../Media/lab9-ex7-16.png)  

1. In **Advanced hunting**, select a result **(1)**, choose **Create detection rule (2)**, and then select **Create analytics rule instead** to continue with the unified experience.

   ![Picture 1](../Media/lab9-june26-p2t1p33.png)

   ![Picture 1](../Media/lab9-ex7-5.png)

1. This starts the "Analytics rule wizard". For the **General** tab type provide the following details:

    |Setting|Value|
    |---|---|
    |Name|**SecurityEvent Local Administrators User Add (1)**|
    |Description|**User added to Local Administrators group (2)**|
    |Severity|**High (3)**|
    |MITRE ATT&CK|**Privilege Escalation (4)**|

    ![Picture 1](../Media/lab9-ex7-18.png)   

1. Then select **Next: Set rule logic > (5)** button.

1. On the **Set rule logic** tab, the **Rule query** should be populated already with you KQL query, as well the entities under **Alert enhancement - Entity mapping** If not add it manually by selecting **+ Add new entity**:

    |Entity|Identifier|Data Field|
    |:----|:----|:----|
    |Account|FullName|AccountCustomEntity|
    |Host|Hostname|HostCustomEntity|

    ![Picture 1](../Media/lab9-ex7-19.png)   

1. For **Query scheduling** set the following:

    |Setting|Value|
    |---|---|
    |Run Query every|5 minutes **(1)**|
    |Lookup data from the last|1 Days **(2)**|

    ![Picture 1](../Media/lab9-ex7-20.png) 

    >**Note:** We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select **Next: Incident settings > (3)** button.

1. For the **Incident settings** tab, leave the default values and select **Next: Automated response >** button.

1. On the **Automated response** tab under **Automation rules**, select **+ Add new**.

    >**Note:** If you are unable to add a new Automation Rule, follow these steps:  
    > 1. Open a new tab and navigate to your **Sentinel workspace**.  
    > 2. Go to the **Automation** section and click on **+ Create**, then select **Automation Rule**.  
    > 3. Enter the required details as specified from Step 14 to Step 15.  
    > 4. Once completed, return to the previously open page and click **Refresh**.
    > 5. Now fill the details again from Step 7.  
    > 5. You should now see the newly created Automation Rule under **Automated Response**.

1. Use the settings in the table to configure the automation rule and the click **Apply (5)**:

   |Setting|Value|
   |:----|:----|
   |Automation rule name|SecurityEvent Local Administrators User Add **(1)**|
   |Trigger|When incident is created **(2)**|
   |Actions |Run playbook **(3)**|
   |playbook |Defender_XDR_Ransomware_Playbook_for_SecOps-Tasks **(4)**|

   ![Picture 1](../Media/lab9-ex7-21.png) 

    >**Note:** You have already assigned permissions to the playbook, so it will be available.

1. Select the **Next: Review and create >** button.
  
1. On the **Review and create** tab, select the **Save** button to create the new Scheduled Analytics rule.

## Review
In this lab, you have completed the following:
- Persistence Attack Detection
- Privileged Elevation Attack Detection

## Select **Next** to continue to Exercise 7
