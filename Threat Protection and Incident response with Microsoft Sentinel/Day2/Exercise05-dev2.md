# Exercise 5: Advanced Threat Hunting with Jupyter Notebooks in Microsoft Sentinel

## Estimated Duration: 90 Minutes

## Overview

In this comprehensive lab exercise, you will leverage **Jupyter notebooks** integrated with **Microsoft Sentinel** and the **MSTICPy Python library** to conduct advanced threat hunting. Jupyter notebooks provide a flexible, interactive environment for security analysis, combining **Kusto Query Language (KQL)** queries, Python data processing, and sophisticated visualizations. You will configure a complete notebook environment, establish secure connections to your Sentinel workspace, perform advanced data analysis using MSTICPy's threat hunting capabilities, and create reusable workflows for ongoing security investigations. By completing this exercise, you will develop powerful, reproducible threat hunting workflows that your security team can leverage for continuous incident investigation and proactive threat detection.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Access and Configure Jupyter Notebooks in Microsoft Sentinel
- Task 2: Create and Configure Your First Notebook
- Task 3: Initialize MSTICPy and Connect to Sentinel Workspace
- Task 4: Perform Advanced Threat Hunting Queries
- Task 5: Create Visualizations
- Task 6: Perform Anomaly Detection

### Task 1: Access and Configure Jupyter Notebooks in Microsoft Sentinel

In this task, you will access the Microsoft Sentinel notebook environment and configure the necessary resources for threat hunting.

1. Open your web browser and navigate to **Microsoft Defender Portal**:

    ```
    https://security.microsoft.com/
    ```

1. In the left sidebar, locate the **Microsoft Sentinel** section and click to expand menu options under **Threat management**, select **Notebooks** from the menu options.

    ![Picture](./images1/Ex08-01.png)

1. Click on the **Configure Azure Machine Learning** button to begin the setup process and select **Create a new ML workspace** from the available options.

    ![Picture](./images1/Ex08-01b.png)

1. Fill in the following details in the configuration form:

    | Field | Value |
    |-------|-------|
    | **Workspace name** | `aml` |
    | **Subscription** | Select your Azure subscription |
    | **Resource group** | sentinel-rg |
    | **Region** | Same region as your Sentinel workspace (important for performance) |
    | **Storage account** | Auto-created or select existing |
    | **Key vault** | Auto-created |
    | **Application Insights** | Auto-created |

1. Click **Review + Create** and wait 3-5 minutes for the workspace to provision.

    ![Picture](./images1/Ex08-01c.png)

### Task 2: Create and Configure Your First Notebook

In this task, you will create a new notebook from a template and configure it for your threat hunting analysis.

1. Click on **Templates (1)** and select **A Getting Started Guide For Microsoft Sentinel ML Notebooks (2)**

    ![Picture](./images1/Ex08-02.png)

1. Select **Create from template**

    ![Picture](./images1/Ex08-02-b.png)

1. Leave the name of your notebook to default and the Azure Machine Learning workspace to **aml** and cick **Save** to save the notebook configuration to your ML workspace.

    ![Picture](./images1/Ex08-02-c.png)

1. Click **Save** to save the notebook configuration to your ML workspace.

1. Wait for the notebook to be created and provisioned (approximately 1-2 minutes).

1. Click **Launch notebook** to open the notebook in the Jupyter environment.

    ![Picture](./images1/Ex08-02-d.png)

1. Once the Notebook is launched, select **Serverless Spark Compute** for Compute

    ![Picture](./images1/Ex08-02-e.png)

1. 

### Task 3: Initialize MSTICPy and Connect to Sentinel Workspace

In this task, you will initialize the MSTICPy library and establish a secure connection to your Microsoft Sentinel workspace.

#### Import Required Libraries

In a code cell, add and run the following Python code:

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

**Expected Output**: The code should display the version numbers for each library and print a success message confirming all libraries have been imported.

#### Initialize Notebook Environment

Add and run the following code in the next cell:

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
- Configuration loading messages will display
- Success indicators will confirm initialization
- Warnings about missing configuration are normal on the first run

#### Configure MSTICPy Settings (First Time Only)

Run this code to launch the configuration editor for MSTICPy:

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

1. In the **AzureSentinel** tab of the configuration editor, enter the following details:

    - **Workspace name**: Your Sentinel workspace name
    - **Workspace ID**: Your workspace ID (found in Sentinel > Settings > Workspace settings)
    - **Tenant ID**: Your Azure AD tenant ID

2. Click **Save Settings** and close the editor to save your configuration.

#### Establish Connection to Sentinel Workspace

Add and run the following code in the next cell:

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
- You will be prompted to authenticate with your Azure credentials
- A device code will be provided in the output
- Follow the link provided to authenticate using your organizational account
- Return to the notebook once authentication is complete

**If authentication fails**, verify the following:
- Check that you have the **LogAnalytics Reader** role on the workspace
- Verify the **Workspace ID** and **Tenant ID** are correct in your configuration
- Try restarting the kernel: Select **Kernel** > **Restart**

#### Verify Connection with Test Query

Run this code to verify your connection to Microsoft Sentinel is working correctly:

```python
# Test connection with a simple query
test_query = """
SecurityAlert
| where TimeGenerated > ago(7d)
| summarize AlertCount=count() by AlertName
| top 10 by AlertCount
"""
```

### Task 4: Perform Advanced Threat Hunting Queries

In this task, you will execute advanced threat hunting queries using KQL within your Jupyter notebook environment.

1. Execute threat hunting queries by combining KQL with Python data processing.

2. Analyze the results using pandas DataFrames for detailed investigation.

3. Create reusable query templates for your security team.

### Task 5: Create Visualizations

In this task, you will generate meaningful visualizations to support your threat hunting analysis.

1. Create charts and graphs to visualize threat hunting results.

2. Build interactive dashboards within your notebook for incident analysis.

3. Export visualization reports for stakeholder communication.

### Task 6: Perform Anomaly Detection

In this task, you will implement anomaly detection techniques to identify unusual security patterns.

1. Configure MSTICPy anomaly detection algorithms.

2. Analyze security events for statistical outliers and behavioral anomalies.

3. Generate alerts based on detected anomalies.

## Summary

In this exercise, you successfully:

- **Accessed and configured** Jupyter notebooks in Microsoft Sentinel
- **Created and deployed** your first notebook with proper environment setup
- **Initialized MSTICPy** and established a secure connection to your Sentinel workspace
- **Executed advanced threat hunting** queries using KQL within Python
- **Created visualizations** to support security analysis and incident investigation
- **Implemented anomaly detection** to identify unusual security patterns

## You have successfully completed the exercise!

### Now, click on **Next >>** from the lower right corner to move on to the next page.

   ![](./images/Next.png)