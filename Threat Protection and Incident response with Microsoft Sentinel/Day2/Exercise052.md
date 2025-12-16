# Lab: Hunt Threats Using KQL Across the Data Lake

**Scenario:** You are a Threat Hunter. You need to investigate a potential "Low and Slow" attack where recent indicators (Hot Data) need to be correlated with historical network traffic logs stored in long-term storage (Cold Data/Data Lake).

### Task 1: Explore the Data Lake Structure and Tables

In this task, you will explore the Microsoft Sentinel data lake structure to understand available data sources and tables for threat hunting.

1. Navigate to **Microsoft Defender Portal** 
    ```text
    https://security.microsoft.com/
    ```

1. On the left side menu, select **Microsoft Sentinel (1)** > **Configuration (2)** and select **Tables (3)** under Configuration. This view allows you to manage the schema and retention settings of your log data.

    ![Picture](./images1/Ex7-01.png)

1. On the **Tables** page, you will see a comprehensive list of tables available in your Sentinel workspace. Review available tables including *SecurityAlert*, *AzureActivity*, *SigninLogs*, and *Heartbeat*.

1. Navigate to 

1. Navigate to the **Logs (1)** section in the left menu under **General** to access the KQL query editor. This is your primary interface for hunting.

    ![Picture](./images1/Ex7-05.png)

1. Ensure you are in **KQL mode (1)** for writing queries. The query editor provides syntax highlighting and Intellisense.

    ![Picture](./images1/Ex7-06.png)

### Task 2: Verify Connectivity to the External Data Lake (ADX)

In this task, you will establish and verify the connection from Microsoft Sentinel to the external Azure Data Explorer (ADX) cluster using the `adx()` pattern.

1. Ensure you are still in the **Logs** blade within Microsoft Sentinel.

    ![Picture](./images1/Ex7-07.png)

1. In the query editor window, copy and paste the following query into the **editor (1)** to test connectivity. We are using Microsoft's public "Help" cluster to simulate your organization's Cold Data Lake.

    ```kusto
    // Connect to external ADX cluster (The "Cold" Store)
    adx("[https://help.kusto.windows.net/Samples](https://help.kusto.windows.net/Samples)").StormEvents
    | take 10
    ```

    ![Picture](./images1/Ex7-08.png)

1. Click the **Run (1)** button.

    ![Picture](./images1/Ex7-09.png)

1. Review the **Results (1)** pane. You should see a table containing columns like *StartTime*, *State*, and *EventType*. This confirms Sentinel can query the remote data without ingesting it.

    ![Picture](./images1/Ex7-10.png)

### Task 3: Execute a Cross-Platform Threat Hunt

In this task, you will perform the actual threat hunt by correlating "Hot" data (simulated recent alerts) with "Cold" data (historical logs) in a single query.

1. In the **Logs** query editor, clear any existing queries.

1. Copy and paste the following code. This query takes specific IPs (Hot Data) and searches for their activity over the last year in the Data Lake (Cold Data).

    ```kusto
    // Step 1: Define the Suspicious Actor (Simulated Hot Data)
    let SuspiciousIPs = datatable(IP:string)
    [
        "192.168.1.55", 
        "10.0.0.99"
    ];
    
    // Step 2: Hunt in the Data Lake (Cold Data)
    adx("[https://help.kusto.windows.net/Samples](https://help.kusto.windows.net/Samples)").StormEvents
    | where StartTime > ago(365d)
    | where EventType == "Flood"
    // Note: We are mapping 'State' to 'IP' to simulate a match for this lab environment
    | extend SimulatedIP = case(
        State == "TEXAS", "192.168.1.55",
        State == "FLORIDA", "10.0.0.99",
        "0.0.0.0"
    )
    | where SimulatedIP in (SuspiciousIPs)
    | project ColdEventTime=StartTime, EventType, Location=State, MatchedIP=SimulatedIP
    ```

    ![Picture](./images1/Ex7-11.png)

1. Click **Run (1)** to execute the cross-platform hunt.

    ![Picture](./images1/Ex7-12.png)

1. Analyze the **Results**. You will see rows pulled from the external Data Lake that match the IPs defined in your variable.

    ![Picture](./images1/Ex7-13.png)

### Task 4: Visualize Long-Term Attack Patterns

In this task, you will visualize the data returned from the Data Lake to identify baseline deviations over a 6-month period.

1. Clear the previous query in the **editor**.

1. Paste the following query to generate a time-series chart:

    ```kusto
    adx("[https://help.kusto.windows.net/Samples](https://help.kusto.windows.net/Samples)").StormEvents
    | where StartTime > ago(180d)
    | where EventType has "Wind"
    | summarize DailyCount = count() by bin(StartTime, 1d)
    | render timechart 
    ```

    ![Picture](./images1/Ex7-14.png)

1. Click **Run**.

1. Observe the **Chart (1)** tab in the results pane to view the traffic trends.

    ![Picture](./images1/Ex7-15.png)

1. Click on **Save (1)** > **Save as Query (2)** to store this hunting logic in your Sentinel workspace.

    ![Picture](./images1/Ex7-16.png)