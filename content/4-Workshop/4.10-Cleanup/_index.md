---
title: "Clean Up"
date: 2026-04-04
weight: 10
chapter: false
pre: " <b> 4.10. </b> "
---

AWS Amplify hosts and continuously deploys the React + Vite frontend directly from your GitHub repository. Every push to the configured branch triggers an automatic rebuild and deployment. Amplify handles HTTPS, CDN distribution, and custom domain configuration.

**Before starting this section, make sure:**
- The `aws-config.js` file with the Cognito Pool ID and Client ID has been committed to your repo (Section 8, Step 7)
- The ALB DNS name has been set as the API base URL in `src/services/apiClient.js`

---

#### Step 1 — Open AWS Amplify and Connect to GitHub

Navigate to **AWS Amplify** in the AWS Console. Click **Create new app**, then select **GitHub** as the source.

Authorize Amplify to access your GitHub account if prompted.

![Open Amplify and Choose GitHub](/images/workshop/9-amplify/amplify-01-github.png)

---

#### Step 2 — Select the Repository

From the repository list, select the repository containing the Voice Summarizer frontend code (`voice-summarizer` or equivalent). If the repository does not appear, click **View GitHub permissions** and grant Amplify access to the correct repository.

![Select Repository](/images/workshop/9-amplify/amplify-02-select-repo.png)

---

#### Step 3 — Choose the Branch and Root Directory

- **Branch**: `main` (or your deployment branch)
- **App root directory**: `api/fe` *(the React frontend lives inside the `api/fe/` subdirectory of the monorepo)*

Amplify will auto-detect the Vite build settings. Confirm the build command and output directory:

| Setting | Value |
|---|---|
| Build command | `npm run build` |
| Build output directory | `dist` |
| Node.js version | 18 or 20 |

![Choose Branch and Directory](/images/workshop/9-amplify/amplify-03-branch-directory.png)

---

#### Step 4 — Review and Create the Amplify App

Review all settings. Add any required **environment variables** your frontend build needs (e.g. `VITE_API_URL` pointing to the ALB DNS name if you use it at build time).

Click **Save and deploy**.

Amplify will provision a build environment, clone the repository, run the build, and deploy the output to its CDN. This typically takes 2–4 minutes.

![Create Amplify App](/images/workshop/9-amplify/amplify-04-create.png)

---

#### Step 5 — Wait for Deployment and Open the Domain

Once the deployment pipeline shows all green checkmarks (Provision → Build → Deploy → Verify), click on the **Domain** link to open the live application.

The default domain format is:
```
https://main.<app-id>.amplifyapp.com
```

![Open Amplify Domain](/images/workshop/9-amplify/amplify-05-domain.png)

---

#### Verify the Full Stack Is Working

Open the live URL and test the following:

1. **Registration** — Create a new user account. You should receive a verification email from Cognito.
2. **Email verification** — Click the verification link. The `user_creation_db` Lambda should fire and create a DynamoDB record in the `User` table.
3. **Login** — Log in with the new account. A JWT token should be issued by Cognito and stored in the browser session.
4. **Audio upload** — Upload a short audio file. The file should land in `s3://one4allthing/raw_audio/`, trigger the `audio2text` Lambda, start a Transcribe job, and eventually show a status of `completed` in the dashboard.
5. **Q&A** — Open the completed recording and ask a question. The FastAPI server should return a grounded answer.

{{% notice info %}}
**Custom domain:** To use a custom domain instead of the default `.amplifyapp.com` URL, go to **Amplify → App settings → Domain management** and add your domain. Amplify will automatically provision an SSL certificate via ACM.
{{% /notice %}}

---

{{% notice tip %}}
✅ The Voice Summarizer platform is fully deployed! The complete data flow is now live:

User → Amplify → Cognito (auth) → ALB → EC2 (FastAPI + Celery) → S3 / DynamoDB / Transcribe / Lambda → LLM API
{{% /notice %}}
