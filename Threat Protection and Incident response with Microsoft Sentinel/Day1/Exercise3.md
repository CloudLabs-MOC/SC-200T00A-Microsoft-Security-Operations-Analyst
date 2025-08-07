# Exercise 3: Threat Intelligence connector and Content Hub

## Estimated Duration: 20 Minutes

## Lab Scenario


## Lab Objectives
 In this lab, you will perform the following:

- Task 1: Connect the Threat Intelligence connector
- Task 2: Create a Threat Indicator


### Task 1: Connect the Threat Intelligence connector from content hub

1. In the Azure portal search bar, type **Microsoft Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](./images/Ex1-05.png)

1. Select the **Microsoft Sentinel Workspace** you created earlier.

   ![](./images/Ex4-00.png)

1. In Microsoft Sentinel, on the left menu, select the **Content hub (1)** option under Content management, and you will find a **Click here to go to the Defender portal (2)** link, click on it to navigate to the **Defender portal**.

   ![](./images/Ex3-04.png)

1. On Defender portal, Content hub page will open, in search bar type **Threat intelligence (1)**, select **Threat intelligence (2)** from the list, then click on **Install (3)**. 

1. Expand **Threat intelligence (1)** data connector and click on it, then select the **Open connector page (2)** on the connector information blade.

### Task 2: Create a Threat Indicator

In this task, you will create an indicator in Microsoft Sentinel.

1. Navigate to Defender Portal, expand **Threat intelligence (1)** from the left hand menu and select **Intel management (2)**. 

1. On **Intel management** page, click on **+ New (3)** under Indicator, then select **TI object (4)**.

   ![](./images/Ex3-00.png)

1. Review the different indicator types available in the ***Types*** dropdown. Select the **domain-name**. Enter your initials in the Domain box. You can use **onmicrosoft.com**.
1. On **New TI objects** pane, enter the following details:

    - **Object type:** Select **Indicator (1)** from the dropdown menu.

    - Click on **+ New observable (2)**, select **Domain name** from the drop down.

    - **Domain name value:** Enter **onmicrosoft.com (3)**.

    - **Name:** provide **Indicator-test (4)**.

    - **Indicator types:** Select **Malicious activity (5)** from the dropdown menu.

    - **Valid from:** Keep **today's date (6)**.

    - **Valid untill:** Keep date of **next day (7)**.

    - **Source:** Should be **Microsoft Sentinel (8)**.

    - Then click on **Add (9)**.

      ![](./images/Ex3-01.png)

      **Note:** It could take a couple of minutes for the indicator to appear.

1. In the Azure portal search bar, type **Microsoft Sentinel (1)**, then select **Microsoft Sentinel (2)**.

   ![](./images/Ex1-05.png)

1. Select the **Microsoft Sentinel Workspace** you created earlier.

   ![](./images/Ex4-00.png)

1. Select the **Logs (1)** option under **General** on the left hand menu. 

   >**Note:** You may need to disable the "Always show queries" option and close the *Queries* window to run the statements.

1. Choose working mode as **KQL mode (2)**, enter the below given query **(3)**, then click **Run (4)** and in **Results (5)** section see the output of the query.  

    ```KQL
    ThreatIntelligenceIndicator
    ```
    ![](./images/Ex3-02.png)
    
    >**Note:** You may need to wait for 20 minutes to get the expected output.

1. Keep the working mode as **KQL mode (1)**, enter the below given query **(2)** to see the DomainName column, then click **Run (3)** and in **Results (5)** section you should now, see the **DomainName column with onmicrosoft.com domain** as an output of the query. 

    ```KQL
    ThreatIntelligenceIndicator
    | project DomainName
    ```
   ![](./images/Ex3-03.png)





   
