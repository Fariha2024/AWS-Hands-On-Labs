
## AWS Hands-On Labs


## 📂 Featured Labs Overview

### 🖥️ Lab 1: Rapid Application Deployment with AWS Lightsail

A hands-on implementation of Platform-as-a-Service (PaaS) utilizing AWS Lightsail to deploy a secure, cost-effective WordPress website.
* **Key Steps:** * Blueprint selection (Linux/Bitnami WordPress) and SSH key pair management.
  * AWS CloudShell integration for default credentials retrieval.
  * Public DNS mapping and administrative portal verification.



🔹 ![alt text](<aws class 41 lab/lightsail-lab/lightsail.step0.png>)



🔹 ![alt text](<aws class 41 lab/lightsail-lab/lightsail.step1.png>)



🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-2.png>)



🔹 ![alt text](<aws class 41 lab/lightsail-lab/lightsail.step3-4.png>)





🔵  PART 1: AWS LIGHTSAIL LAB

→ AWS Lightsail
↳ PaaS (Platform as a Service)

→ LAB for AWS Lightsail

🔹 Step 1:- Lightsail (search)
↓

→ Instances

→ create Instance

→ select a platform

• Linux apps

→ select a blueprint

• WordPress

→ Blueprint details

• Originally Packaged by Bitnami

→ SSH Key

→ create custom key

• My-Lightsail-key-123

→ choose your instance plan

→ select a plan type

• General purpose

→ select a network type

• Dual-stack

→ select a size

• $5 USD per month

→ Instance name

• WordPress-1




🔹Step 2: Lightsail

-> Instances

-> WordPress-1


-> click on

Retrieve default Password

-> WordPress credentials

  User

-> Access default password

-> step 1: click on

Launch cloudshell

_________________ (Password generate) ---> Copy <--- Paste 

-> step 2: Copy and paste this command into the cloudshell window

_________________ ---> copy ---> (flows up to Paste)




🔹 Step 3: Go to Web Portal
[Arrow Down]

search -------- Public IP


ex:- 13.126.46.165/wp-admin

-> Username

user

-> Password

_________________ <--- Paste 

seen yes ---> Welcome to WordPress!



🔹 Step 4: Go to web portal

search ---------> IP

Blog

seen yes -------> Hello world!

-----------x-----------

### AWS Lightsail Lab – Part 1 (Beginner Friendly)

#### Step 1: Open Lightsail

1. Login to AWS Console.
2. Search **Lightsail** in the search bar.
3. Click **Lightsail**.

---

#### Step 2: Create Instance

1. Click **Create instance**.

---

#### Step 3: Choose Platform

Under **Select a platform**:

✅ **Linux/Unix**

---

#### Step 4: Choose Blueprint

Under **Select a blueprint**:

✅ **WordPress**

You should see:

✅ **Originally packaged by Bitnami**

Leave it as default.

---

#### Step 5: Create SSH Key

1. Scroll to **SSH key pair manager**.
2. Click **Change SSH key pair** (or Create new key pair).
3. Click **Create new**.
4. Enter:

```text
My-Lightsail-key-123
```

5. Click **Create key pair**.
6. A `.pem` file will download automatically.

⚠️ Save this file safely. You may need it later for SSH access.

---

#### Step 6: Select Instance Plan

Under **Choose your instance plan**:

**Plan type**
✅ General purpose

**Network type**
✅ Dual-stack

**Size**
✅ $5 USD/month

---

#### Step 7: Name the Instance

Under **Identify your instance**:

Instance name:

```text
WordPress-1
```

---

#### Step 8: Create Instance

Click:

✅ **Create instance**

Wait 2–5 minutes.

Status will change from:

```text
Pending
```

to

```text
Running
```

---

### After Instance is Running

Send me a screenshot or tell me when **WordPress-1** shows **Running**, and I'll guide you through:

* Getting the public IP
* Opening the WordPress website
* Getting the WordPress admin password
* Logging into WordPress admin panel
* Final cleanup to avoid charges after the lab.



### Step 2: Retrieve WordPress Default Password

After **WordPress-1** is running:

1. Go to **Lightsail** → **Instances**.
2. Click **WordPress-1**.
3. Open the **Connect** tab (or look for **Retrieve default password**).
4. Click **Retrieve default password**.

You will see **WordPress credentials**.

### Step 1

Click:

**Launch CloudShell**

A terminal window will open.

### Step 2

On the password page, AWS will show a command similar to:

```bash
cat $HOME/bitnami_application_password
```

or another Bitnami/Lightsail command.

**Copy the exact command AWS displays** and **paste it into CloudShell**, then press **Enter**.

The terminal will output a password like:

```text
AbCd1234EfGh
```

Copy that password.

### WordPress Login Credentials

* Username: **user**
* Password: **(the password returned by CloudShell)**

If you can see the command AWS is showing, paste it here and I'll verify it before you run it.



### Step 3: Go to WordPress Web Portal

You have already completed this step. ✅

Follow these steps:

### 1. Open Browser

Search your **Public IP + /wp-admin**

Your URL:

```text
http://3.110.133.168/wp-admin
```

---

### 2. WordPress Login Page

Enter:

**Username**

```text
user
```

**Password**

```text
2bS543NFECFwYfZG
```

Click:

✅ **Log In**

---

### 3. Verify Success

You should see:

🎉 **Welcome to WordPress!**

and the **WordPress Dashboard**.

Your lab progress:

✅ Lightsail Instance Created
✅ WordPress Blueprint Installed
✅ SSH Key Created
✅ Default Password Retrieved
✅ WP Admin Login Completed

Next step in the lab will likely be WordPress configuration or Lightsail management. Send the next part.



### Step 4: Check WordPress Web Portal

Now you will verify that your WordPress website is working.

### 1. Open Browser

Search your **Public IP address only** (without `/wp-admin`):

```text
http://3.110.133.168
```

---

### 2. WordPress Website Opens

You should see the default WordPress site:

✅ **Blog**
✅ **Hello world!**

This confirms:

* WordPress is installed successfully ✅
* Lightsail instance is running ✅
* Web server is working ✅
* Website is publicly accessible ✅

Your Lightsail Lab progress:

✅ Step 1: Create Lightsail WordPress Instance
✅ Step 2: Retrieve Default Password
✅ Step 3: Login to WP Admin
✅ Step 4: Verify Public Website

Next step is usually WordPress customization, HTTPS setup, or cleanup. Send the next lab step.




## AWS Lightsail Lab – Post Cleanup Checklist

After finishing the lab, delete resources to avoid charges.

### 1. Delete Lightsail Instance

Go to:

**Lightsail → Instances**

Select:

```text
WordPress-1
```

Click:

```text
Delete
```

Confirm deletion.

✅ Instance deleted

---

### 2. Delete Static IP (if created)

Go to:

**Lightsail → Networking**

Check if any:

* Static IP
* IPv4 address attachment

exists.

If yes:

```text
Delete Static IP
```

✅ Static IP removed

---

### 3. Delete Snapshots (if created)

Go to:

**Lightsail → Snapshots**

Delete:

* Manual snapshots
* Automatic snapshots

✅ Snapshots removed

---

### 4. Delete Custom SSH Key (Optional)

Go to:

**AWS Account → SSH keys / Lightsail SSH keys**

Remove:

```text
my-lightsail-key-123
```

(if you don't need it for future labs)

✅ Key removed

---

### 5. Check Other AWS Regions

Lightsail is region-specific.

Check:

* Mumbai (ap-south-1)
* Any other region you used

Make sure no instances remain.

---

### Final Verification

Your Lightsail should show:

```
Instances: 0
Static IPs: 0
Snapshots: 0
```

Then you can safely logout. ✅

**Lab completed:**

* Created Lightsail WordPress VPS
* Generated SSH key
* Retrieved WordPress credentials
* Accessed WP Admin
* Verified website
* Cleaned resources



------------xxx------------


### 🛡️ Lab 2: Secure Web Infrastructure (VPC + ALB + EC2 + WAF)
A production-grade, multi-tier web application architecture featuring high-availability routing and centralized security controls.
* **VPC Networking:** Provisioned a custom VPC (`10.0.0.0/16`) spanning multiple Availability Zones with custom subnets, an Internet Gateway (IGW), and routing tables (`custom-RT`).
* **Compute & Web Server:** Deployed a Windows EC2 instance hosting an IIS (Internet Information Services) web server with custom web assets.
* **Load Balancing:** Configured an Application Load Balancer (ALB) and Target Groups with robust health check policies.
* **AWS WAF Integration:** Implemented an AWS Web Application Firewall (WAF) to filter incoming traffic. 
  * Configured **IP Sets** to block malicious IP ranges using `/32` subnet masks.
  * Created a **Web ACL (Protection Pack)** using custom rules to return `403 Forbidden` errors for blocked clients while keeping traffic open for legitimate users.



🔹 ![alt text](<aws class 41 lab/aws-WAF/waf0.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf1.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-2.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-3.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-4.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-5.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-6.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-7.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-8.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-9.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-10.png>)




🔹 ![alt text](<aws class 41 lab/aws-WAF/waf-11-12.png>)






## 📐 Architecture Topology

Below is the conceptual flow of the AWS WAF and Application Load Balancer setup:


[ Incoming Requests ]
│
▼
┌─────────┐
│ AWS WAF │ ──(Matches Block List?)──► [ ✗ Blocked IPs ] ──► (403 Forbidden / Logs)
└─────────┘
│
(Allowed)
│
▼
┌─────────┐
│   IGW   │ (Internet Gateway)
└─────────┘
│
▼
┌─────────┐
│  VPC-1  │
│  ┌──────┴────────────────────────┐
│  │ Public Subnets (1a & 1b)      │
│  │   ┌───────────────────────┐   │
│  │   │          ALB          │   │ (Application Load Balancer)
│  │   └──────────┬────────────┘   │
│  │              │                │
│  │              ▼                │
│  │   ┌───────────────────────┐   │
│  │   │      EC2 Instance     │   │ (Windows IIS Web Server)
│  │   │     (Web-Target-1)    │   │
│  │   └───────────────────────┘   │
│  └───────────────────────────────┘
└──────────────────────────────────┘



🔵 PART 2: AWS WEB APPLICATION FIREWALL (WAF) LAB
→ LAB for AWS Web Application Firewall


🔹 AWS WAF + ALB Lab — Purpose

Understand Web Application Security
              ↓
Learn How to Protect a Web Application
              ↓
Deploy Website on Windows Server (IIS)
              ↓
Use Application Load Balancer to Handle Traffic
              ↓
Place AWS WAF as Security Layer in Front of ALB
              ↓
Create Rules to Control Incoming Requests
              ↓
Block Malicious IP Addresses
              ↓
Prevent Excessive Requests Using Rate Limiting
              ↓
Allow Only Safe and Valid User Traffic
              ↓
Monitor Attacks and Traffic Using WAF Dashboard
              ↓
Build a Secure, Scalable and Protected Web Application



🔹 Shortly:
The purpose of this lab was to secure a web application using AWS WAF and Application Load Balancer, where we blocked malicious IPs, controlled unwanted traffic, and allowed legitimate users to access the website.


🔹 Step 1:- Create VPC ⟶ CSIR (CIDR)


① → Create VPC ⟶ 10.0.0.0/16

• VPC-1

② → Create Subnet

• public Subnet-1 ⟶ 10.0.1.0/24 ⟶ 1a

• public Subnet-2 ⟶ 10.0.2.0/24 ⟶ 1b

③ → Create Internet Gateway

• IGW-1 & attach to VPC (VPC-1)

④ → create Route Table

VPC-1 ──┬── Main Route Table ⟶ Main-RT (By default)
└── custom Route Table ⟶ custom-RT (Create)

→ Create custom Route Table

• custom-RT

Two Imp steps (Ⓐ & Ⓑ):

Ⓐ ⟶ Routes

• 0.0.0.0/0 ⟶ IGW-1

Ⓑ ⟶ Subnet association

• public subnet-1 ✓

• public subnet-2 ✓



🔹 Step 2:- Create Windows server
• Window Server-1

→ VPC

• VPC-1

→ Subnet

• public Subnet-1

→ Auto Assign Public IP

• Enable

→ security Group ⟶ All-Traffic-Allow-SG

• Allow All traffic



🔹 Step 3:- Connect windows server-1
↓

connect

Connect to your Windows instance using Remote Desktop with this information.

i-02be49e9419881137 (windows-server-1)
10.0.1.91
Administrator
z(Envjwi21U*tOO=ESVQCMu.DY%$;!EG


🔹 Step 4:- In Windows server-1, create a web page
→ Server Manager

↓

Add roles and features

↓

Install web server IIS (Installed)

→ This PC

→ C/drive

→ inetpub

→ wwwroot

_________________ { Copy and paste website files }



🔹 Step 5:- Go to web portal
↓

search ⟶ IP

↓

seen ⟶ (website (web page))

(seen yes) ✓



🔹 Step 6:- Create Target Group
→ Target Type

• Instances ✓

→ Target Group Name

• Web-Target-1

→ Protocol

• HTTP ✓

→ Port

• 80

→ Instance type

• IPv4


-> VPC

VPC-1

-> Advanced Health check settings

(same as it is --- (no changes))

-> Register targets

Window Server-1

click on include as pending below



🔹 Step 7:- Create Load Balancer
→ create

• Application Load Balancer

→ Load Balancer Name

• ALB-1

→ Scheme

• Internet facing ✓

→ Load Balancer IP address Type

• IPv4 ✓

→ Network Mapping

• VPC-1

→ Availability zones and Subnets

✓ ap-south-1a ──┬── { public subnet ✓ }

✓ ap-south-1b ──┘

→ Security Group (SG) (select)

• All-Traffic-Allow-SG

→ Listener and Mapping

• HTTP (Port = 80)

→ Target Group

• Web-Target-1


→ VPC

• VPC-1

→ Advanced Health check settings

(same as it is ── (no changes))

→ Register targets

• Window Server-1

↓

click on include as pending below ✓




🔹 Step 8:- Go to Web Portal
↓

search ⟶ DNS Name

↓

website (yes ✓) (search)

(seen yes ✓) ⟶ Website



🔹 Step 9:- WAF and shield
↓

→ IP sets

→ create IP address sets

→ IP set name

• AWS-Batch-IPs

→ Scope

• Regional

→ Description

• All these Users IPs are blocked

→ IP version

• IPv4

→ IP address { copy and paste all IPs those are blocked }

• _____________/32,

• _____________/32,

• _____________/32,

• _____________/32, ( If taking a single IP, then we use /32 ✓ )




🔹 Step 10:- WAF and shield
↓

→ protection packs (web ACLs)

→ Create protection pack (Web ACL)

→ App category

• connect & publishing systems

→ App focus

• Web

 WAF Setup & Rules

→ Add resources

→ Add regional resources

→ Resources

• ALB-1 ✓ (Add)

→ choose initial protection

→ Essential rules ✓

→ Name and describe

→ Name

• Web-ACL-1

→ Description

• AWS 1 Jan Batch demo

→ Customize protection pack (Web ACL)

→ IP address

→ IP set for address to block

• AWS-Batch-IPs

→ IP address to block

• _________________ { Here shows, this IPs are blocked to my firewall }




🔹 Step 11:- Go to web portal
↓

search ⟶ DNS Name

(see ⟶ No ✗) ⟶ IPs are blocked

↓

error ⟶ 403 Forbidden

(see ⟶ yes ✓) ⟶ IPs allows (remaining all) are seen ✓



🔹 Step 12:- WAF and shield
↓

→ protection packs (WebACLs)

→ Web-ACL-1

↓

→ view dashboard, logs and sampled requests

↓

→ sampled requests

→ Metric Name

• Web-ACL-1

Action { All Allow and Block IPs are shown }




---

## 📝 Key Takeaways
1. **Defense in Depth:** Secured web applications at the perimeter using AWS WAF prior to traffic ever hitting backend servers.
2. **High Availability:** Leveraged Load Balancers and target groups to prepare environments for seamless horizontal scaling.
3. **Infrastructure Control:** Hand-configured networking tables, subnets, and security groups to adhere to the principle of least privilege.



Let's create this **AWS VPC Lab step-by-step**. We'll build:

* VPC: `VPC-1` → `10.0.0.0/16`
* Public Subnet-1 → `10.0.1.0/24` (AZ 1a)
* Public Subnet-2 → `10.0.2.0/24` (AZ 1b)
* Internet Gateway: `IGW-1`
* Route Table: `custom-RT`
* Make both subnets public

---

## 🔹 Step 1: Create VPC

1. Login to AWS Console.

2. Search:

```
VPC
```

3. Open:

```
VPC Dashboard
```

4. Click:

```
Create VPC
```

5. Select:

```
VPC only
```

6. Fill:

**Name tag**

```
VPC-1
```

**IPv4 CIDR block**

```
10.0.0.0/16
```

7. Leave:

```
IPv6 CIDR block → No IPv6 CIDR block
Tenancy → Default
```

8. Click:

```
Create VPC
```

✅ VPC created.

---

# 🔹 Step 2: Create Public Subnet-1

1. Left menu → click:

```
Subnets
```

2. Click:

```
Create subnet
```

3. Select:

```
VPC ID → VPC-1
```

4. Subnet settings:

**Subnet name**

```
public-subnet-1
```

**Availability Zone**

Choose:

```
us-east-1a
```

(or your region's first AZ)

**IPv4 subnet CIDR block**

```
10.0.1.0/24
```

5. Click:

```
Create subnet
```

---

# 🔹 Step 3: Create Public Subnet-2

Again:

```
Create subnet
```

Select:

```
VPC-1
```

Fill:

**Subnet name**

```
public-subnet-2
```

Availability Zone:

```
us-east-1b
```

CIDR:

```
10.0.2.0/24
```

Click:

```
Create subnet
```

✅ Two subnets created.

---

# 🔹 Step 4: Create Internet Gateway

1. Left menu:

```
Internet Gateways
```

2. Click:

```
Create internet gateway
```

3. Name:

```
IGW-1
```

4. Click:

```
Create internet gateway
```

---

## Attach IGW to VPC

After creation:

1. Select:

```
IGW-1
```

2. Click:

```
Actions
```

3. Select:

```
Attach to VPC
```

4. Choose:

```
VPC-1
```

5. Click:

```
Attach internet gateway
```

✅ IGW attached.

---

# 🔹 Step 5: Create Custom Route Table

1. Left menu:

```
Route Tables
```

2. Click:

```
Create route table
```

3. Enter:

Name:

```
custom-RT
```

VPC:

```
VPC-1
```

4. Click:

```
Create route table
```

---

# 🔹 Step 6A: Add Route to Internet Gateway

Open:

```
custom-RT
```

Go to:

```
Routes tab
```

Click:

```
Edit routes
```

Click:

```
Add route
```

Add:

Destination:

```
0.0.0.0/0
```

Target:

```
Internet Gateway
```

Choose:

```
IGW-1
```

Click:

```
Save changes
```

✅ Now traffic goes to the internet.

---

# 🔹 Step 6B: Associate Subnets

Inside:

```
custom-RT
```

Go to:

```
Subnet associations
```

Click:

```
Edit subnet associations
```

Tick:

✅ public-subnet-1

✅ public-subnet-2

Click:

```
Save associations
```

---

# 🔹 Step 7: Enable Public IP (Important)

Go to:

```
Subnets
```

Select:

```
public-subnet-1
```

Click:

```
Actions
→ Edit subnet settings
```

Enable:

✅ Auto-assign public IPv4 address

Save.

Repeat for:

```
public-subnet-2
```

---

## Final Architecture:

```
                 Internet
                    |
                 IGW-1
                    |
                 VPC-1
              10.0.0.0/16
                    |
        -------------------------
        |                       |
 public-subnet-1        public-subnet-2
 10.0.1.0/24             10.0.2.0/24
    AZ-1a                  AZ-1b
        \                 /
             custom-RT
          0.0.0.0/0 → IGW-1
```

When you finish **Step 1 (Create VPC)**, tell me "done" and I'll guide you to the next step.



Great. Now we continue with **Step 2: Create Windows Server EC2 Instance** inside your VPC.

Your target:

```
EC2 Instance:
Windows Server-1

VPC:
VPC-1

Subnet:
public-subnet-1 (10.0.1.0/24)

Public IP:
Enabled

Security Group:
All-Traffic-Allow-SG
(Allow All Traffic)
```

---

# 🔹 Step 2: Launch Windows Server EC2

## ① Open EC2

1. AWS Console → Search:

```
EC2
```

2. Open:

```
EC2 Dashboard
```

3. Click:

```
Launch instance
```

---

# ② Name and Tags

Under **Name** enter:

```
Windows-Server-1
```

---

# ③ Choose AMI (Operating System)

Under **Application and OS Images (AMI)**:

Select:

```
Windows
```

Choose:

```
Microsoft Windows Server 2022 Base
```

(Windows Server 2019 is also fine if your teacher wants that.)

---

# ④ Instance Type

Choose:

```
t2.micro
```

or if unavailable:

```
t3.micro
```

(Free tier eligible if available.)

---

# ⑤ Key Pair

For Windows you need a key pair to get the Administrator password.

Click:

```
Create new key pair
```

Name:

```
Windows-Key-1
```

Type:

```
RSA
```

Format:

```
.pem
```

Click:

```
Create key pair
```

Save the `.pem` file safely.

---

# ⑥ Network Settings

Click **Edit**.

## VPC:

Select:

```
VPC-1
```

Should show:

```
10.0.0.0/16
```

---

## Subnet:

Select:

```
public-subnet-1
```

Should be:

```
10.0.1.0/24
AZ: ap-southeast-1a
```

---

## Auto Assign Public IP:

Enable:

```
Enable
```

✅ Important because this is a public subnet.

---

# ⑦ Security Group

Choose:

```
Create security group
```

Security group name:

```
All-Traffic-Allow-SG
```

Description:

```
Allow All Traffic
```

---

## Add Rules

For lab purposes:

### Type:

```
All traffic
```

### Protocol:

```
All
```

### Port:

```
All
```

### Source:

Choose:

```
Anywhere IPv4
```

It becomes:

```
0.0.0.0/0
```

⚠️ This is only for learning labs. In real production, don't allow all traffic.

---

# ⑧ Storage

Keep default:

```
30 GiB
gp3
```

---

# ⑨ Launch

Click:

```
Launch instance
```

Wait until:

```
Instance state: Running
```

---

# ⑩ Verify

Go to:

```
EC2 → Instances
```

You should see:

```
Windows-Server-1
```

with:

```
VPC:
VPC-1

Subnet:
public-subnet-1

Public IPv4:
Yes

Security Group:
All-Traffic-Allow-SG
```

---

After it becomes **Running**, tell me **"Windows server created"** and we will do the next step: **Connect to Windows using RDP**.



Great. Now we will connect to your **Windows-Server-1** using **RDP (Remote Desktop Protocol)**.

---

# 🔹 Step 3: Connect Windows Server-1

## ① Open EC2 Instances

1. AWS Console → Search:

```text
EC2
```

2. Go to:

```text
Instances
```

3. Select:

```text
Windows-Server-1
```

---

## ② Get Administrator Password

1. Click:

```text
Connect
```

2. Choose:

```text
RDP client
```

3. Click:

```text
Get password
```

4. Click:

```text
Upload private key file
```

5. Select your key:

```text
Windows-Key-1.pem
```

6. Click:

```text
Decrypt password
```

You will see:

```
Username:
Administrator

Password:
xxxxxxxxxxxxxxxx
```

Copy the password.

---

## ③ Download RDP File

Still on **RDP client** tab:

Click:

```text
Download remote desktop file
```

It downloads:

```
Windows-Server-1.rdp
```

---

## ④ Connect From Your Computer

### On Windows PC:

1. Open the downloaded:

```
Windows-Server-1.rdp
```

2. Click:

```
Connect
```

3. Enter:

```
Username:
Administrator
```

4. Paste the decrypted password.

5. Accept certificate warning.

---

## ⑤ Verify Connection

You should see:

```
Windows Server Desktop
```

Your server is now connected.

---

### If RDP fails, check:

EC2 → Security Group:

```
All-Traffic-Allow-SG
```

Should have:

```
Type: RDP
Port: 3389
Source: Your IP
```

(or for your lab: All Traffic)

---

After you successfully enter the Windows desktop, tell me:

**"Windows connected"**

Then we continue to the next lab step. ✅




Great, now we continue with **Step 4: Install IIS and Create a Web Page on Windows Server-1**.

You are already connected to the Windows Server desktop.

---

# 🔹 Step 4: Create Web Page in Windows Server-1

## ① Open Server Manager

1. On Windows Server desktop, open:

```text
Server Manager
```

2. Wait for it to load.

---

## ② Add IIS Web Server Role

1. In Server Manager click:

```text
Manage
```

(top right)

2. Select:

```text
Add Roles and Features
```

3. Click:

```text
Next
```

---

## ③ Installation Type

Select:

```text
Role-based or feature-based installation
```

Click:

```text
Next
```

---

## ④ Server Selection

Choose your server:

```text
Windows-Server-1
```

Click:

```text
Next
```

---

## ⑤ Server Roles

Tick:

```text
Web Server (IIS)
```

A popup appears:

```text
Add features required for Web Server (IIS)?
```

Click:

```text
Add Features
```

Then:

```text
Next
```

---

## ⑥ Features

Leave default.

Click:

```text
Next
```

---

## ⑦ Web Server Role Services

Leave default settings.

Click:

```text
Next
```

---

## ⑧ Confirm Installation

Click:

```text
Install
```

Wait until:

```text
Installation succeeded
```

Click:

```text
Close
```

---

# 🔹 Step 5: Add Website Files

Now open:

```text
This PC
```

Go to:

```text
C:\
```

Open:

```text
inetpub
```

Open:

```text
wwwroot
```

Full path:

```text
C:\inetpub\wwwroot
```

---

## Create your webpage

Inside **wwwroot**:

1. Right-click → New → Text Document

Rename:

```text
index.html
```

⚠️ Make sure it is not:

```text
index.html.txt
```

---

## Edit index.html

Open it with Notepad and paste:

```html
<html>
<head>
<title>AWS IIS Lab</title>
</head>

<body>
<h1>Welcome to Windows Server-1 IIS Web Server</h1>
<p>This website is hosted on AWS EC2 Windows Server.</p>
</body>

</html>
```

Save.

---

# 🔹 Test IIS Website

On the Windows Server:

Open browser:

```text
Internet Explorer / Edge
```

Enter:

```text
http://localhost
```

You should see your webpage.

---

# 🔹 Access From Your Laptop

Get your EC2 public IP:

AWS Console:

```text
EC2 → Instances → Windows-Server-1
```

Copy:

```text
Public IPv4 address
```

Open on your own computer browser:

```
http://YOUR_PUBLIC_IP
```

Example:

```
http://13.xxx.xxx.xxx
```

Your IIS webpage should open. ✅

---

After IIS is installed, tell me **"IIS installed"** and we will configure the Security Group for HTTP (port 80) so the website is reachable from the internet.




Great, now we continue with **Step 6: Create Target Group** for your Windows IIS server.

Target Group purpose:

* It will register your EC2 Windows Server
* Load Balancer will send HTTP traffic to this target

---

# 🔹 Step 6: Create Target Group

## ① Open Target Groups

1. AWS Console → Search:

```text
EC2
```

2. Left menu:

```text
Load Balancing
→ Target Groups
```

3. Click:

```text
Create target group
```

---

# ② Choose Target Type

Under **Target type** select:

✅

```text
Instances
```

---

# ③ Target Group Name

Enter:

```text
Web-Target-1
```

---

# ④ Protocol and Port

Set:

**Protocol**

```text
HTTP
```

**Port**

```text
80
```

---

# ⑤ IP Address Type

Select:

```text
IPv4
```

---

# ⑥ VPC Selection

Choose your VPC:

```text
VPC-1
```

(Important: It must be the same VPC where Windows-Server-1 exists.)

---

# ⑦ Health Check

Leave default:

Protocol:

```text
HTTP
```

Path:

```text
/
```

Port:

```text
Traffic port
```

---

# ⑧ Register Targets

You will see your instance:

```text
Windows-Server-1
```

Select:

✅ Windows-Server-1

Click:

```text
Include as pending below
```

Then click:

```text
Create target group
```

---

## Final Target Group should look like:

```text
Target Group:
Web-Target-1

Target Type:
Instances

Protocol:
HTTP

Port:
80

VPC:
VPC-1

Registered Target:
Windows-Server-1
```

After creating it, tell me **"Target Group created"** and we will create the **Application Load Balancer (ALB)** next. ✅



## 🔹 Step 7: Create Application Load Balancer (ALB) — Beginner Level

A **Load Balancer** distributes incoming traffic to your servers. Here we will create an **Application Load Balancer (ALB)** and connect it with our Windows Server.

---

### ✅ Step 1: Open Load Balancer Page

1. Open **AWS Console**
2. Go to:

```
EC2
 ↓
Load Balancers
 ↓
Create Load Balancer
```

3. Select:

```
Application Load Balancer
```

4. Click:

```
Create
```

---

## ✅ Step 2: Basic Configuration

### Load Balancer Name

Enter:

```
ALB-1
```

---

### Scheme

Select:

```
Internet-facing ✓
```

Meaning:

* Users from the internet can access your application.

---

### IP Address Type

Select:

```
IPv4 ✓
```

---

# ✅ Step 3: Network Mapping

### VPC

Select:

```
VPC-1
```

---

### Availability Zones

Select **two Availability Zones**:

First:

```
ap-south-1a
```

Choose:

```
Public Subnet ✓
```

Second:

```
ap-south-1b
```

Choose:

```
Public Subnet ✓
```

Example:

```
ap-south-1a
      |
      └── Public Subnet

ap-south-1b
      |
      └── Public Subnet
```

Why two?

* If one Availability Zone fails, the other can handle traffic.

---

# ✅ Step 4: Security Group

Under Security Groups:

Select:

```
All-Traffic-Allow-SG ✓
```

This allows traffic to reach the Load Balancer.

---

# ✅ Step 5: Listener Configuration

Listener means which port the Load Balancer listens on.

Set:

```
Protocol: HTTP
Port: 80
```

Example:

```
User
 |
 | HTTP :80
 ↓
Application Load Balancer
```

---

# ✅ Step 6: Select Target Group

Target Group = The servers where ALB sends traffic.

Select:

```
Web-Target-1
```

---

# ✅ Step 7: Health Check Settings

Health check checks whether your server is working.

Keep default settings:

```
Protocol: HTTP

Path: /

Port: Traffic Port
```

Do not change anything.

---

# ✅ Step 8: Register Targets

Now select your server.

You will see:

```
Instances

☐ Windows Server-1
```

Do:

1. Tick the checkbox:

```
✓ Windows Server-1
```

2. Click:

```
Include as pending below
```

Now it should appear under:

```
Registered targets
```

Example:

```
Windows Server-1
Port: 80
Status: Pending
```

---

# ✅ Step 9: Create Load Balancer

Scroll down.

Click:

```
Create Load Balancer
```

Wait a few minutes.

---

# ✅ Step 10: Check ALB Status

Go to:

```
EC2
 ↓
Load Balancers
```

Find:

```
ALB-1
```

Check:

```
State: Active ✅
```

---

# ✅ Step 11: Test Website

Click:

```
ALB-1
```

Copy:

```
DNS name
```

Example:

```
ALB-1-xxxx.ap-south-1.elb.amazonaws.com
```

Open browser:

```
http://ALB-1-xxxx.ap-south-1.elb.amazonaws.com
```

If your IIS page opens:

✅ Load Balancer is working
✅ Target Group is working
✅ Windows Server is connected 🎉



## 🔹 Step 9: Create WAF IP Set — Beginner Level

**AWS WAF (Web Application Firewall)** protects your website by blocking unwanted traffic.
Here we create an **IP Set** containing IP addresses that we want to block.

---

# ✅ Step 1: Open AWS WAF

1. Open **AWS Console**
2. Search:

```text
WAF
```

3. Open:

```text
AWS WAF
```

---

# ✅ Step 2: Go to IP Sets

From the left menu:

```text
AWS WAF
    ↓
IP sets
```

Click:

```text
Create IP set
```

---

# ✅ Step 3: Configure IP Set

### IP set name

Enter:

```text
AWS-Batch-IPs
```

Example:

```
Name: AWS-Batch-IPs
```

---

### Scope

Select:

```text
Regional ✓
```

Meaning:

* Used for regional resources like:

  * Application Load Balancer (ALB)
  * API Gateway
  * App Runner

---

### Description

Enter:

```text
All these Users IPs are blocked
```

---

### IP Version

Select:

```text
IPv4 ✓
```

---

# ✅ Step 4: Add Blocked IP Addresses

In the IP address box, enter the IPs you want to block.

Example:

```
192.168.1.10/32
203.0.113.5/32
45.67.89.100/32
172.16.5.20/32
```

---

### What does `/32` mean?

`/32` means:

✅ Block only **one specific IP address**

Example:

```
192.168.1.10/32
```

Blocks only:

```
192.168.1.10
```

It does NOT block the whole network.

---

### CIDR Examples:

Single IP:

```
10.0.0.5/32
```

Block multiple IPs:

```
10.0.0.5/32
10.0.0.6/32
10.0.0.7/32
```

Block a range:

```
10.0.0.0/24
```

(blocks 256 IP addresses)

---

# ✅ Step 5: Create IP Set

After adding IPs:

Click:

```text
Create IP set
```

You should see:

```
AWS-Batch-IPs
Status: Active
```

---

### Next Step (after creating IP Set)

You will attach this IP Set to a **WAF Web ACL rule**:

```
User Request
       |
       ↓
Application Load Balancer
       |
       ↓
AWS WAF
       |
       ↓
Check IP Set
       |
       ↓
Block / Allow Traffic
```

Blocked IPs → ❌ Denied
Other users → ✅ Allowed



After **Step 9 (Create IP Set)**, the next step is **Step 10: Create Web ACL and attach WAF rules**.

So the order is:

---

# 🔹 Step 10: WAF Setup & Rules (Start)

## ✅ 1. Create Protection Pack (Web ACL)

Go to:

```text
AWS WAF
 ↓
Protection packs (Web ACLs)
 ↓
Create protection pack (Web ACL)
```

---

## ✅ 2. Application Category

Select:

```text
App category
→ Connect & publishing systems
```

---

## ✅ 3. Application Focus

Select:

```text
App focus
→ Web
```

Click:

```text
Next
```

---

## ✅ 4. Add Resources

Choose:

```text
Add regional resources
```

Under Resources:

Select:

```text
✓ ALB-1
```

Click:

```text
Add
```

---

## ✅ 5. Choose Initial Protection

Select:

```text
✓ Essential rules
```

---

## ✅ 6. Name and Describe

Name:

```text
Web-ACL-1
```

Description:

```text
AWS 1 Jan Batch demo
```

---

## ✅ 7. Customize Protection Pack (Web ACL)

Add your IP blocking rule:

Choose:

```text
IP address
```

Select:

```text
IP set for address to block
```

Choose:

```text
AWS-Batch-IPs
```

Now WAF will use the IPs you created in Step 9.

---

## ✅ 8. Create Web ACL

Click:

```text
Create protection pack
```

---

So the exact flow is:

```
Step 9
Create IP Set
        ↓
Step 10
Create Web ACL
        ↓
Add ALB-1
        ↓
Add Essential Rules
        ↓
Attach AWS-Batch-IPs
        ↓
Create Web ACL
```

Step 9 **always comes first**, because Step 10 needs the IP Set (`AWS-Batch-IPs`) to create the blocking rule.



## 🔹 Step 11: Test WAF Protection from Web Portal — Beginner Level

Now we will check whether **AWS WAF is blocking and allowing traffic correctly**.

---

# ✅ Step 1: Get ALB DNS Name

Go to:

```text
EC2
 ↓
Load Balancers
 ↓
ALB-1
```

Copy:

```text
DNS Name
```

Example:

```text
ALB-1-123456.ap-south-1.elb.amazonaws.com
```

---

# ✅ Step 2: Open Website

Open browser and paste:

```text
http://ALB-1-xxxx.ap-south-1.elb.amazonaws.com
```

---

# ✅ Step 3: Check Result

### Case 1: Blocked IP

If your current IP is added inside:

```text
AWS-Batch-IPs
```

WAF will block you.

You will see:

```text
403 Forbidden
```

Meaning:

❌ IP blocked by AWS WAF

---

### Case 2: Allowed IP

If your IP is NOT inside:

```text
AWS-Batch-IPs
```

You will see:

✅ Your website page (IIS page)

Example:

```text
Welcome to IIS
```

Meaning:

✅ WAF allowed your request
✅ ALB forwarded traffic to Windows Server

---

Your final traffic flow:

```text
User
 |
 | HTTP Request
 ↓
Application Load Balancer (ALB-1)
 |
 ↓
AWS WAF Web ACL
 |
 ├── Blocked IP → 403 Forbidden ❌
 |
 └── Allowed IP → Windows Server IIS Page ✅
```

If you get **403**, your WAF is working correctly. 🎉




## 🔹 Step 12: View AWS WAF Dashboard, Logs & Sampled Requests — Beginner Level

This step is used to **check WAF activity** and see which requests were **allowed or blocked**.

---

# ✅ Step 1: Open AWS WAF

Go to:

```text
AWS Console
 ↓
WAF
 ↓
Protection packs (Web ACLs)
```

---

# ✅ Step 2: Open Your Web ACL

Select:

```text
Web-ACL-1
```

---

# ✅ Step 3: Open Dashboard

Click:

```text
View dashboard, logs and sampled requests
```

Here you can see:

* Allowed requests ✅
* Blocked requests ❌
* Total traffic
* WAF metrics

---

# ✅ Step 4: Open Sampled Requests

Go to:

```text
Sampled requests
```

This shows recent requests inspected by AWS WAF.

---

# ✅ Step 5: Check Metric Name

You should see:

```text
Metric Name:
Web-ACL-1
```

---

# ✅ Step 6: Check Action

Under **Action**, you will see:

### Allowed traffic:

```text
ALLOW ✅
```

Meaning:

* User IP is not blocked
* Request passed WAF

---

### Blocked traffic:

```text
BLOCK ❌
```

Meaning:

* IP matched your AWS-Batch-IPs rule
* WAF denied access

---

Example:

| IP Request                     | Action  |
| ------------------------------ | ------- |
| Normal User IP                 | ALLOW ✅ |
| AWS-Batch-IPs                  | BLOCK ❌ |
| Too many requests (Rate Limit) | BLOCK ❌ |

---

Your final WAF verification:

```text
User Request
      |
      ↓
ALB-1
      |
      ↓
AWS WAF Web-ACL-1
      |
      ├── Allowed → Windows IIS Page ✅
      |
      └── Blocked → 403 Forbidden ❌
```

If you see **ALLOW and BLOCK actions** in Sampled Requests, your WAF setup is working correctly. ✅




## AWS ALB + WAF Lab — Post Cleanup Key Points

* ✅ Delete **Application Load Balancer (ALB)**

  * `alb1`

* ✅ Delete **Target Group**

  * `web-target-one`

* ✅ Delete **AWS WAF Web ACL**

  * `web-acl-1`

* ✅ Delete WAF auto-created **IP Sets**

  * `web-acl-1_IPV4_Allow`
  * `web-acl-1_IPV4_Block`
  * `web-acl-1_IPV6_Allow`
  * `web-acl-1_IPV6_Block`

* ✅ Terminate EC2 instances

  * `windows-server-1`

* ✅ Delete unused EBS volumes

  * Root volume after EC2 termination

* ✅ Delete leftover Network Interfaces (ENI)

* ✅ Delete custom subnets

  * `public-subnet-one` (AZ 1a)
  * `public-subnet-two` (AZ 1b)

* ✅ Delete custom Internet Gateway

* ✅ Delete custom Route Tables

* ✅ Delete custom Network ACL

* ✅ Delete custom Security Groups

* ✅ Delete custom VPC

  * `vpc-one`

* ✅ Final verification:

  * No running EC2 instances
  * No ALB
  * No Target Groups
  * No WAF resources
  * No unused volumes
  * No NAT Gateway
  * No extra Elastic IPs

**Keep AWS default VPC resources unless you intentionally want to remove them.**
