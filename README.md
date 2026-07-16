



![alt text](<aws class 41 lab/lightsail-lab/lightsail.step0.png>)



![alt text](<aws class 41 lab/lightsail-lab/lightsail.step1.png>)



![alt text](<aws class 41 lab/aws-WAF/waf-2.png>)



![alt text](<aws class 41 lab/lightsail-lab/lightsail.step3-4.png>)





PART 1: AWS LIGHTSAIL LAB
→ AWS Lightsail
↳ PaaS (Platform as a Service)

→ LAB for AWS Lightsail
Step 1:- Lightsail (search)
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









Step 2: Lightsail

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


Step 3: Go to Web Portal
[Arrow Down]

search -------- Public IP


ex:- 13.126.46.165/wp-admin

-> Username

user

-> Password

_________________ <--- Paste 

seen yes ---> Welcome to WordPress!



Step 4: Go to web portal

search ---------> IP

Blog

seen yes -------> Hello world!

-----------x-----------------





![alt text](<aws class 41 lab/aws-WAF/waf0.png>)




![alt text](<aws class 41 lab/aws-WAF/waf1.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-2.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-3.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-4.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-5.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-6.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-7.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-8.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-9.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-10.png>)




![alt text](<aws class 41 lab/aws-WAF/waf-11-12.png>)






PART 2: AWS WEB APPLICATION FIREWALL (WAF) LAB
→ LAB for AWS Web Application Firewall
Step 1:- Create VPC ⟶ CSIR (CIDR)
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

Step 2:- Create Windows server
• Window Server-1

→ VPC

• VPC-1

→ Subnet

• public Subnet-1

→ Auto Assign Public IP

• Enable

→ security Group ⟶ All-Traffic-Allow-SG

• Allow All traffic



Step 3:- Connect windows server-1
↓

connect

Step 4:- In Windows server-1, create a web page
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

Step 5:- Go to web portal
↓

search ⟶ IP

↓

seen ⟶ (website (web page))

(seen yes) ✓

Step 6:- Create Target Group
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







Step 7:- Create Load Balancer
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

Step 8:- Go to Web Portal
↓

search ⟶ DNS Name

↓

website (yes ✓) (search)

(seen yes ✓) ⟶ Website



Step 9:- WAF and shield
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

Step 10:- WAF and shield
↓

→ protection packs (web ACLs)

→ Create protection pack (Web ACL)

→ App category

• connect & publishing systems

→ App focus

• Web

Step 10 (Cont.):- WAF Setup & Rules
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

Step 11:- Go to web portal
↓

search ⟶ DNS Name

(see ⟶ No ✗) ⟶ IPs are blocked

↓

error ⟶ 403 Forbidden

(see ⟶ yes ✓) ⟶ IPs allows (remaining all) are seen ✓

Step 12:- WAF and shield
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

—— X ——







Step 7:- Create Load Balancer

-> create

Application Load Balancer

-> Load Balancer Name

ALB-1

-> Scheme

Internet facing 

-> Load Balancer IP address type

IPv4

-> Network Mapping

VPC-1

-> Availability zones and subnets

 ap-south-1a \

 ap-south-1b /  { public subnet }

-> Security Group (SG)

All-Traffic-Allow-SG (select)

-> Listener and Mapping

HTTP (Port = 80)

-> Target Group

Web-Target-1







Step 8:- Go to Web Portal

search ----------> DNS Name

website yes  search

seen yes  ---> website



Step 9:- WAF and shield


-> IP sets

-> create IP address sets

-> IP set name

AWS-Batch-IPs

-> Scope

Regional

-> Description

All these Users IPs are blocked

-> IP version

IPv4

-> IP address

_____________/32, { copy and paste all IPs those are blocked }

_____________/32,

_____________/32,

_____________/32, If taking a single IP, then we use /32 




Step 10:- WAF and shield


-> protection packs (Web ACLs)

-> Create protection pack (Web ACL)

-> App category

connect & publishing systems

-> App focus

Web




-> Add resources

-> Add regional resources

-> Resources

    ALB-1 

-> Choose initial protection

-> Essential rules

-> Name and describe

-> Name: Web-ACL-1

-> Description: AWS 1 Jan Batch demo

-> Customize protection pack (Web ACL)

-> IP address

-> IP set for address to block: AWS-Batch-IPs

-> IP address to block:
{ Here shows, this IPs are blocked to my firewall }



Step 11: Go to web portal


- Search -------------> DNS Name

- See -----> No [X] ---> IPs are blocked

- Error ---> 403 Forbidden

- (See ---------> Yes ---------- ---> IPs allowed (remaining all) are seen 



Step 12: WAF and Shield


-> Protection packs (WebACLs)

-> Web-ACL-1

-> View dashboard, logs and sampled requests

-> Sampled requests

-> Metric Name: Web-ACL-1

Action: { All Allow and Block IPs are shown }






Step 2: Lightsail
[Arrow Down]

-> Instances

-> WordPress-1

[Arrow Down]

-> click on [v]

Retrieve default Password

-> WordPress credentials

User

-> Access default password

-> step 1: click on [v]

Launch cloudshell

_________________ (Password generate) ---> Copy <--- (Paste v)

-> step 2: Copy and paste this command into the cloudshell window

_________________ ---> (copy) ---> (flows up to Paste)

Step 3: Go to Web Portal
[Arrow Down]

search ---> Public IP

[Arrow Down]

ex:- 13.126.46.165/wp-admin

[Arrow Down]

-> Username

user

-> Password

_________________ <--- (Paste v)

(seen yes v) ---> Welcome to WordPress!

Step 4: Go to web portal
[Arrow Down]

search ---> IP

[Arrow Down]

Blog

(seen yes v) ---> Hello world!

—— X ——