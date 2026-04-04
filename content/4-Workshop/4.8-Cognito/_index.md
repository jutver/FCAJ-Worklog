---
title: "Creating Cognito User Pool"
date: 2026-04-04
weight: 8
chapter: false
pre: " <b> 4.8. </b> "
---

Amazon Cognito manages user registration, email verification, login, and JWT token issuance for the platform. The React frontend uses the Cognito **Hosted UI** and the Amplify/Cognito JS SDK to authenticate users. A **Post Confirmation Lambda trigger** wires Cognito to the `user_creation_db` Lambda from Section 5.2, automatically provisioning a DynamoDB record when a new user verifies their email.

By the end of this section you will have:
- A Cognito **User Pool**
- An **App Client** configured for SPA (no client secret)
- The **Pool ID** and **Client ID** values needed for the frontend config file

---

#### Step 1 — Open Cognito and Go to User Pools

Navigate to **Amazon Cognito** in the AWS Console. Click **User pools** in the left sidebar, then click **Create user pool**.

![Open Cognito User Pools](/images/workshop/8-cognito/cognito-01-user-pools.png)

---

#### Step 2 — Choose Application Type: Single-Page Application (SPA)

On the first screen, select **Single-page application (SPA)** as the application type. This configures the app client without a client secret, which is required for browser-based authentication flows.

![Choose SPA](/images/workshop/8-cognito/cognito-02-spa.png)

---

#### Step 3 — Configure Sign-In, Self-Registration, and Attributes

Configure the sign-in and registration options:

- **Sign-in options**: ✅ **Email**
- **Self-registration**: ✅ **Enable self-registration** *(allows users to sign up themselves)*
- **Required attributes**: ✅ **email**
- **MFA**: Optional (leave off for the workshop)
- **User account recovery**: Email

![Configure Email and Self-Registration](/images/workshop/8-cognito/cognito-03-email-selfregistration.png)

---

#### Step 4 — Create the User Pool

Review all settings. Scroll down and click **Create user pool**.

- **User pool name**: `voice-summarizer-user-pool`

![Create User Pool](/images/workshop/8-cognito/cognito-04-create-user-pool.png)

---

#### Step 5 — Copy the User Pool ID

After creation, click on `voice-summarizer-user-pool` to open its detail page. At the top of the **Overview** tab, locate and copy the **User pool ID** (format: `ap-southeast-1_XXXXXXXXX`).

You will paste this value into the frontend config file in Step 7.

![Copy User Pool ID](/images/workshop/8-cognito/cognito-05-copy-pool-id.png)

---

#### Step 6 — Open the App Client and Copy the Client ID

In the left sidebar (inside the User Pool detail view) click **App clients**. Click on the app client that was automatically created. Copy the **Client ID**.

You will paste this value alongside the Pool ID in the frontend config file.

![Copy Client ID](/images/workshop/8-cognito/cognito-06-copy-client-id.png)

---

#### Step 7 — Create the Frontend Config File

In your frontend repository, open or create the file `src/aws-config.js` (the path matches the existing `aws-config.js` in the project). Populate it with the values you just copied:

```javascript
const awsConfig = {
  userPoolId: "ap-southeast-1_XXXXXXXXX",   // ← Paste your User Pool ID
  userPoolClientId: "XXXXXXXXXXXXXXXXXXXXXXXXXX", // ← Paste your Client ID
  region: "ap-southeast-1",
};

export default awsConfig;
```

Commit and push this file to GitHub. The Amplify deployment in Section 9 will pick it up automatically.

![Create Config File](/images/workshop/8-cognito/cognito-07-config-file.png)

---

#### Step 8 — Add the Post Confirmation Lambda Trigger

Still in the User Pool detail view, click **User pool properties** in the left sidebar. Scroll to **Lambda triggers** and click **Add Lambda trigger**.

- **Trigger type**: Authentication
- **Authentication event**: **Post confirmation trigger**
- **Lambda function**: `user_creation_db`

Click **Add Lambda trigger**.

![Add Post Confirmation Trigger](/images/workshop/8-cognito/cognito-08-lambda-trigger.png)

This wires the `user_creation_db` Lambda to fire automatically every time a new user successfully verifies their email, creating their DynamoDB record without any additional backend logic.

---

{{% notice tip %}}
✅ Cognito is fully configured:
- Users can self-register with their email address
- Email verification is required before access is granted
- On successful verification, the `user_creation_db` Lambda provisions a DynamoDB record automatically
- The frontend `aws-config.js` has the Pool ID and Client ID needed for the Cognito JS SDK

Keep the **User Pool ID** and **Client ID** handy — you will verify they are correct during the Amplify deployment test.
{{% /notice %}}
