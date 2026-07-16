
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



🔹 Step 10 (Cont.):- WAF Setup & Rules
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


