# Exercise 5: Advanced Threat Hunting with Jupyter Notebooks in Microsoft Sentinel

## Estimated Duration: 90 Minutes

## Overview

In this comprehensive lab exercise, you will leverage **Jupyter notebooks** integrated with **Microsoft Sentinel** and the **MSTICPy Python library** to conduct advanced threat hunting. Jupyter notebooks provide a flexible, interactive environment for security analysis, combining **Kusto Query Language (KQL)** queries, Python data processing, and sophisticated visualizations. You will configure a complete notebook environment, establish secure connections to your Sentinel workspace, perform advanced data analysis using MSTICPy's threat hunting capabilities, and create reusable workflows for ongoing security investigations. By completing this exercise, you will develop powerful, reproducible threat hunting workflows that your security team can leverage for continuous incident investigation and proactive threat detection.

## Lab Objectives

By completing this lab, you will:

= Task 1: Access and Configure Jupyter Notebooks in Microsoft Sentinel
- Task 2: Create and Configure Your First Notebook
- Task 3: Initialize MSTICPy and Connect to Sentinel Workspace
- Task 4: Perform Advanced Threat Hunting Queries
- Task 5: Create Visualizations
- Task 6: Perform Anomaly Detection

## Task 1: Access and Configure Jupyter Notebooks in Microsoft Sentinel

1. Open your web browser and navigate to **Microsoft Defender Portal**:
   ```
   https://security.microsoft.com/
   ```

1. In the left sidebar, locate **Microsoft Sentinel** section

    ![Picture](./images1/Ex08-01.png)

1. Click on **Microsoft Sentinel** to expand menu options
1. Under **Threat management**, select **Notebooks**

**Note**: The UI path shown in your screenshot indicates:
- Path: Microsoft Sentinel > Content Management > Notebooks (in Threat Management)
- Alternative path: Some portals may show: Microsoft Sentinel > Threat Management > Notebooks

#### Verify Notebook Templates

1. You should see a page showing "25 Notebook templates"
2. Review the available templates including:
   - "A Getting Started Guide For Microsoft Sentinel ML Notebooks" (recommended for first-time users)
   - "Guided Investigation - Process Alerts"
   - "Credential Scan on Azure Log Analytics"

**If templates don't appear**:
- Verify you have Microsoft Sentinel Reader role
- Check that an Azure ML workspace is linked to your Sentinel workspace
- Try refreshing the page or clearing browser cache

#### Create Azure Machine Learning Workspace

If this is your first time setting up notebooks:

1. Click on **Configure Azure Machine Learning** button

1. Select **Create a new ML workspace**

1. Fill in the following details:
   - **Workspace name**: `sentinel-threatunting-ws` (or your preferred name)
   - **Subscription**: Select your Azure subscription
   - **Resource group**: Create new or select existing
   - **Region**: Same region as your Sentinel workspace (important for performance)
   - **Storage account**: Auto-created or select existing
   - **Key vault**: Auto-created
   - **Application Insights**: Auto-created

4. Click **Create** and wait 3-5 minutes for the workspace to provision

#### Create or Select Compute Instance

1. Once the AML workspace is created/linked, navigate to the AML workspace
2. Select **Compute** > **Compute instances**
3. Click **+ New** to create a compute instance:
   - **Name**: `sentinelnotebook-compute`
   - **Compute type**: Compute instance
   - **VM size**: Standard_DS2_v2 (or larger for production)
   - **Enable idle shutdown**: Toggle ON
   - **Idle shutdown time**: 30 minutes

4. Click **Create** and wait for the compute instance to start (5-10 minutes)

**Cost Optimization Tip**: Stop compute instances when not in use to prevent unnecessary charges.

## Task 2: Create and Configure Your First Notebook

#### Create a New Notebook from Template

1. In the Notebooks section, click on **Templates** tab
2. Search for or select: **"A Getting Started Guide For Microsoft Sentinel ML Notebooks"**
3. Click **Create from template**

#### Configure Notebook Details

In the dialog that appears, enter:

| Field | Value |
|||
| **Notebook name** | `Threat Hunting Analysis Lab` |
| **Description** | `Advanced threat hunting using Python and MSTICPy with KQL integration` |
| **Kernel** | Python 3.8 (or higher available) |
| **ML workspace** | Select your linked Azure ML workspace |
| **Compute** | Select your compute instance created in Step 1.5 |

#### Save and Launch Notebook

1. Click **Save** to save the notebook to your ML workspace
2. Wait for the notebook to be created and provisioned (1-2 minutes)
3. Click **Launch notebook** to open in Jupyter environment

**Expected UI Changes (December 2025 Update)**:
- The notebook launches in a web-based Jupyter interface
- Left sidebar shows file explorer and kernel information
- Top toolbar displays Kernel status, Run buttons, and Save options
- Markdown cells display formatted text and instructions
- Code cells show syntax highlighting for Python code

#### Verify Notebook Environment

1. Check the kernel indicator in the top-right (should show "Python 3.8" or higher)
2. Verify you see:
   - Cell selector area
   - Markdown cells with instructions
   - Code cells ready for execution

**If notebook fails to load**:
- Ensure compute instance is running: Check **Compute** > **Compute instances**
- Verify kernel is started: See Step 2.1 instructions for starting a kernel
- Clear browser cache and try again
- Check for service health: https://status.azure.com

## Task 3: Initialize MSTICPy and Connect to Sentinel Workspace

#### Import Required Libraries

In a code cell, add and run the following code:

```python
# Import required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime, timedelta
import warnings
warnings.filterwarnings('ignore')

# Import MSTICPy components
import msticpy as mp
from msticpy.nbtools import *
from msticpy.nbtools import nbdisplay
from msticpy.analysis import anomalies

print(f"MSTICPy version: {mp.__version__}")
print(f"Pandas version: {pd.__version__}")
print(f"NumPy version: {np.__version__}")
print("✓ All libraries imported successfully")
```

**Expected Output**: Version numbers and success message

#### Initialize Notebook Environment

Add and run the following code:

```python
# Initialize the notebook environment
mp.init_notebook(
    namespace=globals(),
    extra_imports=['msticpy.analysis.anomalies', 'msticpy.analysis.clustering']
)

print("✓ Notebook environment initialized")
print("✓ MSTICPy configuration loaded")
```

**Expected Output**: 
- Configuration loading messages
- Success indicators
- Warnings about missing configuration are normal on first run

#### Configure MSTICPy Settings (First Time Only)

Run this code to launch the configuration editor:

```python
from msticpy.config import MpConfigEdit
import os
from pathlib import Path

# Check for existing configuration file
mp_conf = "msticpyconfig.yaml"
mp_env = os.environ.get("MSTICPYCONFIG")
mp_conf = mp_env if mp_env and Path(mp_env).is_file() else mp_conf

# Launch configuration editor
if not Path(mp_conf).is_file():
    print("Creating new configuration. Please fill in your Sentinel workspace details...")
    mp.config.mp_settings_editor.MpConfigEdit(
        settings_path=mp_conf
    )
else:
    print("Loading existing configuration...")
    mpedit = mp.config.MpConfigEdit(mp_conf)
    mpedit.set_tab("AzureSentinel")
    display(mpedit)
```

**Configuration Setup Steps**:

1. In the **AzureSentinel** tab, enter:
   - **Workspace name**: Your Sentinel workspace name
   - **Workspace ID**: Your workspace ID (found in Sentinel > Settings > Workspace settings)
   - **Tenant ID**: Your Azure AD tenant ID

2. Click **Save Settings** and close the editor

#### Establish Connection to Sentinel Workspace

Add and run the following code:

```python
# Create QueryProvider for Azure Sentinel
from msticpy.data import QueryProvider
from datetime import datetime, timedelta

# Initialize QueryProvider for Azure Sentinel
qry_prov = mp.QueryProvider(data_environment="LogAnalytics")

# Connect to Sentinel workspace
print("Connecting to Microsoft Sentinel workspace...")

# This will prompt for authentication on first run
qry_prov.connect()

print("✓ Successfully connected to Sentinel workspace")
print(f"✓ Available query sources: {list(qry_prov.data_sources.keys())}")
```

**Authentication Flow**:
- You will be prompted to authenticate
- A device code will be provided
- Follow the link to authenticate using your organizational account
- Return to the notebook once authenticated

**If authentication fails**:
- Check your LogAnalytics Reader role on the workspace
- Verify Workspace ID and Tenant ID are correct
- Try restarting the kernel: Kernel > Restart

#### Verify Connection with Test Query

Run this code to verify your connection works:

```python
# Test connection with a simple query
test_query = """
SecurityAlert
| where TimeGenerated > ago(7d)
| summarize AlertCount=count() by AlertName
| top 10 by AlertCount
"""

print("Running test query...")
try:
    test_results = qry_prov.exec_query(test_query)
    print(f"✓ Connection verified! Retrieved {len(test_results)} alert types")
    display(test_results)
except Exception as e:
    print(f"✗ Connection failed: {str(e)}")
    print("Please verify workspace ID and authentication")
```

**Expected Output**: Table showing top 10 alert types from your Sentinel workspace

## Task 4: Perform Advanced Threat Hunting Queries

#### Query High-Severity Security Alerts (Last 7 Days)

Add and run the following code:

```python
# Query high-severity security alerts
from datetime import datetime, timedelta

print("Querying high-severity security alerts...")

alert_query = """
SecurityAlert
| where TimeGenerated > ago(7d)
| where AlertSeverity in ("Medium", "High")
| summarize Count=count(), LastAlert=max(TimeGenerated) by AlertName, AlertSeverity
| sort by Count desc
"""

alerts_df = qry_prov.exec_query(alert_query)

print(f"✓ Retrieved {len(alerts_df)} distinct alert types")
display(alerts_df)

# Store for later use
globals()['alerts_df'] = alerts_df
```

#### Query Failed Authentication Events

Add and run the following code:

```python
# Query failed authentication attempts
print("Querying failed authentication events...")

failed_auth_query = """
SigninLogs
| where TimeGenerated > ago(7d)
| where ResultType !in ("0", "50125", "50140")
| summarize FailureCount=count(), LastAttempt=max(TimeGenerated) by UserPrincipalName, IPAddress
| where FailureCount > 3
| sort by FailureCount desc
| take 20
"""

try:
    failed_auth_df = qry_prov.exec_query(failed_auth_query)
    print(f"✓ Retrieved {len(failed_auth_df)} users with suspicious failed logins")
    display(failed_auth_df)
    globals()['failed_auth_df'] = failed_auth_df
except Exception as e:
    print(f"Note: SigninLogs may not be available. Error: {str(e)}")
    print("This is normal if Azure AD connector is not enabled")
```

## Task 5: Create Visualizations

#### Alert Distribution by Severity

Add and run the following code:

```python
# Create alert distribution visualization
print("Creating alert distribution visualization...")

alert_severity_query = """
SecurityAlert
| where TimeGenerated > ago(7d)
| summarize AlertCount=count() by AlertSeverity
"""

severity_df = qry_prov.exec_query(alert_severity_query)

# Create visualization
fig, ax = plt.subplots(figsize=(10, 6))
colors = {'High': '#d32f2f', 'Medium': '#ffa500', 'Low': '#4caf50'}
color_list = [colors.get(severity, '#9e9e9e') for severity in severity_df['AlertSeverity']]

severity_df.plot(
    x='AlertSeverity',
    y='AlertCount',
    kind='bar',
    ax=ax,
    color=color_list,
    legend=False
)

ax.set_title('Alert Distribution by Severity (Last 7 Days)', fontsize=14, fontweight='bold')
ax.set_xlabel('Alert Severity', fontsize=12)
ax.set_ylabel('Alert Count', fontsize=12)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

print("✓ Visualization created successfully")
```

#### Timeline of High-Severity Alerts

Add and run the following code:

```python
# Create timeline visualization
print("Creating alert timeline...")

timeline_query = """
SecurityAlert
| where TimeGenerated > ago(7d)
| where AlertSeverity == "High"
| summarize AlertCount=count() by bin(TimeGenerated, 1h)
| sort by TimeGenerated asc
"""

timeline_df = qry_prov.exec_query(timeline_query)

# Create timeline visualization
fig, ax = plt.subplots(figsize=(14, 6))
ax.plot(timeline_df['TimeGenerated'], timeline_df['AlertCount'], 
        marker='o', linewidth=2, markersize=6, color='#d32f2f')

ax.fill_between(timeline_df['TimeGenerated'], timeline_df['AlertCount'], 
                 alpha=0.3, color='#d32f2f')

ax.set_title('High-Severity Alert Timeline (Last 7 Days)', fontsize=14, fontweight='bold')
ax.set_xlabel('Time', fontsize=12)
ax.set_ylabel('Alert Count per Hour', fontsize=12)
plt.xticks(rotation=45)
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

print("✓ Timeline visualization created")
```

## Task 6: Perform Anomaly Detection

#### Set Up Time Series Analysis

Add and run the following code:

```python
# Setup time series analysis for anomaly detection
print("Setting up time series analysis...")

# Query logon events for time series analysis
timeseries_query = """
SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID == 4624
| summarize LogonCount=count() by bin(TimeGenerated, 1h)
| sort by TimeGenerated asc
"""

try:
    ts_df = qry_prov.exec_query(timeseries_query)
    ts_df = ts_df.set_index('TimeGenerated')
    
    print(f"✓ Retrieved {len(ts_df)} data points for time series analysis")
    
    # Perform time series anomaly detection
    from msticpy.analysis import timeseries
    
    ts_decomp = ts_df.mp_timeseries.analyze(
        data_column='LogonCount',
        seasonal=7,
        period=24
    )
    
    print("✓ Time series decomposition completed")
    
    # Identify anomalies
    anomalies_df = ts_decomp[ts_decomp['anomalies'] == 1]
    print(f"✓ Detected {len(anomalies_df)} anomalous hours in logon activity")
    
    globals()['anomalies_df'] = anomalies_df
    display(anomalies_df.tail(10))
    
except Exception as e:
    print(f"Note: Time series analysis may have limited data. Error: {str(e)}")
```

#### Visualize Anomalies

Add and run the following code:

```python
# Visualize anomalies in time series
try:
    fig, ax = plt.subplots(figsize=(14, 8))
    
    # Plot normal data
    normal_data = ts_decomp[ts_decomp['anomalies'] == 0]
    ax.plot(normal_data.index, normal_data['LogonCount'], 
            'o-', label='Normal', color='#4caf50', markersize=3)
    
    # Plot anomalies
    anomaly_data = ts_decomp[ts_decomp['anomalies'] == 1]
    ax.scatter(anomaly_data.index, anomaly_data['LogonCount'], 
              label='Anomaly', color='#d32f2f', s=100, zorder=5)
    
    ax.set_title('Logon Activity with Detected Anomalies', fontsize=14, fontweight='bold')
    ax.set_xlabel('Time', fontsize=12)
    ax.set_ylabel('Logon Count', fontsize=12)
    ax.legend()
    plt.xticks(rotation=45)
    plt.grid(True, alpha=0.3)
    plt.tight_layout()
    plt.show()
    
    print("✓ Anomaly visualization created")
except Exception as e:
    print(f"Could not create visualization: {str(e)}")
```


