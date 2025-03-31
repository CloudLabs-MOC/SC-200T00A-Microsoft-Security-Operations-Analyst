# Secure Windows Servers Azure Arc & Microsoft Defender

### Overall Estimated Duration: 4 hours

## Overview

In this hands-on lab, you will explore security operations and hybrid cloud management using Microsoft security and monitoring tools. You will start by onboarding on-premises Hyper-V VMs to Azure Arc, enabling centralized management of hybrid environments. You will then enable Microsoft Defender for Cloud to enhance cloud workload protection and respond to security alerts. Moving to Microsoft Sentinel, you will integrate log data from multiple sources, including Microsoft 365, non-Azure VMs, network appliances, and Linux VMs using CEF and Syslog connectors. 

## Objective

By completing this lab, you will learn to:

- **Onboard Windows Servers to Azure Arc**: Onboard on-premises servers to Azure Arc-enabled servers for centralized management and governance.
- **Enable Microsoft Defender for Cloud**: Configure security monitoring and threat protection by setting up a Subscription, creating a Log Analytics Workspace, enabling Microsoft Defender for Cloud, installing Azure Arc on an on-premises server, and implementing security measures to protect it.
- **Mitigate threats using Microsoft Defender for Cloud**: Enhance security and compliance awareness by exploring regulatory compliance, assessing security posture and recommendations, and mitigating security alerts effectively.
- **Connect Windows devices to Microsoft Sentinel using data connectors**: Set up the Microsoft Defender XDR workspace and configure security monitoring by connecting both Azure and non-Azure Windows machines. Onboard a Windows device to Microsoft Defender for Endpoint to enhance threat protection and response.
- **Connect Linux hosts to Microsoft Sentinel using data connectors**: Access the Microsoft Sentinel Workspace and connect a Linux host using the Common Event Format (CEF) connector. You will also connect another Linux host using the Syslog connector and configure facilities and severity levels for log collection.

## Prerequisites

- Basic knowledge of on-premises Hyper-V infrastructure
- Familiarity with Security Information and Event Management (SIEM) concepts
- Basic understanding of KQL syntax for querying and analyzing logs

## Architecture

In this hands-on lab, you will implement a comprehensive security and hybrid cloud management architecture leveraging Microsoft security and monitoring tools. The workflow begins with onboarding on-premises Hyper-V VMs to Azure Arc, extending Azure’s management capabilities to hybrid and multi-cloud environments. This enables centralized governance, policy enforcement, and security monitoring across on-premises and cloud resources. Next, you will activate Microsoft Defender for Cloud, which provides security posture management and threat protection, continuously assessing workloads and generating security alerts based on detected vulnerabilities or threats. To enhance security operations, you will integrate Microsoft Sentinel, a cloud-native SIEM and SOAR solution, to collect, correlate, and analyze log data from diverse sources, including Microsoft 365, non-Azure VMs, network appliances, and Linux VMs. This integration is facilitated using CEF (Common Event Format) and Syslog connectors, enabling the ingestion of security events and logs from heterogeneous environments. By combining these tools, you will establish a proactive security posture, leveraging AI-driven threat intelligence, automated incident response, and centralized visibility into security events across your hybrid infrastructure.

## Getting started with the lab
 
Welcome to your Secure Windows Servers Azure Arc & Microsoft Defender Workshop! We've prepared a seamless environment for you to explore and learn about Azure services. Let's begin by making the most of this experience:

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and lab guide will be right at your fingertips within your web browser.

   ![](../Media/lab6-100.png)
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
   ![](../Media/lab6-101.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
   ![](../Media/lab6-102.png)

## Managing Your Virtual Machine
 
Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!

   ![](../Media/lab6-104.png)

## Lab Guide Zoom In/Zoom Out
 
1. To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

   ![](../Media/new-get-start-25-6.png)

## Login to Azure Portal

1. In the JumpVM, click on the Azure portal shortcut of the Microsoft Edge browser from the desktop.

   ![](../Media/lab6-103.png)

1. In the Welcome to Microsoft Edge page, select **Start without your data**, and on the help for importing Google browsing data page select **Continue without this data** button and proceed to select **Confirm and start browsing** on the next page.
   
1. On the **Sign in to Microsoft Azure** tab you will see a login screen, enter the following email/username and then click on **Next**. 

   * Email/Username: <inject key="AzureAdUserEmail"></inject>
   
     ![](../Media/sc900-image-1.png)
     
1. Now enter the following password and click on **Sign in**.
   * Password: <inject key="AzureAdUserPassword"></inject>
   
     ![](../Media/sc900-image-2.png)

1. If you see the pop-up Action Required, click Ask Later.

     ![](../Media/asklater.png)     
 
    >**NOTE:** Do not enable MFA, select **Ask Later**.
     
1. If prompted to **stay signed in**, you can click **"No"**.
 
1. If a **Welcome to Microsoft Azure** pop-up window appears, simply click **Cancel** to skip the tour.

## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next** from the lower right corner to move on to the next page.

### Happy Learning!!
