---
title: "Week 10 Worklog"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:
* Fully research and test all of the components and ready to add together to build the workshop

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Assisted in building ETL Pipeline for CloudWatch logs with team member <br> -  Updated proposal:<br>&emsp; + Included updated Architecture and Services <br>&emsp; + Recalculated prices | 10/11/2025 | 10/11/2025      ||
| 3   | - Finished building ETL Pipeline for CloudWatch logs <br> - Fixed ETL Pipeline for CloudTrail logs: Processed logs from different dates caused schema errors due to randomized field order in struct data type <br> - Successfully used AWS SSM to get EC2 system logs after IR Responses <br> - Successfully integrated threat notification chatbots in Slack and Telegram <br> - Successfully showed formatted notifications based on live threat findings <br> Got sent over 1000 emails because team member triggered all GuardDuty sample findings combined with multiple test SNS <br> - Team member suggested adding SES (Simple Email Service) to format emails and send| 11/11/2025 | 11/11/2025 ||
| 4   |- Did research into CloudTrail Lake: Good for future usage specifically for in-depth CloudTrail log analysis, deemed unnecessary for current project due to it being CloudTrail exclusive <br> - Updated CloudTrail ETL Lambda: promoted fields in request parameters into columns for better query and fewer schema crawling errors => Reliably crawled processed data between days <br> - Team members started on designing dashboard site, suggested integrating Grafana <br> - Team member finished Lambda IR Functions <br> - Got started on updating proposal to the new format| 12/11/2025 | 12/11/2025      ||
| 5   | - Successfully tested using Lambda to query with Athena to prepare for API Gateway for Dashboard <br> - Family matters | 13/11/2025 | 13/11/2025      | [Lambda Athena Query Guide](https://www.youtube.com/watch?v=a_Og1t3ULOI)|
| 6   | - Crawling raw GuardDuty exported logs proved to be a bad idea, a large number of schema errors <br> - Built a Lambda ETL Pipeline for GuardDuty logs <br> - Revised architecture: <br>&emsp; + Directed the log from GuardDuty to the Raw Log S3 Bucket to undergo ETL Pipeline <br>&emsp; Added SES as per team member's suggestion <br> - Researched alternative architectures: We might be able to remove Crawler altogether, due to the custom Lambda ETL pipeline we created, we already did most of the Crawler's service. Crawler is mostly used for large amounts of logs with various data types, except for **struct** data type it seems, which CloudWatch, CloudTrail and GuardDuty logs have a lot of. After formatting the logs into Parquet with custom Lambda ETL, Crawler's purpose now is to turn it into a Catalog Table, which alternatively can be done with Lambda. Will be testing this alternative approach. <br> - Successfully updated CloudTrail ETL Pipeline to directly call Glue API to create table without the use of Crawler <br> - Included the use of KMS in the project due to the sensitive nature of the security logs <br> - Joined the AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS | 14/11/2025 | 16/11/2025 |[Event Summary and Experience](../../4-EventParticipated/4.3-Event3)|


### Week 10 Achievements:

* Advanced ETL Pipeline Development and Optimization**
    * Successfully completed the build of the ETL pipeline for **CloudWatch logs**.
    * Resolved critical schema errors in the **CloudTrail ETL pipeline** to ensure reliable processing of data across different dates.
    * Built a custom Lambda ETL pipeline for **GuardDuty logs** to address schema issues encountered with raw log exports.
    * Refined the CloudTrail ETL process to bypass the **Glue Crawler** by having the Lambda function directly call the **Glue API** to create the Catalog Table.
* Security Tooling and Notification Integration
    * Successfully implemented **AWS Systems Manager (SSM)** for the retrieval of EC2 system logs for incident response.
    * Integrated and tested threat notification chatbots in both **Slack** and **Telegram**, successfully showing formatted notifications based on live threat findings.
    * Added **Amazon Simple Email Service (SES)** to the project architecture for professional email formatting and distribution.
* Project Architecture, Documentation, and Security
    * Updated the project proposal, including the revised architecture, service list, and recalculated pricing.
    * Integrated **Key Management Service (KMS)** into the project to secure the sensitive security logs.
* Dashboard Backend Development
    * Successfully tested a Lambda function to query with **Athena**, preparing for the **API Gateway** integration for the dashboard.
    * Contributed to the dashboard design, suggesting the integration of **Grafana**.
* Event Participated
    * Joined the AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS
