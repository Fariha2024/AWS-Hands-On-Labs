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


