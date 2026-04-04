---
title : "DynamoDB Tables"
date: "2000-01-01"
weight : 03
chapter : false
pre : " <b> 4.4.3. </b> "
---

You will create **two DynamoDB tables**:

| Table Name | Partition Key | Sort Key | Purpose |
|---|---|---|---|
| `VoiceSummarizerHistory` | `raw_id` (String) | — | Per-recording status, progress, stage, and conversation memory |
| `User` | `user_id` (String) | — | User records provisioned by the Cognito Lambda trigger |

---

### Table 1 — VoiceSummarizerHistory

This is the main operational table. The Celery worker writes status transitions (`pending → processing → completed / failed`) here, and the FastAPI router reads from it to serve status polls and conversation memory.

#### Step 1 — Open DynamoDB and Click Create Table

Navigate to **DynamoDB** in the AWS Console. Click **Create table**.

![Click Create Table](/images/workshop/4-storage/dynamo-01-create-table.png)

---

#### Step 2 — Configure the History Table

Fill in the table settings:

- **Table name**: `VoiceSummarizerHistory`
- **Partition key**: `raw_id` — type **String**
- **Sort key**: *(leave empty)*
- **Table settings**: Default settings (On-demand capacity)

![Enter Table Name and Partition Key](/images/workshop/4-storage/dynamo-02-table-name-partition-key.png)

---

#### Step 3 — Create the Table

Review the settings and click **Create table**. Wait for the status to change to **Active** before proceeding.

![Click Create](/images/workshop/4-storage/dynamo-03-create.png)

---

### Table 2 — User

This table is written to by the Cognito post-confirmation Lambda (`lambda_user_creation_db.py`). When a user verifies their email after registration, a record is automatically created here with their `user_id`, `email`, `created_at`, and usage counters.

#### Step 4 — Create the User Table

Click **Create table** again. Configure:

- **Table name**: `User`
- **Partition key**: `user_id` — type **String**
- **Sort key**: *(leave empty)*

![Configure User Table](/images/workshop/4-storage/dynamo-04-user-table-keys.png)

---

#### Step 5 — Create the User Table

Click **Create table**. Wait for the status to show **Active**.

![Create User Table](/images/workshop/4-storage/dynamo-05-create-user-table.png)

---

#### Step 6 — Verify Both Tables Exist

In the DynamoDB console, confirm both tables are listed with **Active** status:

![Verify All Tables](/images/workshop/4-storage/dynamo-06-verify-tables.png)

---

{{% notice tip %}}
✅ Both DynamoDB tables are ready:
- **VoiceSummarizerHistory** — tracks recording pipeline state
- **User** — stores user records created on Cognito sign-up

Note: The environment variable `HISTORY_TABLE` on the EC2 instance should be set to `VoiceSummarizerHistory`, and `USERS_TABLE` in the Lambda code maps to `User`.
{{% /notice %}}
