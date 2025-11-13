# Threat Protection and Incident response with Microsoft Sentinel

### Overall Estimated Duration: 4 Hours

## Overview
 
In this lab, you will get hands-on experience with Microsoft Sentinel. Participants will learn how to deploy Sentinel, integrate critical data sources, enrich security insights using threat intelligence and content packs, and leverage User and Entity Behavior Analytics (UEBA) to detect anomalous activities.
By completing this lab, learners will be equipped to set up a robust security monitoring environment, detect potential threats, and initiate effective incident response measures.

## Objective

By the end of this lab, participants will be able to:

  - **Deploy Microsoft Sentinel** to a Log Analytics workspace for centralized security data collection and analysis.

  - **Enable and configure data connectors** to ingest security logs from various Microsoft and third-party services.

  - **Integrate threat intelligence** feeds and deploy relevant analytics/content from the Content Hub to enhance detection capabilities.

  - **Enable and use UEBA** in Microsoft Sentinel to detect abnormal user and entity behaviors.

Understand the role of each component in the threat detection and incident response workflow.

## Pre-requisites

Participants should have:

- Basic understanding of Microsoft Azure services and portal navigation.

- Experience with Defender portal.

- Familiarity with security concepts such as SIEM, SOAR, and threat intelligence.

- Experience with log analysis or security event monitoring.

## Architecture

In this lab, you will use Microsoft Sentinel to collect, analyze, and respond to security events from multiple data sources. The workflow begins by deploying a Log Analytics workspace and enabling Microsoft Sentinel for centralized log collection. You will connect various security data sources using built-in data connectors, including Azure Active Directory, Microsoft 365 Defender, and other supported services.Threat intelligence will be integrated into Sentinel to enrich alerts with known malicious indicators, enhancing the accuracy of detections. You will explore the Content Hub to deploy prebuilt analytics rules, hunting queries, and workbooks for faster detection and visualization. Additionally, you will enable User and Entity Behavior Analytics (UEBA) to profile normal user activity and detect anomalies.

Throughout the lab, you will investigate generated incidents, run hunting queries, and use automated playbooks to respond to threats, simulating a complete security operations workflow from detection to remediation.

## Architecture Diagram

![Image](./images/ArcDay1.png)

## Explanation of Components

The architecture for this lab involves the following key components:

1. **Log Analytics Workspace:** A central repository where Sentinel stores ingested log data.
   - Acts as the backend for Sentinel’s analytics and hunting capabilities.
   - Supports Kusto Query Language (KQL) for querying logs.

1. **Data Connectors:** Pre-built integrations that allow ingestion of logs and telemetry from various services:
   - Microsoft sources: Microsoft 365 Defender, Azure AD, Azure Activity, Security Events.
   - Non-Microsoft sources: Firewalls, endpoint solutions, SaaS applications.
   - Configured in Sentinel’s Data Connectors blade. 

1. **Threat Intelligence Connector:** Enables ingestion of threat indicators (IP addresses, domains, URLs, file hashes) from external or internal sources.
   - Enhances detection rules by correlating indicators with ingested telemetry.
   - Supports integration with Microsoft Defender Threat Intelligence (MDTI) or TAXII-based feeds.

1. **Content Hub:** A repository of packaged security solutions (workbooks, analytics rules, hunting queries, playbooks, data connectors) for specific products, threats, or industries.
   - Allows quick deployment of best-practice detections and visualizations. 

1. **UEBA (User and Entity Behavior Analytics):** A Sentinel feature that builds behavioral profiles for users and entities based on ingested data.
   - Detects anomalies by comparing current activity to baseline behavior.
   - Useful for detecting insider threats, compromised accounts, and suspicious activity.

1. **Kusto Query Language (KQL):** The query language used to search and analyze data within Sentinel.
   - Powers analytics rules, hunting queries, and workbooks.
   - Essential for creating custom detections.         

## Getting Started with Lab
Once you're ready to dive in, your virtual machine and **Guide** will be right at your fingertips within your web browser.

![Image](./images/GettingStarted-00.png)

## Lab Guide Zoom In/Zoom Out

To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

![Image](./images/GettingStarted-01.png)

## Virtual Machine & Lab Guide
Your virtual machine is your workhorse throughout the workshop. The guide is your roadmap to success.

## Exploring Your Lab Resources
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.

![Image](./images/GettingStarted-02.png)

## Utilizing the Split Window Feature
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the top right corner.

![Image](./images/GettingStarted-03.png)

## Managing Your Virtual Machine
Feel free to **start, restart, or stop (2)** your virtual machine as needed from the **Resources (1)** tab. Your experience is in your hands!

![Image](./images/GettingStarted-04.png)

## Let's Get Started with Azure Portal
 
1. On your virtual machine, click on the **Azure Portal** icon.

    ![Image](../Day2/images/GettingStarted-11.png)

1. On the **Sign in to Microsoft Azure** tab you will see the login screen, in that enter the following email/username, and click on **Next (2)**. 

   * **Email/Username**: <inject key="AzureAdUserEmail"></inject> **(1)**
   
      ![Image](./images/GettingStarted-05.png "Enter Email")
     
1. Now enter the following password and click on **Sign in (2)**.
   
   * **Password**: <inject key="AzureAdUserPassword"></inject> **(1)**
   
      ![Image](./images/GettingStarted-07.png "Enter Password")

      >**Note:** If prompted to Enter Temporary Access Pass, enter the following **Password**: <inject key="AzureAdUserPassword"></inject> **(1)** and click on **Sign in (2)**.

      ![](./images/GS-0.png) 

1. If you see the pop-up Action Required, click **Ask Later**.

   ![Image](./images/GettingStarted-08.png)

   >**NOTE:** Do not enable MFA, select **Ask Later**.
     
1. If you see the pop-up **Stay Signed in?**, select **No**.

   ![Image](./images/GettingStarted-06.png)

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

1. If a **Welcome to Microsoft Azure** popup window appears, select **Maybe Later** to skip the tour.

## Support Contact

The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:

- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Click **Next >>** from the bottom right corner to embark on your Lab journey!

![Image](./images/Next.png)

### Happy Learning!!
