---
title : "Lambda Functions Setup"
date: "2000-01-01"
weight : 05
chapter : false
pre : " <b> 4.5. </b> "
---

The Voice Summarizer platform uses two Lambda functions, each serving a distinct purpose:

| Function | Trigger | Purpose |
|---|---|---|
| `audio2text` | S3 object creation in `raw_audio/` | Reads the uploaded audio file and starts an AWS Transcribe job |
| `user_creation_db` | Cognito Post Confirmation | Provisions a new user record in the DynamoDB `User` table on email verification |

#### Content

- [Audio-to-Text Lambda](4.5.1-lambda-audio-to-text/)
- [User Creation Lambda](4.5.2-lambda-user-creation/)