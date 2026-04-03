---
title: "Week 13 Worklog"
date: "2025-12-01"
weight: 13
chapter: false
pre: " <b> 1.13. </b> "
---
### Week 13 Objectives:
Complete the project and submit
### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Removed Map State for Isolating EC2 Instance in Steps Function <br> - Created Lambdas to add policies to EC2 Instance for SSM automation in IR Step Functions <br> - Reconfigured Quarantine SG: Added Outbound rule for HTTPS for SSM connection <br> - Replaced Lambdas with Step Functions provided States: Used DescribeIamInstanceProfileAssociation, AttachRolePolicy, DetachRolePolicy and StartAutomationExecution <br> - CDK: Created EventBridge and Topics with subscription emails stored in cdk-context <br> - Team meetings: Planned and reassigned task to meet the new deadline | 01/12/2025 | 01/12/2025      ||
| 3   | - CDK: Added SES alert for GuardDuty findings <br> - CDK: Added ENI ETL into ETL Pipeline <br> - Assisted in upgrading dashboard <br> Updated Event Participated and overall Worklog update fix and improvement <br> - Researched more on how to optimize pipeline, currently the S3 Get Request is higher than expected do to Athena query low size but many objects | 02/12/2025 | 02/12/2025      |  |
| 4   | - CDK: Upgraded Alert with Slack <br> - Architecture: <br> &emsp; + Researched and failed in using SQS to pool logs before sending to Lambda: Lambda is still event based and still process log individually instead of pooling <br> &emsp; + Researched and added Data Firehose to consolidate logs before writing to the processed S3 => Reduced the amount of objects written to S3 <br> - IR Step Function revised: Removed SSM actions due to it requiring outbound connections after isolating EC2 => Replaced it with tagging, removing it from ASG and taking a EBS Snapshot to for analyzing and preserving data <br> - Team member updated CloudWatch ETL with Data Firehose succesfully <br> - CDK: Updated all of ETL Pipeline with Kinesis Firehose + Overhauled CloudTrailELT | 03/12/2025 | 03/12/2025  |  |
| 5   | - Partly finished writing Workshop on creating ETL Pipeline <br> CDK: Created and updated Step Functions: Removed SSM entirely replacing it with tagging, termination protection, detachment from ASG and snapshot creation <br> - Removed SQS between EventBridge and StepFunctions <br> - Updated Worklog: Events  | 04/12/2025 | 04/12/2025      |  |
| 6   | - Joined the BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock Workshop: Won a prize from CloudThinker for winning in the Workshop <br> - Updated GuardDuty ETL and table for querying optimzation <br> - Redrew and updated Architecture Diagram <br> Updated Proposal to the newest format <br> - Updated Step Functions States <br> - Overall infrastructure optimization and bug fixes | 05/12/2025 | 07/12/2025      | [Event Summary and Experience](../../4-EventParticipated/4.7-Event7)|


### Week 13 Achievements:
* Final Architecture Refinement and Optimization
    * **Integrated Kinesis Data Firehose** into the ETL pipelines (including CloudWatch and CloudTrail) to consolidate logs before writing to S3.
        * This redesign successfully **reduced the number of objects written to S3**, optimizing the pipeline and lowering future Athena query costs. 
    * Overhauled the **CloudTrail ETL** to work with the new Firehose configuration.
    * Added **ENI (Elastic Network Interface) ETL** into the core data processing pipeline.
    * Finalized overall **infrastructure optimization and bug fixes** across the project.
* Incident Response Workflow Overhaul
    * Completely **revised the IR Step Function** to remove reliance on outbound connections (SSM), which were blocked after isolation.
    * The new isolation workflow now focuses on robust **data preservation and asset removal** by:
        * Tagging the instance.
        * Enabling termination protection.
        * Detaching the instance from its **Auto Scaling Group (ASG)**.
        * Creating an **EBS Snapshot** for forensic analysis.
* AWS CDK
    * Finalized the **CDK Stack for the Incident Response workflow**, implementing the new, fully-revised Step Functions logic.
    * Completed the **CDK deployment of all alerts**, adding both **SES** and **Slack** notifications for GuardDuty findings.
* Documentation and Workshop Material
    * Redrew and updated the Architecture Diagram to reflect the final Kinesis Firehose integration and IR changes.
    * Updated the Proposal to its newest and final format.
    * Partly finished writing the Workshop documentation.
* Event Participated
    * Joined the **BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock Workshop**.
    * Won a prize from CloudThinker during the workshop.