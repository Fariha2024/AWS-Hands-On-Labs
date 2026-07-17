
![alt text](<cloudwatch lab/cloudwatch-1.png>)


![alt text](<cloudwatch lab/cloudwatch01.png>)



![alt text](<cloudwatch lab/cloudwatch2.png>)


![alt text](<cloudwatch lab/cloudwatch3.png>)


![alt text](<cloudwatch lab/cloudwatch-3.png>)


![alt text](<cloudwatch lab/cloudwatch4.png>)


![alt text](<cloudwatch lab/cloudwatch-4.png>)


![alt text](<cloudwatch lab/cloudwatch5.png>)

![alt text](<cloudwatch lab/cloudwatch-5.png>)

![alt text](<cloudwatch lab/cloudwatch6.png>)

![alt text](<cloudwatch lab/cloudwatch-6.png>)

![alt text](<cloudwatch lab/cloudwatch7.png>)

![alt text](<cloudwatch lab/cloudwatch-7.png>)


![alt text](<cloudwatch lab/cloudwatch-8.png>)



# CloudWatch Monitoring and Alarm Lab (Beginner Level)

## Lab Purpose

The purpose of this lab is to learn:

* What AWS CloudWatch is
* How CloudWatch monitors AWS resources
* Difference between Basic and Detailed Monitoring
* How to create a CloudWatch Alarm
* How to receive notifications using SNS
* How to test an alarm by generating high CPU usage on an EC2 instance

---

# Lab Flow

```text
EC2 Instance
      ↓
CloudWatch Monitoring
      ↓
Create SNS Topic
      ↓
Create CloudWatch Alarm
      ↓
Generate CPU Load
      ↓
Alarm Changes:
OK → In Alarm
      ↓
Receive Notification
      ↓
Stop Load
      ↓
Alarm Returns:
In Alarm → OK
```

---

# Theory

## CloudWatch

AWS CloudWatch is a:

* Monitoring Service
* Regional Service

CloudWatch monitors AWS resources and applications.

Examples:

### Compute Services

* EC2 Instances
* Auto Scaling Groups
* Elastic Load Balancer (ELB)
* Route 53 Health Checks

### Storage Services

* EBS Volumes
* Storage Gateway
* CloudFront

---

## CloudWatch Monitoring Types

### 1. Basic Monitoring (Default)

* Free
* Metrics collected every 5 minutes

### 2. Detailed Monitoring

* Paid Service
* Metrics collected every 1 minute

---

# Lab Architecture

```text
EC2 Instance
      │
      ▼
CloudWatch Metrics
      │
      ▼
CloudWatch Alarm
      │
      ▼
SNS Topic
      │
      ▼
Email Notification
```

---

# Step 1: Launch EC2 Instance

Go to:

```text
AWS Console
→ EC2
→ Launch Instance
```

Configuration:

```text
Name:
cloudwatch-lab-ec2

AMI:
Amazon Linux 2023

Instance Type:
t3.micro

Key Pair:
aws hands on labs

Security Group:
Allow SSH (Port 22)

Storage:
Default
```

Click:

```text
Launch Instance
```

Wait until:

```text
Running
3/3 Status Checks Passed
```

---

# Step 2: Open CloudWatch

Go to:

```text
AWS Console
→ CloudWatch
```

Observe:

```text
Metrics
Dashboards
Logs
Alarms
Events
```

---

# Step 3: Create SNS Topic

Purpose:

SNS will send email notifications whenever the alarm changes state.

Go to:

```text
CloudWatch
→ Alarms
→ Create Alarm
```

During alarm creation select:

```text
Create New SNS Topic
```

Topic Name:

```text
cloudwatch-alerts-alaram
```

Email:

```text
your-email@example.com
```

Click:

```text
Create Topic
```

---

# Step 4: Confirm Email Subscription

Check your email inbox.

AWS sends:

```text
AWS Notification - Subscription Confirmation
```

Open email.

Click:

```text
Confirm Subscription
```

Status becomes:

```text
Confirmed
```

---

# Step 5: Create CloudWatch Alarm

Go to:

```text
CloudWatch
→ Alarms
→ Create Alarm
```

---

## Select Metric

Choose:

```text
Metrics
```

Select:

```text
EC2
→ Per-Instance Metrics
```

Choose your instance:

```text
cloudwatch-lab-ec2
```

Select:

```text
CPUUtilization
```

Click:

```text
Select Metric
```

---

## Configure Conditions

Choose:

```text
Threshold Type:
Static
```

Set:

```text
Whenever CPUUtilization is:

Greater than 70
```

Period:

```text
5 Minutes
```

Statistic:

```text
Average
```

Click:

```text
Next
```

---

# Step 6: Configure Notification

Alarm State:

```text
In Alarm
```

Select SNS Topic:

```text
cloudwatch-alerts-alaram
```

Click:

```text
Next
```

---

# Step 7: Alarm Details

Alarm Name:

```text
high-cpu-alaram
```

Description:

```text
Triggers when CPU utilization exceeds 70%
```

Click:

```text
Create Alarm
```

---

# Step 8: Verify Alarm

Go to:

```text
CloudWatch
→ Alarms
```

You should see:

```text
high-cpu-alaram

State:
OK
```

Meaning:

```text
CPU is below 70%
```

---

# Step 9: Connect to EC2

Using MobaXterm:

```text
Session
→ SSH
```

Host:

```text
13.233.47.184
```

Username:

```text
ec2-user
```

Private Key:

```text
aws hands on labs.pem
```

Connect.

---

# Step 10: Install Stress Tool

Run:

```bash
sudo dnf install stress -y
```

Verify installation completed successfully.

---

# Step 11: Generate CPU Load

Run:

```bash
stress --cpu 2 --timeout 600
```

Explanation:

```text
--cpu 2
Uses 2 CPU workers

--timeout 600
Runs for 10 minutes
```

Expected:

```text
stress: info: dispatching hogs: 2 cpu
```

Leave it running.

---

# Step 12: Verify CPU Usage

Run:

```bash
top
```

Expected:

```text
CPU utilization very high
```

Example:

```text
95%+
```

Press:

```text
q
```

to exit top.

---

# Step 13: Observe Alarm State Change

Go to:

```text
CloudWatch
→ Alarms
```

Wait approximately:

```text
5 minutes
```

Alarm changes:

```text
OK
↓
In Alarm
```

Example:

```text
high-cpu-alaram
State: In Alarm
```

This means CloudWatch detected high CPU usage.

---

# Step 14: Receive Email Notification

Check email inbox.

Expected email:

```text
ALARM: high-cpu-alaram
```

This confirms SNS integration is working.

---

# Step 15: Stop CPU Load

Press:

```text
Ctrl + C
```

or wait for timeout.

CPU utilization returns to normal.

---

# Step 16: Verify Alarm Recovery

Wait another:

```text
5 minutes
```

Alarm changes:

```text
In Alarm
↓
OK
```

Meaning:

```text
CPU usage is back below threshold
```

---

# Expected Results

## Initial State

```text
CPU < 70%
Alarm = OK
```

## During Stress Test

```text
CPU > 70%
Alarm = In Alarm
```

## After Stress Stops

```text
CPU < 70%
Alarm = OK
```

---

# Lab Cleanup

To avoid AWS charges:

## Terminate EC2

```text
EC2
→ Instances
→ Select Instance
→ Terminate
```

---

## Delete CloudWatch Alarm

```text
CloudWatch
→ Alarms
→ high-cpu-alaram
→ Delete
```

---

## Delete SNS Topic

```text
SNS
→ Topics
→ cloudwatch-alerts-alaram
→ Delete
```

---

# Key Commands Used

```bash
sudo dnf install stress -y
```

Install stress utility.

```bash
stress --cpu 2 --timeout 600
```

Generate CPU load.

```bash
top
```

Monitor CPU usage.

```bash
ps aux | grep stress
```

Verify stress process is running.

---

# Lab Summary

In this lab, we:

* Launched an EC2 instance
* Learned Basic vs Detailed Monitoring
* Created an SNS Topic
* Created a CloudWatch Alarm
* Monitored CPUUtilization
* Generated high CPU load using stress
* Triggered Alarm State (OK → In Alarm)
* Received notifications
* Observed alarm recovery (In Alarm → OK)
* Performed cleanup of AWS resources

**Outcome:** Successfully implemented AWS CloudWatch monitoring and alerting for an EC2 instance. ✅





![alt text](<cloudwatch lab/CW.windows-server1.png>)



![alt text](<cloudwatch lab/CWwindows-server-1.png>)


![alt text](<cloudwatch lab/CW.windows-server2.png>)


![alt text](<cloudwatch lab/CW.windows-server-2.png>)


![alt text](<cloudwatch lab/CW.windows-server3.png>)


![alt text](<cloudwatch lab/CW.windows-server-3.png>)

![alt text](<cloudwatch lab/CW.windows-server4.png>)




Great! ✅ Your **Windows Server CloudWatch Monitoring Lab** is completed.

Here is the complete beginner-level Markdown documentation.

```markdown
# AWS CloudWatch Windows Server Monitoring Lab

## Lab Purpose

The purpose of this lab is to learn how to monitor a Windows Server EC2 instance using Amazon CloudWatch.

In this lab we learn:

- How to launch a Windows Server EC2 instance
- How to configure RDP access
- How to enable CloudWatch Detailed Monitoring
- How to connect to Windows Server using Remote Desktop
- How to generate CPU load using a batch file
- How to create a CloudWatch CPU alarm
- How SNS notifications work with CloudWatch alarms
- How to test alarm states

---

# Lab Flow

```

Create Windows EC2 Instance
↓
Configure Security Group
(RDP + HTTP)
↓
Enable Detailed Monitoring
↓
Connect to Windows Server using RDP
↓
Create CPU Load Batch File
(a.bat)
↓
Monitor CPU Usage
↓
Create CloudWatch CPU Alarm
↓
CPU Usage Crosses Threshold
↓
CloudWatch Alarm Triggered
↓
SNS Notification Sent
↓
Stop CPU Load
↓
Alarm Returns to OK
↓
Cleanup Resources

```

---

# Architecture

```

Windows EC2 Instance
|
|
↓
CloudWatch Metrics
|
|
↓
CloudWatch Alarm
|
|
↓
SNS Topic
|
|
↓
Email Notification

```

---

# Step 1: Create Windows Server EC2 Instance

Go to:

```

AWS Console
→ EC2
→ Launch Instance

```

Configure:

```

Name:
Windows Server-2

AMI:
Windows Server

VPC:
Default VPC

Subnet:
ap-south-1a

Auto Assign Public IP:
Enable

```

Select:

```

Instance Type:
t3.micro

```

Select Key Pair:

```

aws hands on labs

```

Launch instance.

---

# Step 2: Configure Security Group

Create Security Group:

```

Name:
SG-123

```

Inbound Rules:

| Type | Port | Purpose |
|---|---|---|
| RDP | 3389 | Remote Desktop Access |
| HTTP | 80 | Web Traffic |

Example:

```

RDP
TCP
3389
Source: My IP

HTTP
TCP
80
Source: 0.0.0.0/0

```

---

# Step 3: Verify EC2 Instance

Go to:

```

EC2
→ Instances

```

Check:

```

Instance State:
Running

Status Check:
3/3 Passed

```

---

# Step 4: Enable Detailed Monitoring

Select:

```

Windows Server-2

```

Go to:

```

Monitoring
→ Manage Detailed Monitoring

```

Enable:

```

Detailed Monitoring

```

## Monitoring Difference

### Basic Monitoring

- Default
- Free
- Metrics every 5 minutes


### Detailed Monitoring

- Paid
- Metrics every 1 minute
- Better for production monitoring

---

# Step 5: Connect to Windows Server

Go to:

```

EC2
→ Windows Server-2
→ Connect

```

Choose:

```

RDP Client

```

Click:

```

Get Password

```

Upload:

```

aws hands on labs.pem

```

Decrypt password.

Credentials:

```

Username:
Administrator

Password:
Generated password

```

Open:

```

Remote Desktop Connection

```

Enter:

```

Public IPv4 Address

```

Login with Administrator credentials.

---

# Step 6: Create CPU Load Batch File

Inside Windows Server:

Right click Desktop:

```

New
→ Text Document

```

Rename:

```

a.bat

```

Important:

Change:

```

Save as type:
All Files

````

Open file and add:

```bat
:loop
start
goto loop
````

Save the file.

---

# Step 7: Run Batch File

Double click:

```
a.bat
```

This creates multiple processes and increases CPU utilization.

---

# Step 8: Check CPU Usage

Open:

```
Task Manager
→ Performance
→ CPU
```

Observe:

```
CPU Utilization %
```

During load:

```
CPU increases
```

---

# Step 9: Create CloudWatch Alarm

Open:

```
CloudWatch
→ Alarms
→ Create Alarm
```

Select Metric:

```
EC2
→ Per-Instance Metrics
→ Windows Server-2
→ CPUUtilization
```

---

# Step 10: Configure Alarm Conditions

Set:

```
Statistic:
Average

Period:
1 minute

Threshold:
Greater than 70%
```

Meaning:

```
If CPU > 70%
CloudWatch triggers alarm
```

---

# Step 11: Configure Notification

Select:

```
SNS Topic
```

Example:

```
cloudwatch-alerts-alaram
```

Alarm State:

```
In Alarm
```

SNS sends notification when alarm triggers.

---

# Step 12: Create Alarm Details

Alarm Name:

```
windows-high-cpu-alarm
```

Description:

```
Triggers when Windows Server CPU exceeds 70%
```

Create alarm.

---

# Step 13: Test Alarm

Initial state:

```
OK
```

After CPU load:

```
CPU > 70%
```

CloudWatch changes:

```
OK
      ↓
In Alarm
```

SNS sends notification.

---

# Step 14: Stop CPU Load

Stop batch file:

```
Close command windows
```

CPU returns to normal.

CloudWatch changes:

```
In Alarm
      ↓
OK
```

---

# Lab Results

Successfully completed:

✅ Windows EC2 deployment
✅ RDP connection
✅ Detailed Monitoring enabled
✅ CPU monitoring
✅ CloudWatch Alarm creation
✅ SNS notification setup
✅ CPU alarm testing

---

# Post Lab Cleanup

To avoid AWS charges:

## 1. Terminate Windows EC2

Go to:

```
EC2
→ Instances
→ Windows Server-2
→ Terminate
```

---

## 2. Delete CloudWatch Alarm

Go to:

```
CloudWatch
→ Alarms
→ Delete Alarm
```

---

## 3. Delete SNS Topic

Go to:

```
SNS
→ Topics
→ Delete Topic
```

---

## 4. Delete Security Group

Go to:

```
EC2
→ Security Groups
→ SG-123
→ Delete
```

---

# Key Learning Points

* EC2 Windows Server management
* RDP connectivity
* CloudWatch metrics
* Basic vs Detailed Monitoring
* CPU alarms
* SNS notifications
* AWS monitoring workflow

```

Your two CloudWatch labs are now documented:

1. ✅ Linux EC2 CloudWatch CPU Alarm Lab  
2. ✅ Windows Server CloudWatch Detailed Monitoring Lab  

These are good GitHub DevOps portfolio labs.
```
