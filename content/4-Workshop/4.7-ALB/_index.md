---
title: "Integrate Application Load Balancer"
date: 2026-04-04
weight: 07
chapter: false
pre: " <b> 4.7. </b> "
---

The Application Load Balancer (ALB) sits in the **public subnet** and acts as the single entry point for all API traffic from the Amplify frontend. It forwards requests to the EC2 instance on port 8000 in the private subnet via a Target Group.

The setup has two parts:
1. Create a **Target Group** that registers the EC2 instance
2. Create the **ALB** and attach the Target Group to a listener

---

### Part 1 — Create the Target Group

#### Step 1 — Open EC2 and Navigate to Target Groups

Navigate to **EC2** in the AWS Console. In the left sidebar scroll down to **Load Balancing → Target Groups**. Click **Create target group**.

Configure the target group:
- **Target type**: Instances
- **Target group name**: `voice-summarizer-tg`
- **Protocol**: HTTP
- **Port**: `8000`
- **VPC**: `voice-summarizer-vpc`
- **Health check protocol**: HTTP
- **Health check path**: `/` *(or `/health` if your FastAPI app has a health endpoint)*

![Create Target Group Settings](/images/workshop/7-alb/alb-01-target-group-settings.png)

---

#### Step 2 — Register the EC2 Instance

Scroll down to **Register targets**. Select the `voice-summarizer-backend` EC2 instance and click **Include as pending below**.

![Select EC2 Instance](/images/workshop/7-alb/alb-02-register-ec2.png)

---

#### Step 3 — Review Before Creating

Review all settings — confirm the target is the correct EC2 instance on port 8000 and the VPC is correct.

![Review Target Group](/images/workshop/7-alb/alb-03-review.png)

---

#### Step 4 — Create the Target Group

Click **Create target group**. Wait for the target group status to show **Active** and the target health to eventually show **Healthy** after the ALB starts sending health checks.

![Create Target Group](/images/workshop/7-alb/alb-04-create-tg.png)

---

### Part 2 — Create the Application Load Balancer

#### Step 5 — Navigate to Load Balancers and Choose ALB

In the left sidebar click **Load Balancers**. Click **Create load balancer**. On the selection page, choose **Application Load Balancer**.

![Choose Application Load Balancer](/images/workshop/7-alb/alb-05-choose-alb.png)

---

#### Step 6 — Configure the ALB — Basic Settings

Fill in the ALB configuration:

- **Name**: `voice-summarizer-alb`
- **Scheme**: Internet-facing *(allows the Amplify frontend to reach it from the public internet)*
- **IP address type**: IPv4
- **VPC**: `voice-summarizer-vpc`
- **Mappings**: Select **ap-southeast-1a** and choose `voice-summarizer-public-subnet`

{{% notice info %}}
The ALB must be placed in the **public subnet**. It receives traffic from the internet and forwards it internally to the EC2 instance in the private subnet.
{{% /notice %}}

![ALB Basic Settings](/images/workshop/7-alb/alb-06-settings.png)

---

#### Step 7 — Configure Listener, Security Group, and Create

**Security groups:**
- Create or select a security group for the ALB that allows inbound **HTTP (80)** and **HTTPS (443)** from `0.0.0.0/0`

**Listeners and routing:**
- **Protocol**: HTTP
- **Port**: 80
- **Default action**: Forward to `voice-summarizer-tg`

Review all settings and click **Create load balancer**.

![ALB Listener and Final Settings](/images/workshop/7-alb/alb-07-final-settings.png)

After creation, note the **DNS name** of the ALB (e.g. `voice-summarizer-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com`). This is the base URL your frontend will call for all API requests.

---

{{% notice tip %}}
✅ The ALB is deployed in the public subnet and forwards traffic to the EC2 instance. 

Copy the **ALB DNS name** — you will need it when configuring the frontend API client in the Amplify deployment step.
{{% /notice %}}
