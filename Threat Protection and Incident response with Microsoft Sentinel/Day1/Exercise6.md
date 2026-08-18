# Lab 06: Operationalizing with Data Lake - KQL Jobs, Table Tiering & the Sentinel MCP Server

## Estimated Duration: 30 Minutes

## Overview

In this lab, you will operationalize Microsoft Sentinel's Data Lake capabilities to manage large-scale security telemetry efficiently. You will learn how to run asynchronous KQL jobs against the Microsoft Sentinel Data Lake to query data that spans beyond the interactive query window. You will then configure table tiering - moving data between the Analytics, Basic, and Auxiliary tiers - to optimize both query performance and long-term storage costs.

Finally, you will connect to and explore the **Microsoft Sentinel MCP (Model Context Protocol) server**, which exposes Sentinel's core capabilities - such as incident management, KQL execution, and threat intelligence - as tools consumable by AI agents and copilot experiences. By the end of this lab, you will have a solid understanding of how to architect a cost-effective, AI-ready security data platform on top of Microsoft Sentinel.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Configure Table Tiering in Microsoft Sentinel
- Task 2: Explore the Sentinel MCP Server

### Task 1: Configure Table Tiering in Microsoft Sentinel

In this task, you will configure table tiering in Microsoft Sentinel to optimize storage costs while maintaining query access across different time horizons. Microsoft Sentinel supports three table tiers:

1. Navigate back to the Azure portal and search for Log Analytics workspaces.

    ![](images/sentinel1.png)

1. Select **uniquenameSentinel**, navigate to **Settings** from the left hand pane, select **Tables (1)**.On the **Tables** page, you will see a list of all tables in your workspace. Use the search bar to locate the **SigninLogs (2)** table, then click the **ellipsis (…)** menu on its row and select **Manage table (3)**.

    >**Note:** It may take up to **30-50 minutes** for the SigninLogs table to appear. In the meantime, you can proceed with the next task. After some time, return to this step, refresh the page, and check again.

    ![](images/sentinel15.png)

1. In the **Manage table** blade, review the current settings:

    - **Table plan (1):** Observe that it is currently set to **Analytics**
    - **Analytics retention (2):** Note the current value (default: 30 days)
    - **Total retention (3):** Note the current value (default: 30 days)

    ![](images/l4t2s4.png)

1. Change the **Table plan (1)** to **Basic** using the dropdown. Observe that the interactive retention is now limited to **30 days** while the total retention period can extend up to **12 years (2)**.

    ![](images/l4t2s5.png)

    >**Note:** The **Basic** tier is well suited for high-volume, verbose logs (e.g., network flow logs, firewall logs) that are ingested in large quantities but queried infrequently for threat hunting or compliance purposes. Basic logs support limited KQL operations - cross-table joins (`join`, `find`, `search`) are not supported.

1. Adjust the **Total retention** period to **1 year (1)**, then click **Save (2)**.

    ![](images/l4t2s6.png)

    >**Note:** It may take a few minutes for the table plan change to take effect. The table will continue to serve interactive queries during this transition.

1. Return to the **Tables** page and locate the **AzureActivity (1)** table. Click the **ellipsis (…) (2)** menu and select **Manage table (3)** to explore its settings.

    ![](images/sentinel10.png)

1. In the **Manage table** blade for **AzureActivity**, look at the **Table plan** field. Note that it is displayed as **Analytics** but is grayed out and not editable from this blade.

      ![](images/sentinel11.png)

    > **Note:** This is expected behavior. The **Table plan** field is disabled for the **AzureActivity** table because it's a built-in connector table, not a custom table — plan selection (including the **Auxiliary**/Data Lake tier) is only configurable at creation time for custom tables via API or CLI. For built-in tables like **AzureActivity**, the plan is fixed to **Analytics**, and cost optimization instead comes from adjusting **Data retention settings** (Analytics retention / Total retention) below, or using **Basic** plan tables for other custom log sources.

### Task 2: Explore the Sentinel MCP Server

In this task, you will connect to and explore the **Microsoft Sentinel MCP (Model Context Protocol) server**. The Sentinel MCP server exposes Sentinel's core capabilities - such as querying the data lake, triaging incidents, and hunting for threats - as structured tools consumable by AI agents and developer toolchains. Microsoft provides three pre-built tool collections, each accessible via a fixed hosted endpoint URL.

**MCP Tool Collections and Endpoints:**

| Collection | Endpoint URL | Purpose |
|---|---|---|
| **Data Exploration** | `https://sentinel.microsoft.com/mcp/data-exploration` | Search tables, retrieve logs, analyze entities |
| **Triage** | `https://sentinel.microsoft.com/mcp/triage` | Incident triage and threat hunting |
| **Security Copilot Agent Creation** | `https://sentinel.microsoft.com/mcp/security-copilot-agent-creation` | Build and customize security agents |

>**Note:** Most MCP tools require onboarding to the **Microsoft Sentinel data lake**. You need at minimum the **Security Reader** role to invoke Sentinel's MCP tool collections.

1. From the Desktop, open **Visual Studio Code**.

    ![](images/sentinel12.png)

1. On the Welcome to VS Code pop-up, click on **Continue without Signing In**.

    ![](images/l4t3s1.png)

1. Open the **Command Palette** using `Ctrl + Shift + P` on Windows, then search for and select **MCP: Add Server… (1)**.

    ![](images/l4t3s2.png)

1. When prompted to select the connection type, choose **HTTP (1)** (Server-Sent Events/SSE).

    ![](images/l4t3s3.png)

1. In the **Server URL** field, enter the **Triage** endpoint:

    ```
    https://sentinel.microsoft.com/mcp/triage
    ```

    Press **Enter** to confirm.

    ![](images/l4t3s4.png)

1. Accept the default **Server ID**, click on **enter**.

    ![](images/l4t3s4b.png)

1. When prompted to authorize the connection, click **Allow (1)**. Visual Studio Code will launch a browser window for **Microsoft Entra ID authentication**. Sign in with your lab credentials.

    ![](images/l4t3s5.png)

1. On the pop-up, select the **Work or school account (1)** and click on **Continue (2)**.

    ![](images/sentinel13.png)

1. Once authenticated, VS Code will confirm the MCP server connection. You will see the **Microsoft Sentinel Data Exploration** tools listed in the VS Code Chat panel under **Tools (1)**.

    ![](images/l4t3s6.png)

    ![](images/l4t3s6c.png)

1. Here, you can verify that the server is running.

    ![](images/l4t3s6b.png)

    >**Note:** The available tools include capabilities to search tables, retrieve security logs, analyze user entities, identify risky devices, and explore URLs - all using natural language prompts that are translated to KQL internally.

1. In the VS Code Chat panel, select **Agent mode (1)** (the `@` icon or model dropdown) and type the following natural language prompt:

    ```
    Analyze all user sign-in activity from the SigninLogs in the last 24 hours and state the exact time range used. Break it down by user, source IP/location, application, and device/client, and flag anything unusual — sign-ins from new or unexpected locations, impossible-travel cases, off-hours activity, or privileged/admin accounts. Start with a short ranked summary of key findings, then supporting detail, and say so explicitly if nothing notable appears.
    ```

    ![](images/l4t3s7.png)

    > **Note:** You will see a pop-up to login to GitHub. Use your **personal GitHub credentials** to login.

      ![](images/l4t3s7b.png)

1. Click on **Allow** as and when prompted.

1. Review the response. Observe how the MCP server translates your natural language prompt into a KQL query, executes it against the Sentinel data lake, and returns a structured summary of sign-in failure patterns - without requiring you to write any KQL manually.

    ![](images/l4t3s8.png)

1. Try a second prompt to demonstrate multi-step agentic reasoning across the security data lake:

    ```
    Find the user that is at risk and explain why they are at risk.
    ```

    ![](images/l4t3s9.png)

    >**Note:** The Sentinel MCP server enables AI agents to act on live Sentinel data - performing triage, retrieving indicators, and analyzing entities - using any MCP-compatible client including VS Code, Microsoft Copilot Studio, or Microsoft Foundry. This represents the next evolution of AI-assisted security operations.

## Summary

In this lab, you have completed the following:

- Configured **table tiering** by migrating tables from the Analytics tier to Basic and Auxiliary tiers to optimize query costs and long-term retention
- Connected to the **Microsoft Sentinel MCP server** and integrated it with Microsoft Copilot for Security to enable AI-driven, natural-language access to live Sentinel incidents, KQL execution, and threat intelligence

## You have successfully completed the lab!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](images/Next.png)
