Diagram 1: Hub and Spoke Model (Centralized Hub)
This diagram illustrates the high-level architecture of the network, showing how the central Transit Gateway acts as the hub for the six surrounding spoke VPCs.


![alt text](tgw-01.png)



Diagram 2: Transit Gateway Route Table and Connectivity
This diagram details the actual connectivity and routing logic. I have replicated the logical VPC placements and all specific route table updates, CIDR blocks (IP ranges), and subnet details from your notes, focusing on the configuration of the Transit Gateway and its four connected VPCs (1, 2, 3, and 4).



![alt text](tgw-02.png)



---

## VPC Flow Logs

* Flow logs can be create on S3 bucket or cloudwatch.

VPC के अंदर आने वाले हर Request की information, Monitor करेगा, Logs बनाकर collect करेगा store in S3 bucket.

### **VPC1 10.0.0.0/16**

* **Subnet 1:** 10.0.1.0/24
* **EC2:** Web server
* **IGW:** Internet Gateway
* **Inbound Traffic** from Internet.

---

### **Monitor**

* Logs $\rightarrow$ Store in S3 bucket.
* (हर आने वाली Request की information)

---

### **Route Table**

| local |  |
| --- | --- |
|  |  |

---

### **Interview Question**

**Q1)** VPC flow logs Enable कर दिया है तो क्या मै Specific IP को blocked कर सकता हूँ कि उसकी Request आगे ही ना (No entry) ?

**Ans:-** NO ❌
(Flow logs में सारे logs maintain होते हैं, Not blocked.

---

## Architecture Diagram (Markdown Text Format)


![alt text](tgw-03.png)


---

### **Core Logic Highlighted from Notes:**

* **Specific IP $\rightarrow$ Block या Reject या Stop $\rightarrow$ No ❌**
* *Reasoning:* VPC Flow Logs are strictly a monitoring and diagnostic tool. They record network traffic history but do not possess any active filtering capabilities to block or permit traffic. For blocking specific IPs, an **NACL (Network Access Control List)** or a **Security Group** must be used.


![alt text](tgw-04.png)



![alt text](tgw-05.png)

![alt text](tgw-06.png)

![alt text](tgw-07.png)


![alt text](tgw-08.png)

![alt text](tgw-9.png)


![alt text](tgw-10.png)

![alt text](tgw-11.png)

![alt text](tgw-12.png)

![alt text](tgw-13.png)

![alt text](tgw-14.png)

![alt text](tgw-15.png)

![alt text](tgw-16.png)

![alt text](tgw-17.png)

![alt text](tgw-18.png)

![alt text](tgw-19.png)

![alt text](tgw-20.png)

![alt text](tgw-21.png)


![alt text](tgw-22.png)

![alt text](tgw-23.png)

![alt text](tgw-24.png)




---

# 🛠️ AWS Hands-On Lab: Centralized Transit Gateway (Hub & Spoke Architecture)

This lab guide details how to build a highly scalable **Hub and Spoke** network pattern using AWS Transit Gateway to interconnect multiple separate Virtual Private Clouds (VPCs).

To easily remember how to build any standalone network block from scratch in AWS, follow the foundational infrastructure rule from your class notes: **CSIR** (**C**reate VPC $\rightarrow$ **S**ubnet $\rightarrow$ **I**nternet Gateway $\rightarrow$ **R**oute Table).

---

## 📋 Lab Architecture Overview

* **Central Hub:** 1 × AWS Transit Gateway (TGW) acting as the single control plane router.
* **Network Spokes:** 4 × Isolated VPCs configured across separate IP Address CIDR spaces:
* **VPC-1:** `10.0.0.0/16` ── Subnet-1: `10.0.1.0/24`
* **VPC-2:** `172.16.0.0/16` ── Subnet-2: `172.16.1.0/24`
* **VPC-3:** `172.17.0.0/16` ── Subnet-3: `172.17.1.0/24`
* **VPC-4:** `172.18.0.0/16` ── Subnet-4: `172.18.1.0/24`



---

## 🚀 Step-by-Step Implementation Guide

### Step 1: Provision the 4 Spoke VPC Networks (Using CSIR)

You must execute these sub-steps four separate times to cleanly initialize `VPC-1`, `VPC-2`, `VPC-3`, and `VPC-4`.

#### 1. C — Create the Base VPC Boundary

1. Open the **AWS Management Console** and navigate to the **VPC Dashboard**.
2. Click **Create VPC**. Select **VPC only**.
3. Configure the **Name tag** and input the primary **IPv4 CIDR block** as designated below:
* **VPC-1:** `10.0.0.0/16`
* **VPC-2:** `172.16.0.0/16`
* **VPC-3:** `172.17.0.0/16`
* **VPC-4:** `172.18.0.0/16`


4. Click **Create VPC**.

#### 2. S — Create the Isolated Subnets

1. Select **Subnets** from the left-hand navigation sidebar, then click **Create Subnet**.
2. Select your newly created VPC target (e.g., `VPC-1`).
3. Set the **Subnet Name** and match its corresponding **IPv4 CIDR block**:
* **Subnet-1 (in VPC-1):** `10.0.1.0/24`
* **Subnet-2 (in VPC-2):** `172.16.1.0/24`
* **Subnet-3 (in VPC-3):** `172.17.1.0/24`
* **Subnet-4 (in VPC-4):** `172.18.1.0/24`


4. Click **Create Subnet**.

#### 3. I — Provision and Attach the Internet Gateways (IGW)

1. Select **Internet Gateways** from the sidebar, then click **Create Internet Gateway**.
2. Name it (e.g., `VPC-1-IGW`) and click **Create**.
3. Select your new IGW, click **Actions** $\rightarrow$ **Attach to VPC**, choose your target VPC, and confirm.

#### 4. R — Configure the Custom Route Tables

1. Select **Route Tables** from the sidebar, then click **Create Route Table**. Name it and link it to your respective VPC.
2. Complete these **two mandatory configuration updates**:
* **Update A: Routes:** Click **Edit Routes** $\rightarrow$ **Add Route**. Set the Destination destination to anywhere (`0.0.0.0/0`) and select **Internet Gateway** as your target. Save changes.
* **Update B: Subnet Association:** Click the **Subnet Associations** tab $\rightarrow$ **Edit Subnet Associations**. Select your created subnet block (e.g., `Subnet-1`) to attach it.



---

### Step 2: Deploy the Central Hub (Transit Gateway)

With all four networks running independently, we now deploy the centralized routing hub device.

1. On the VPC Console sidebar, scroll down to the **Transit Gateways** section.
2. Click **Create Transit Gateway**.
3. **Configure Settings:**
* **Name tag:** `Central-Transit-Hub`
* **Amazon side ASN:** Leave as the AWS default value, or manually provide a custom private Autonomous System Number (e.g., `64512`) as specified in your setup instructions.


4. Click **Create Transit Gateway** and wait for the status to change from `Pending` to `Available`.

---

### Step 3: Establish Transit Gateway Attachments

This step attaches your isolated networks back into the central Transit Gateway router.

1. Select **Transit Gateway Attachments** from the sidebar menu.
2. Click **Create Transit Gateway Attachment**.
3. Configure the base parameters:
* **Transit Gateway ID:** Select the gateway created in Step 2.
* **Attachment Type:** Choose **VPC**.


4. Sequentially create four attachments by targeting your VPC blocks one by one:
* **Attachment 1:** Maps to `VPC-1`
* **Attachment 2:** Maps to `VPC-2`
* **Attachment 3:** Maps to `VPC-3`
* **Attachment 4:** Maps to `VPC-4`



---

### Step 4: Update Spoke Route Tables (Define Target Paths)

To allow traffic to travel through the centralized hub, you must add structural target static paths inside each VPC Subnet Route Table pointing directly to your **Transit Gateway (TGW)**.

Navigate back to **Route Tables**, select your custom tables, and apply the following static additions:

* **In VPC-1's Route Table:**
* Destination `172.16.0.0/16` (VPC-2) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.17.0.0/16` (VPC-3) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.18.0.0/16` (VPC-4) $\rightarrow$ Target: `Transit Gateway`


* **In VPC-2's Route Table:**
* Destination `10.0.0.0/16` (VPC-1) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.17.0.0/16` (VPC-3) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.18.0.0/16` (VPC-4) $\rightarrow$ Target: `Transit Gateway`


* **In VPC-3's Route Table:**
* Destination `10.0.0.0/16` (VPC-1) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.16.0.0/16` (VPC-2) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.18.0.0/16` (VPC-4) $\rightarrow$ Target: `Transit Gateway`


* **In VPC-4's Route Table:**
* Destination `10.0.0.0/16` (VPC-1) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.16.0.0/16` (VPC-2) $\rightarrow$ Target: `Transit Gateway`
* Destination `172.17.0.0/16` (VPC-3) $\rightarrow$ Target: `Transit Gateway`



---

### Step 5: Launch Compute Test Instances (EC2)

To validate end-to-end network connectivity, deploy virtual machines into your environment boundaries:

1. Navigate to the **EC2 Dashboard** and click **Launch Instance**.
2. **Launch Server-1:**
* **Network configuration:** Select **VPC-1** and place it inside **Subnet-1**.
* **Security Group:** Create a rule that explicitly permits **All ICMP - IPv4** traffic from your collective CIDR boundaries (`10.0.0.0/8` or `172.16.0.0/12`).


3. **Launch Server-4:**
* **Network configuration:** Select **VPC-4** and place it inside **Subnet-4**.
* **Security Group:** Mirror the security profile settings above to allow ICMP echo traffic.



---

### Step 6: Validate Inter-VPC Interconnection (Ping Test)

1. Use **SSH** or **AWS EC2 Instance Connect** to log safely into your terminal environment on **Server-1**.
2. Locate the private internal IP address allocated to **Server-4** via your EC2 console overview.
3. Issue an ICMP echo ping request directly to that address:
```bash
ping <Private-IP-of-Server-4>

```



#### 📊 Expected Successful Output Summary:

```text
PING 172.18.1.XX (172.18.1.XX) 56(84) bytes of data.
64 bytes from 172.18.1.XX: icmp_seq=1 ttl=64 time=1.42 ms
64 bytes from 172.18.1.XX: icmp_seq=2 ttl=64 time=1.11 ms
64 bytes from 172.18.1.XX: icmp_seq=3 ttl=64 time=0.98 ms

--- 172.18.1.XX ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 0.982/1.171/1.421/0.185 ms

```

If your terminal yields continuous inbound reply packets with **0% packet loss**, your AWS Transit Gateway deployment is running perfectly. **It works!**


🛑 Optional Housekeeping
If you leave the ping running in Linux, it will continue indefinitely until stopped:

Press CTRL + C on your keyboard to stop the ping process anytime.
Run ping -c 5 172.18.1.119 if you ever want to test sending just 5 clean packets (it will automatically stop on its own and report 0% packet loss).


🏆 Lab Checklist Complete!
You have successfully built, configured, and verified a multi-VPC architecture:

✅ CSIR Networks created (VPC-1 through VPC-4).
✅ Transit Gateway Hub deployed & attachments created.
✅ Route Tables updated with TGW targets.
✅ Security Groups configured to allow cross-VPC ICMP traffic.
✅ End-to-End Ping Test verified!