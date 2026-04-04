---
title : "User Creation Lambda Trigger"
date: "2000-01-01"
weight : 02
chapter : false
pre : " <b> 4.5.2. </b> "
---

This Lambda is triggered by Amazon Cognito's **Post Confirmation** event. When a new user verifies their email after registration, Cognito calls this function, which creates a record in the `User` DynamoDB table containing the user's ID, email, creation timestamp, and initial usage counters.

**Runtime:** Python 3.11  
**Trigger:** Cognito User Pool — Post Confirmation trigger *(configured in Section 8)*

---

#### Step 1 — Create the Lambda Function

Navigate to **Lambda** in the AWS Console. Click **Create function**.

- **Function name**: `user_creation_db`
- **Runtime**: **Python 3.11** *(important — do not use the default)*
- **Architecture**: x86_64
- **Execution role**: Create a new role with basic Lambda permissions

Click **Create function**.

![Click Create Function](/images/workshop/5-lambda/lambda-user-01-create-function.png)

---

#### Step 2 — Enter the Name, Set Runtime to Python 3.11, and Deploy the Code

After creation, open the function and replace the default handler code with the following:

![Name and Python 3.11](/images/workshop/5-lambda/lambda-user-02-name-python311.png)

```python
import boto3
from botocore.exceptions import ClientError
from datetime import datetime
import os

DYNAMODB_REGION = os.environ.get("DYNAMODB_REGION", "ap-southeast-1")
dynamodb = boto3.resource("dynamodb", region_name=DYNAMODB_REGION)
USERS_TABLE = "User"

def lambda_handler(event, context):
    """
    Cognito Post Confirmation Trigger.
    Creates a DynamoDB record when a user verifies their email.
    """
    print(f"Cognito Event Triggered: {event['triggerSource']}")

    if event["triggerSource"] == "PostConfirmation_ConfirmSignUp":
        user_attributes = event["request"]["userAttributes"]
        user_id = user_attributes.get("sub")
        email = user_attributes.get("email", "")

        if not user_id:
            print("Error: No 'sub' found in user attributes.")
            return event

        try:
            table = dynamodb.Table(USERS_TABLE)
            table.put_item(
                Item={
                    "user_id": user_id,
                    "email": email,
                    "created_at": datetime.utcnow().isoformat() + "Z",
                    "total_files": 0,
                    "storage_used_bytes": 0,
                    "total_audio_duration": 0,
                },
                ConditionExpression="attribute_not_exists(user_id)"
            )
            print(f"Successfully provisioned DynamoDB record for user: {user_id}")

        except ClientError as e:
            if e.response['Error']['Code'] == 'ConditionalCheckFailedException':
                print(f"User {user_id} already exists. Skipping.")
            else:
                print(f"Failed to insert user into DynamoDB: {e}")

    return event
```

Click **Deploy**.

---

#### Add IAM Permissions to the Lambda Role

Navigate to **Configuration → Permissions** and open the execution role in IAM. Add the following inline policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:PutItem",
        "dynamodb:GetItem"
      ],
      "Resource": "arn:aws:dynamodb:ap-southeast-1:*:table/User"
    }
  ]
}
```

---

{{% notice info %}}
The Cognito trigger that connects this Lambda to your User Pool will be configured in **Section 8 — Cognito Setup**. You will select this function as the Post Confirmation trigger when creating the User Pool.
{{% /notice %}}

{{% notice tip %}}
✅ The `user_creation_db` Lambda is deployed and ready. It will be wired to Cognito in the next sections.
{{% /notice %}}
