

![alt text](1a.png)


![alt text](1b.png)


![alt text](1c.png)

![alt text](1d.png)




---

## **Class - 28**

**Date:** 02/05/26

**Page:** 1

### **Simple Storage Service (S3)**

* **Simple Storage Service**

$$\downarrow$$



**Web based service**

---

### **Comparison Architecture**

```
 [ EBS Volume ]                      [ S3 Bucket ]
   (Zonal Service)                   (Regional Service)
          │                                  │
          ▼                                  ▼
┌──────────────────┐               ┌──────────────────┐
│   EBS Volume     │ ◄─── EC2 ──── │     Internet     │ ◄── User
└─────────┬────────┘               └─────────┬────────┘
          │                                  │
          ▼                                  ▼
┌──────────────────┐               ┌──────────────────┐
│Block level       │               │Object level      │
│storage           │               │storage           │
└─────────┬────────┘               └─────────┬────────┘
          │                                  │
          ▼                                  ▼
 ┌──┐ ┌──┐ ┌──┐ ┌──┐                  [ 100 MB File ]
 └──┘ └──┘ └──┘ └──┘                 (Stored as it is)
 (Data stores into
   small blocks)

```

---

### **EBS Volume vs S3 Comparison**

| **EBS Volume** | **S3 (Simple Storage Service)** |
| --- | --- |
| **Zonal Service** | **Regional Service** |
| **Block level storage** | **Object level storage** |
| Data stores into small blocks | 100MB file stores as it is |
| **Block Size:**<br>

<br>• $4\text{ KiB}$ (Min. Size)<br>

<br>• $64\text{ KiB}$ (Max. Size) | • Any size or any amount of Data.<br>

<br>• S3 has **unlimited storage**. |
| **Lower Latency** $\rightarrow$ $10\text{ ms}$<br>

<br>*(It is fast)* | **Higher Latency** $\rightarrow$ $100\text{ ms}$<br>

<br>*(Not fast compared to EBS)* |

---

### **Block Storage**

* For transactional databases, random read/write loads, and structured database storage.
* Data blocks stored in block storage **would not contain metadata**.
* Block storage only keeps the **address (index)**.
* EBS volume can only be accessed through **EC2**.
* It is **SAN storage** (*SAN – Storage Area Network*).


-----------------xxxxxxxxxxxx----------------------


![alt text](2a.png)


![alt text](2b.png)


![alt text](2c.png)


![alt text](2d.png)




---

## **Page: 2**

### **Two Types of Block storage available for EC2 Instance:**

```
               ┌──────────────────────────────────────────────┐
               │ Two Types of Block Storage for EC2 Instance  │
               └──────────────────────┬───────────────────────┘
                                      │
            ┌─────────────────────────┴─────────────────────────┐
            ▼                                                   ▼
  ┌───────────────────┐                               ┌───────────────────┐
  │    EBS Volume     │                               │   Instance Store  │
  └─────────┬─────────┘                               └─────────┬─────────┘
            │                                                   │
            ▼                                                   ▼
   Persistent Volume                                 Non-Persistent Volume
            │                                                   │
            ▼                                                   ▼
    Data Not Deleted                                  Data Deleted when server stops,
 (Stored on SAN network)                                terminates, or hibernates

```

---

### **1. EBS Volume**

* **Persistent Volume**

$$\downarrow$$



**Data Not Deleted**

> **Why? $\rightarrow$** > EBS Volume is obtained from **SAN (Storage Area Network)**, therefore EBS Volume data is not deleted.

---

### **2. Instance Store**

* **Non-Persistent Volume**

$$\downarrow$$



**Data Deleted when server stops, terminates or hibernates.**

---

---

### **Simple Storage Service (S3)**

* S3 is a storage for the internet. It has a simple web-based service.
* S3 is an **object-based storage**.
* We **cannot** install OS on S3.
* S3 has distributed data & stored in multiple locations *(minimum 3 locations in the same region)*.
* Max capacity of an object in a bucket is **50 TB** *(Single file / one file object size is 50 TB)*.
* S3 bucket is a region-specific, regional service.

---

### **Companies Using S3**

* Netflix
* Pinterest
* Walt Disney
* Slack
* Airbnb


----------------xxxxxxxxxxxx-------------------


![alt text](3a.png)



![alt text](3b.png)


![alt text](3c.png)


![alt text](3d.png)



![alt text](3e.png)



---

## **Page: 3**

### **Interview Questions**

**Que)** On what basis does S3 charge fee? OR (S3 billing charges for what basis?)

**Ans:**

1. **Storage** $\rightarrow$ Data consumed
2. **Requests** $\rightarrow$ Read / Write / Update
3. **Storage Management** $\rightarrow$ Lifecycle Management
4. **Data Transfer**

---

**Que)** S3 is suitable to store which type of data?

**Ans:** *(For Unstructured data)* *(In cloud all backups are stored in S3)*

1. Images, PDF, and Videos
2. Backup and Archive
3. Static Website Hosting
4. Big Data Analytics
5. Log storage

---

### **S3 is NOT Suitable to Store:**

1. Low latency access
2. Frequent updates
3. OS transactional support

---

### **S3 Bucket Naming Rules**

* S3 bucket names are having two options:

```
                      ┌─────────────────────────────────┐
                      │    S3 Bucket Naming Options     │
                      └────────────────┬────────────────┘
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            ▼                                                     ▼
┌───────────────────────┐                             ┌───────────────────────┐
│   Global Namespace    │                             │ Account Regional      │
│                       │                             │ Namespace             │
└───────────┬───────────┘                             └───────────┬───────────┘
            │                                                     │
            ▼                                                     ▼
 Error: (Bucket with the                             Account regional namespace
 same name already exists)                           are unique to your account.

```

1. **Global Namespace**

$$\rightarrow \text{Error: (Bucket with the same name already exists)}$$


2. **Account Regional Namespace**

$$\rightarrow \text{Account regional namespace are unique to your account.}$$



----------xxxxxxxxxxxxxxxxxxxxxx--------------------


![alt text](4a.png)


![alt text](4b.png)


![alt text](4c.png)



---

## **Page: 4**

### **S3 Bucket Naming Rules (Continued)**

* Bucket names **cannot be changed** after they are created.
* Bucket names **must not be empty**.
* Bucket names must be **at least 3 and no more than 63 characters**.
* Bucket names can contain **lowercase, numbers, and hyphens (`-`)**. We **cannot use uppercase letters**.
* Bucket name **must not be an IP Address**.

---

### **S3 Bucket URL Format**

$$\text{[https://tg-bucket-new.s3.ap-south-1.amazonaws.com/cloud+security.pdf](https://tg-bucket-new.s3.ap-south-1.amazonaws.com/cloud+security.pdf)}$$

```
https://  tg-bucket-new  .s3.  ap-south-1  .amazonaws.com/  cloud+security.pdf
───────   ─────────────   ───  ──────────   ───────────────   ──────────────────
 Protocol   Bucket Name    S3    Region       AWS Domain          File Name

```

* **Breakdown Structure:**

$$\text{https:// [bucketname] .s3. [region] .amazonaws.com / [filename]}$$



---

### **Interview Question**

**Que)** By default Bucket Versioning is disabled. If we enable Bucket Versioning, is it possible to disable it again?

**Ans:**

* Bucket Versioning **cannot be disabled after enabling it**, but you can **suspend** it.
* *(You can suspend the versioning, but you cannot disable it again.)*

---

### **Navigation Flow**

$$\text{Properties} \longrightarrow \text{Bucket Versioning} \longrightarrow \text{Edit} \longrightarrow \text{Suspend}$$

* **Suspend:** *(For temporarily stopping the service)*


----------xxxxxxxxxxxxxxxxxxxxxxxxxx----------------------



![alt text](5a.png)


![alt text](5b.png)


![alt text](5c.png)


---

## **Page: 5**

### **Bucket Versioning**

#### **Example Scenario:**

```
          Code Progress                 Action
       ┌──────────────────┐          ───────────
Day 1: │   +10% ──> 10%   │  ───────> Save
       ├──────────────────┤
Day 2: │   +10% ──> 20%   │  ───────> Save
       ├──────────────────┤
Day 3: │   +10% ──> 30%   │  ───────> Save
       ├──────────────────┤
Day 4: │   +10% ──> 40%   │  ───────> Save
       └────────┬─────────┘
                │
            { +10% } ◄── [Wrong]

```

---

### **Interview Question**

**Que)** When the current version file is deleted, does it get permanently deleted?

**Ans:**

* When the current file (Object) is deleted, it becomes a **Delete Marker**.
* *(It is not permanently deleted; instead, AWS places a Delete Marker on top of the current version).*

---

### **S3 Bucket Versioning Key Points**

* Versioning can also be used for **data retention or archive**.
* By default, Bucket Versioning is in **Disabled** state.
* Once we enable Versioning on a bucket, it **cannot be disabled**, however it can be **suspended**.
* When Versioning is enabled and we try to delete a current object, a **Delete Marker** is placed on the object.
* If we reconsider deleting the objects, we can delete the **Delete Marker** and the object will be available again.
* **Bucket Version States:** `Disabled`, `Enabled`, `Suspended`.


------------------xxxxxxxxxxxxxxxxxxxxxxxxxxx-------------------------



![alt text](6a.png)


![alt text](6b.png)


![alt text](6c.png)


---

## **Page: 6**

* **Note:** Object existing before enabling versioning will have a Version ID as **'null'**.

---

### **Interview Question**

#### **Scenario 1:**

```
[TG Company] ───> Developer 👤 ───> Code ───> Daily Update
                                               │
                                               ├── Day 1 ──┐
                                               ├── Day 2   │ ✖ Old Version Not Maintain 
                                               ├── Day 3   │   (File overwrite)
                                               └── Day 4 ──┘
                                                    │
                      ┌─────────────────────────────┴─────────────────────────────┐
                      ▼                                                           ▼
         Versioning Not Enabled ✖                                   Versioning Enabled  
                      │                                                           │
                      └─────────────────────────────┬─────────────────────────────┘
                                                    │
                                                    ▼
                                                  Day 5 ──> ??

```

**Que)** On **Day 5**, total number of version files available = **??**

**Ans: 2 Files** ($\rightarrow$ Day 4 & Day 5)

> **Explanation:** > When you enable versioning, it only tracks changes from that point onward. Versions created before enabling versioning will not be saved—they get overwritten.

---

#### **Scenario 2:**

```
Day 1 ───────────────────────────────> Versioning Enabled
  │
  ▼
7 Files
  │
  ▼
Day 7 ─────────> Upload a File ──────> Suspend Versioning
  │
  ▼
Day 10 ────────> Enable Versioning ──> How many versions I will get?
                 (Not any data / 
                  upload file)

```

**Que)** **Day 1** (Versioning Enabled, 7 Files) $\rightarrow$ **Day 7** (Upload a file, Suspend Versioning) $\rightarrow$ **Day 10** (Enable Versioning, No data/file uploaded).

How many versions will I get?

**Ans: 7 Files**



-----------------------xxxxxxxxxxxxxxxxxxxx---------------------





![alt text](7a.png)


![alt text](7b.png)


![alt text](7c.png)


![alt text](7d.png)



---

## **Page: 7**

### **Interview Question**

**Que)** Is it possible to make my previous version my current version?

**Ans: Yes** $\checkmark$

* First, delete the current version *(Delete current version without adding a Delete Marker)*.

$$\downarrow$$



**Delete**
* The previous version automatically becomes the current version *(becomes the current version)* $\checkmark$.

---

### **Note: Delete Marker Behavior**

```
                         ┌─────────────────────────────┐
                         │        Delete Marker        │
                         └──────────────┬──────────────┘
                                        │
           ┌────────────────────────────┴────────────────────────────┐
           ▼                                                         ▼
    Is a Delete Marker (✓)                               Not a Delete Marker (✗)
           │                                                         │
           ▼                                                         ▼
        Deleted                                                   Deleted
           │                                                         │
           ▼                                                         ▼
       Recoverable ✓                                         Permanently Deleted ✓

```

#### **Explanation:**

* **If it IS a Delete Marker (✓):**

$$\text{Deleted} \longrightarrow \text{Can be Recovered} \checkmark$$


* **If it is NOT a Delete Marker (✗):**

$$\text{Deleted} \longrightarrow \text{Permanently Deleted} \checkmark$$




--------------------xxxxxxxxxxxxxxxxxxxxxxxxxx---------------------------



![alt text](8a.png)


![alt text](8b.png)


![alt text](8c.png)


![alt text](8d.png)



---

## **Class - 29**

**Date:** 03/05/26

**Page:** 8

### **Amazon S3 Classes**

```
                                ┌───────────────────────────┐
                                │    Amazon S3 Classes      │
                                └─────────────┬─────────────┘
                                              │
        ┌─────────────────────────────────────┼─────────────────────────────────────┐
        ▼                                     ▼                                     ▼
┌───────────────────────────────┐ ┌───────────────────────────────┐ ┌───────────────────────────────┐
│       Frequently Access       │ │           Archival            │ │       Infrequent Access       │
│      (No min duration)        │ │  (90 & 180 Days Min Duration) │ │   (30 Days Min Duration)      │
├───────────────────────────────┤ ├───────────────────────────────┤ ├───────────────────────────────┤
│ 1) S3 Standard                │ │ 1) Glacier Deep Archive       │ │ 1) Standard-IA                │
│    (Default storage)          │ │ 2) Glacier Flexible Retrieval │ │ 2) One Zone-IA                │
│ 2) Reduced Redundancy         │ │    (Formerly Glacier)         │ │                               │
│ 3) S3-Express One Zone        │ │ 3) Glacier Instant Retrieval  │ │                               │
│    (used in Directory buckets │ │                               │ │                               │
│    for latency sensitive app) │ │                               │ │                               │
├───────────────────────────────┤ ├───────────────────────────────┤ ├───────────────────────────────┤
│ • Daily Access                │ │ • Once in a year              │ │ • Once in a month             │
│ • No Retrieval (Read) charge  │ │ • More Retrieval (Read) charge│ │ • Retrieval (Read) charge     │
└───────────────────────────────┘ └───────────────────────────────┘ └───────────────────────────────┘

```

---

### **Interview Question**

**Que)** What is the durability of Amazon S3 classes?

**Ans:** All categories have the **same Durability**: **$99.999999999\%$** *(11 Nines)*.

---

### **1. Frequently Access (No min duration)**

#### **1) S3 Standard (Default storage)**

* **Durability is $99.999999999\%$** *(11 Nines)*.
* Designed for **$99.99\%$ availability** over a given year.
* Supports **SSL for data in-transit** and **encryption of data at-rest**.
* **Storage cost** $\longrightarrow$ High
* **Accessing the objects cost** $\longrightarrow$ Very less
* **Largest object that can be uploaded in a single part is $50\text{ TB}$.**


---------------xxxxxxxxxxxxxxxxxxxxxxxxxx-------------------------



![alt text](9a.png)


![alt text](9b.png)


![alt text](9c.png)


![alt text](9d.png)



---

## **Page: 9**

### **S3 Standard Replication Overview**

```
              ┌─────────┐
              │  AZ-A   │
            ┌─┤         │
            │ └─────────┘
            │
            │ ┌─────────┐
 User ───> API┼─┤  AZ-B   │
  │         │ └─────────┘
  ▼         │
Object      │ ┌─────────┐
            └─┤  AZ-C   │
              └─────────┘

```

> **Objects are replicated across at least 3 AZs in the AWS region.**

---

### **2) Reduced Redundancy**

* In Reduced Redundancy, all features are same as **S3 Standard**, **except** there is no backup copy of object/data or no replica of objects/data.
* **Availability is $99.95\%$.**

```
 User ───> ┌───────────┐
           │  Object   │
           └─────┬─────┘
                 │
                 ├── ✖ No backup copy
                 └── ✖ No replica of object/data

```

---

### **3) S3 Express One Zone**

* The S3 bucket exists in the **same Availability Zone** where the server exists.

```
┌─────────────────────────────────────────────────────────────────────────┐
│ ap-south-1                                                              │
│                                                                         │
│  ┌────────────────────────┐  ┌───────────────┐  ┌────────────────────┐  │
│  │ 1a                     │  │ 1b            │  │ 1c                 │  │
│  │                        │  │               │  │                    │  │
│  │ User                   │  │               │  │                    │  │
│  │  │                     │  │               │  │                    │  │
│  │  ▼                     │  │               │  │                    │  │
│  │ Application            │  │               │  │                    │  │
│  │  │                     │  │               │  │                    │  │
│  │  ▼ (Zonal)             │  │               │  │                    │  │
│  │ [Data] ──> Data Upload │  │               │  │                    │  │
│  │    │                   │  │               │  │                    │  │
│  │    ▼                   │  │               │  │                    │  │
│  │ [Server]               │  │               │  │                    │  │
│  │    │ (Fast)            │  │               │  │                    │  │
│  │    ▼                   │  │               │  │                    │  │
│  │  [ S3 ] (Regional) ─────────────────> No Fast ────> [ S3 ] (Regional)│
│  └────────────────────────┘  └───────────────┘  └────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘

```

* **Used in Directory buckets for latency-sensitive applications.**



----------------------xxxxxxxxxxxxxxxxxxxxxxxxxx-------------------------


![alt text](10a.png)


![alt text](10b.png)



![alt text](10c.png)




---



## **Page: 10**

### **Bucket Type**

```
                            ┌───────────────────────────┐
                            │        Bucket Type        │
                            └─────────────┬─────────────┘
                                          │
            ┌─────────────────────────────┴─────────────────────────────┐
            ▼                                                           ▼
┌───────────────────────────────┐                           ┌───────────────────────────────┐
│        General Purpose        │                           │           Directory           │
├───────────────────────────────┤                           ├───────────────────────────────┤
│ • No option to choose         │                           │ • Option to choose            │
│   Availability Zone ✗         │                           │   Availability Zone ✓         │
│ • None Not Select ✗           │                           │ • Zone select ✓               │
└───────────────────────────────┘                           └───────────────┬───────────────┘
                                                                            │
                                                                            ▼
                                                            • Data stores in a single       
                                                              Availability Zone, but does   
                                                              NOT store data across         
                                                              multiple Availability Zones.  
                                                              *(Multiple copies are created │
                                                              inside Directory Bucket)* • Availability Zone outage/down,│
                                                              my data might be unavailable  │
                                                              or lost.                      │

```

---

### **Archival (90 or 180 Days Min Duration)**

#### **1) Glacier Deep Archive**

* **Cheapest storage**
* Designed to retain data for long period, e.g., **10 years**.
* All objects stored in S3 Glacier Deep Archive are replicated and stored across **at least three geographically dispersed AZs**.
* **Durability is $99.999999999\%$** *(11 Nines)*.
* **Retrieval time:** within **12 hours**.
* **Availability is $99.9\%$.**



--------------------------xxxxxxxxxxxxxxxxxxxxx---------------------


![alt text](11a.png)


![alt text](11b.png)



![alt text](11c.png)




---



## **Page: 11**

### **Interview Question**

**Que)** What is the lock-in period / Min storage duration of all categories?

**Ans:**

| **Storage Class** | **Min Storage Duration / Lock-in Period** | **Availability Zone (AZ)** | **Min. Billable Object Size** |
| --- | --- | --- | --- |
| **S3 Standard** | — | $\ge 3$ *(backup copy $\checkmark$)* | — |
| **Reduced Redundancy** | — | $\ge 3$ | — |
| **Intelligent-Tiering** | — | $\ge 3$ | — |
| **Standard-IA** | $30\text{ days}$ | $\ge 3$ | $128\text{ KB}$ |
| **One Zone-IA** | $30\text{ days}$ | $1$ *(No backup copy $\mathbf{\times}$)* | $128\text{ KB}$ |
| **Glacier Instant Retrieval** | $90\text{ days}$ | $\ge 3$ | $128\text{ KB}$ |
| **Glacier Flexible Retrieval** *(Formerly Glacier)* | $90\text{ days}$ | $\ge 3$ | — |
| **Glacier Deep Archive** | $180\text{ days}$ | $\ge 3$ | — |

> **Note on Min. Billable Object Size ($128\text{ KB}$):** > Example: If a file is less than $128\text{ KB}$ (e.g., $64\text{ KB}$), it will still be billed as $128\text{ KB}$ minimum.

---

### **3) Glacier Instant Retrieval**

```
               ┌───────────┐
               │ S3 Bucket │
               └─────┬─────┘
                     │
       ┌─────────────┴─────────────┐
       ▼                           ▼
[ Glacier Instant ]        [ Deep Archive ]
   Retrieval                (12 Hours Delay)
       │                           │
       ▼                           ▼
  Instantly                   ✖ Slow
 (Milliseconds)

```

* **For Read:**
* **Glacier Instant Retrieval:** Instantly $\checkmark$
* **Glacier Deep Archive:** $\mathbf{\times}$ Takes up to $12\text{ hours}$


* **Archival:**
* Use for archiving data that is rarely accessed and requires **milliseconds retrieval**.


--------------------xxxxxxxxxxxxxxxxxxxxx-------------------



![alt text](12a.png)



![alt text](12b.png)



![alt text](12c.png)



---

## **Page: 12**

### **2) Glacier Flexible Retrieval**

* Best for **Backups / disaster recovery** accessed 1-2 times/year.
* **Retrieval Speed** is **1 minute to 12 hours**.
* **Lock-in period or Min storage duration** is **90 days**.

---

### **Infrequent Access (30 Days Min Duration)**

```
                         ┌───────────────────────────┐
                         │     Infrequent Access     │
                         └─────────────┬─────────────┘
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            ▼                                                     ▼
┌───────────────────────────────┐                     ┌───────────────────────────────┐
│        1) Standard - IA       │                     │        2) One Zone - IA       │
├───────────────────────────────┤                     ├───────────────────────────────┤
│ • Min storage duration:       │                     │ • Min storage duration:       │
│   30 days                     │                     │   30 days                     │
│ • Availability Zone (AZ):     │                     │ • Availability Zone (AZ):     │
│   ≥ 3 (backup copy ✓)         │                     │   1 (backup copy ✗)           │
│ • Min billable object size:   │                     │ • Min billable object size:   │
│   128 KB                      │                     │   128 KB                      │
└───────────────────────────────┘                     └───────────────────────────────┘

```

---

### **Server Access Logging**

* **Server access logging** maintains request details. Each log entry includes requester, bucket name, request time, action (`GET`, `PUT`), response status, and error codes.
* **Logging to the same bucket can create an "Infinite Logging Loop".**

> **Best Practice:** > To **avoid Infinite Loops**, it is best practice to **use a separate target bucket** for storing logs.

---

### **Interview Question**

*(Note: Continuation onto the next page/topic)*


-------------------------xxxxxxxxxxxxxxxxxxxxxx------------------------



![alt text](13a.png)


![alt text](13b.png)



![alt text](13c.png)




---

## **Page: 13**

### **Lifecycle Management**

#### **Interview Question**

**Que)** Scenario-based: What is the solution to transition data automatically over time across storage tiers?

```
 Day 1 ───────> [ Data ] ───────> S3 Standard
                                      │
 Day 30 ────────────────────────> S3-IA (Infrequent Access)
                                      │
 Day 90 ────────────────────────> Glacier
                                      │
 Day 180 ───────────────────────> Glacier Deep Archive

```

**Ans: Lifecycle Management**

---

### **Important Notes on S3 Bucket Scope**

* **Buckets Dashboard $\longrightarrow$ Global**

$$\text{All buckets in our Account will be visible in all Regions, regardless of where they were created.}$$



```
 Mumbai ──────────────────────> Singapore / All Regions
   │                                     │
   ▼                                     ▼
All Buckets ✓                        All Buckets ✓

            (All Buckets are shown across regions)

```

* **S3 is a Regional Service** $\checkmark$
* **S3 is NOT a Global Service** $\mathbf{\times}$



----------------xxxxxxxxxxxxxxxxxxxx--------------------




![alt text](14a.png)


![alt text](14b.png)



![alt text](14c.png)



![alt text](14d.png)




---

## **Page: 14**

### **Intelligent Tiering**

```
Data (File)
    │
    ├─ Day 0  ─────────> Standard (by default)
    ├─ Day 1  ─────────> Standard
    ├─ Day 2  ─────────> Standard
    └─ Day 5  ─────────> Standard
            │
            │  (Last 30 Days No Access)
            ▼
       Day 35 ─────────> Standard-IA
       Day 40 ─────────> Access ──┐
       Day 41 ─────────> Access ──┴─> Standard

```

* Moves data automatically between access tiers based on access patterns without operational overhead.

---

### **Cross Region Replication**

* **Purpose:** For Backup purpose.
* **Flow:** Replication from **Source to Destination**.

```
  Mumbai (Source Region)                        Singapore (Destination Region)
┌───────────────────────────────┐              ┌───────────────────────────────┐
│                               │              │                               │
│        Source Bucket          │              │      Destination Bucket       │
│     ┌──────────────────┐      │  Automatic   │     ┌──────────────────┐      │
│     │   Upload XYZ     │ ─────┼──────────────┼────>│      XYZ         │      │
│     │   abc            │      │ Replication  │     │      abc         │      │
│     │   Z (Not Replicate)│    │              │     │      Z (Uploaded)│      │
│     │   [M] (Deleted)  │      │              │     │      [M]         │      │
│     └──────────────────┘      │              │     └──────────────────┘      │
│                               │              │                               │
└───────────────────────────────┘              └───────────────────────────────┘

```

#### **Replication Behavior Rules:**

* **Delete Behavior (Independent Lifecycle / Backup):**
* Deleted on Source ($\checkmark$) $\longrightarrow$ Destination **Not Deleted** ($\mathbf{\times}$)
* Not Deleted on Source ($\mathbf{\times}$) $\longrightarrow$ Deleted on Destination ($\checkmark$)


* **Upload Behavior (Source to Destination Only):**
* Uploaded on Source ($\checkmark$) $\longrightarrow$ Replicated to Destination ($\checkmark$)
* Uploaded on Destination ($\checkmark$) $\longrightarrow$ **NOT Replicated** to Source ($\mathbf{\times}$)


---------------x-----------------------------


![alt text](15a.png)


![alt text](15b.png)



![alt text](15c.png)


---

## **Page: 15**

### **Lab Exercises**

* **LAB for:** Create S3 bucket, How to give a link as a public access or private access etc. *(Object URL)*
* **LAB for:** S3 bucket Naming conventions
* **LAB for:** Public and Private Bucket.

---

### **Create a S3 bucket and put some data and try to access.**

#### **Step 1: Create Bucket**

* $\longrightarrow$ **Bucket Type**
* General purpose


* $\longrightarrow$ **Bucket Namespace**
* Global namespace


* $\longrightarrow$ **Bucket name**
* `tg-bucket-04-26`


* $\longrightarrow$ **Object Ownership**
* ACLs disabled (recommended)


* $\longrightarrow$ **Block Public Access settings for this bucket**
* [ $\checkmark$ ] Block *all* public access


* $\longrightarrow$ **Bucket Versioning**
* Disable



---

#### **Step 2: Upload** $\longrightarrow$ *(Upload a file - 1)*

```
             ┌───────────┐
             │  Upload   │
             └─────┬─────┘
                   │
                   ▼
            ┌─────────────┐
            │ Add files   │
            └─────┬─────┘
                   │
                   ▼
  AWS Diploma Syllabus (File uploaded to Bucket)

```

---

#### **Step 3: Object URL Created**

$$\text{[https://tg-bucket-04-26.s3.ap-south-1.amazonaws.com/AWS+Diploma+Syllabus.pdf](https://tg-bucket-04-26.s3.ap-south-1.amazonaws.com/AWS+Diploma+Syllabus.pdf)}$$

```
https://  bucketname  .s3.  region  .amazonaws.com /  filename
───────   ──────────   ───  ──────   ───────────────   ────────
Protocol  Bucket Name  S3   Region     AWS Domain      File Name

```



--------------------xxxxxxxxxxxxxxxxxxx---------------------



![alt text](16a.png)



![alt text](16b.png)


![alt text](16c.png)


---

## **Page: 16**

### **File Access Behaviors**

```
 File Access
  ├── Internally (My Account)  ──> Open / Download  ──> Read / Write Allowed ✓
  └── External (For all)       ──> Access Denied    ──> Public Access Denied ✗

```

---

### **Step 4: Upload** $\longrightarrow$ *(Upload a file - 2)*

```
             ┌───────────┐
             │  Upload   │
             └─────┬─────┘
                   │
                   ▼
            ┌─────────────┐
            │ Add files   │
            └─────┬─────┘
                   │
                   ▼
            AZURE Syllabus

```

---

### **Step 5: For giving a permission to All users**

$$\text{Buckets} \longrightarrow \text{tg-bucket-04-26} \longrightarrow \text{AWS Diploma Syllabus (Select)} \longrightarrow \text{Permissions}$$

$$\downarrow$$

$$\text{Object ownership} \longrightarrow \text{Edit} \longrightarrow \text{ACLs enabled}$$

$$\downarrow$$

$$\text{[ }\checkmark\text{ ] I acknowledge that ACLs will be restored}$$

---

### **Step 6: Bucket Permissions**

$$\text{Bucket} \longrightarrow \text{tg-bucket-04-26} \longrightarrow \text{Permissions} \longrightarrow \text{Edit}$$

$$\downarrow$$

$$\text{[ }\mathbf{\times}\text{ ] Block all public access (Disable / Off)}$$




-------------------xxxxxxxxxxxxxxxxxxxxxxxx-----------------



![alt text](17a.png)



![alt text](17b.png)



![alt text](17c.png)


![alt text](17d.png)



---

## **Page: 17**

### **Step 7: Granting Public Read Access to Specific Objects**

```
                     Buckets
                        │
                        ▼
                 tg-bucket-04-26
                        │
        ┌───────────────┴───────────────┐
        ▼                               ▼
AWS Diploma Syllabus             AZURE Syllabus
        │                               │
        ▼                               ▼
   Permissions                     Permissions
        │                               │
        ▼                               ▼
      Edit                           Objects
        │                               │
        ▼                               ▼
Everyone (public access)           ✓ Read

```

---

### **Step 8: Granting Public Access Directly at Time of File Upload**

$$\text{Upload} \longrightarrow \text{(Upload a file - 3)}$$

$$\downarrow$$

$$\text{Add file} \longrightarrow \text{price comparison}$$

$$\downarrow$$

$$\text{Permissions}$$

* $\longrightarrow$ **Access Control List (ACL)**
* Choose from predefined ACLs


* $\longrightarrow$ **Predefined ACLs**
* Grant public-read-access



---

### **Step 9: Making the File Private Again (No Public Access)**

$$\text{Buckets} \longrightarrow \text{tg-bucket-04-26} \longrightarrow \text{price comparison} \longrightarrow \text{Permissions} \longrightarrow \text{Edit}$$

$$\downarrow$$

$$\text{Everyone (public access)} \longrightarrow \text{Objects} \longrightarrow \mathbf{\times}\text{ Read}$$

---

* $\longrightarrow$ **Check Object URL Link:**
When checked in Google / browser, file is not seen $\mathbf{\times}$ *(Access Denied $\mathbf{\times}$)*.



-------------------xxxxxxxxxxxxxxxxxxxxxxxxx--------------------


![alt text](18a.png)



![alt text](18b.png)


![alt text](18c.png)




---

## **Page: 18**

### **Step 10: For making this file public (Given public Access)**

```
                     Buckets
                        │
                        ▼
                 tg-bucket-04-26
                        │
                        ▼
                 price comparison
                        │
                        ▼
                   Permission
                        │
                        ▼
                      Edit
                        │
                        ▼
            Everyone (public access) ─────> Objects
                                               │
                                               ▼
                                             ✓ Read

```

* $\longrightarrow$ **Check Object URL Link:**
When checked in Google / browser, file is visible $\checkmark$ *(Access given $\checkmark$)*.

---

### **Step 11: How to delete a bucket**

$$\longrightarrow \text{First empty the bucket and delete.}$$

```
                       tg-bucket-04-26
                              │
                              ▼
                            empty
                              │
                              ▼
                      permanently delete

                              │
                              ▼

                       tg-bucket-04-26
                              │
                              ▼
                            delete

```


------------xxxxxxxxxxxxxxxxxxxxx-------------------


Here is the beginner-friendly guide for the **11-Step S3 Static Website Hosting & Access Control Lab** covered across pages 15 to 18.

---

## 🎯 **Lab Overview**

### **Objective**

To set up an Amazon S3 bucket, upload website files, configure public access permissions, and host a static website accessible worldwide via a custom S3 URL.

### **Purpose**

This lab teaches how Amazon S3 stores files (objects), how permissions and Access Control Lists (ACLs) regulate file access, and how S3 serves static web pages directly to users on the internet.

---

## 🛠️ **11-Step Beginner-Friendly Lab Guide**

### **Phase 1: S3 Bucket Creation & Setup**

#### **Step 1: Create the S3 Bucket**

1. Log in to your **AWS Management Console**.
2. Search for **S3** in the top search bar and click on **S3**.
3. Click the orange **Create bucket** button.
4. Set the following configuration:
* **Bucket Type:** General purpose
* **Bucket Name:** `tg-bucket-04-26` *(or any unique bucket name)*
* **AWS Region:** Select your default region (e.g., `ap-south-1` / Mumbai)
* **Object Ownership:** ACLs disabled (recommended)
* **Block Public Access settings:** Keep **[✓] Block *all* public access** enabled for now.
* **Bucket Versioning:** Disable


5. Click **Create bucket**.

#### **Step 2: Upload Initial File**

1. Open your newly created bucket: **`tg-bucket-04-26`**.
2. Click **Upload** $\rightarrow$ **Add files**.
3. Select your file (e.g., `AWS Diploma Syllabus.pdf` or `index.html`).
4. Click **Upload**.

#### **Step 3: Test Object URL Access (Verify Access Block)**

1. Click on the uploaded file name inside your bucket to view its **Properties**.
2. Copy the **Object URL**:

$$\text{[https://tg-bucket-04-26.s3.ap-south-1.amazonaws.com/AWS+Diploma+Syllabus.pdf](https://tg-bucket-04-26.s3.ap-south-1.amazonaws.com/AWS+Diploma+Syllabus.pdf)}$$


3. Paste the URL into a new browser tab.
4. **Expected Result:** An `AccessDenied` error message appears because public access is safely blocked.

---

### **Phase 2: Enable Object Ownership & Public Access**

#### **Step 4: Enable ACLs (Object Ownership)**

1. Go to the **Permissions** tab of your bucket.
2. Scroll to **Object Ownership** and click **Edit**.
3. Change the selection from *ACLs disabled* to **ACLs enabled**.
4. Acknowledge the warnings and click **Save changes**.

#### **Step 5: Unblock Public Access Settings**

1. Stay on the **Permissions** tab.
2. Scroll to **Block public access (bucket settings)** and click **Edit**.
3. **Uncheck** the box **Block *all* public access**.
4. Click **Save changes**.
5. Type `confirm` in the popup field to verify the action.

#### **Step 6: Configure Public Access Control List (ACL)**

1. Scroll down to **Access control list (ACL)** on the Permissions tab and click **Edit**.
2. Under **Everyone (public access)**, check the following permissions:
* **Objects:** Read ✓
* **Bucket ACL:** Read ✓


3. Acknowledge the warning and click **Save changes**.

---

### **Phase 3: Upload Website Files & Enable Hosting**

#### **Step 7: Upload Website Template Files**

1. Navigate back to the **Objects** tab of your bucket.
2. Click **Upload** $\rightarrow$ **Add files** or **Add folder**.
3. Upload your website assets (such as `index.html`, CSS/JS assets, or website template files).

#### **Step 8: Set Public Read Access on Uploaded Files**

1. Before finishing the upload, expand the **Permissions** section at the bottom of the Upload page.
2. Under **Access Control List (ACL)**, choose **Grant public-read access**.
3. Check the acknowledgment box and click **Upload**.

#### **Step 9: Enable Static Website Hosting**

1. Go to the **Properties** tab of your bucket.
2. Scroll down to the bottom section: **Static website hosting**.
3. Click **Edit**.
4. Select **Enable**.
5. Under **Hosting type**, choose **Host a static website**.

#### **Step 10: Set Index Document**

1. In the **Index document** field, type `index.html`.
2. *(Optional)* In the **Error document** field, type `error.html` if you have one.
3. Click **Save changes**.

#### **Step 11: Access Your Public Website**

1. Scroll back down to **Static website hosting** under the **Properties** tab.
2. Copy the newly generated **Bucket website endpoint** URL:

$$\text{[http://tg-bucket-04-26.s3-website.ap-south-1.amazonaws.com](http://tg-bucket-04-26.s3-website.ap-south-1.amazonaws.com)}$$


3. Open the endpoint link in any browser tab to verify your live website!

---

## 🔑 **Key Takeaways**

* **S3 Security by Default:** Every S3 bucket is created 100% private by default to keep data safe.
* **Two-Layer Public Access:** To make an S3 bucket public, you must unblock public access at the bucket level **AND** grant permissions on the individual object level (or via a bucket policy).
* **Static vs. Dynamic Hosting:** S3 only hosts static content (HTML, CSS, JavaScript, Images). It cannot run server-side code like PHP, Python, or Node.js databases.

---

## 🧹 **Post-Lab Cleanup**

To avoid ongoing charges or unwanted public access on your AWS account:

1. **Delete Bucket Objects:**
* Open your bucket `tg-bucket-04-26`.
* Select all files/folders, click **Delete**, type `permanently delete`, and confirm.


2. **Delete the Bucket:**
* Go back to the **S3 > Buckets** list.
* Select `tg-bucket-04-26`, click **Delete**, enter the bucket name to confirm, and click **Delete bucket**.





----------------xxxxxxxxxxxxxxxxxxxxxxxxxxxx-----------------------


![alt text](19a.png)


![alt text](19b.png)


![alt text](19c.png)


![alt text](19d.png)



---

## **Page: 19**

### **LAB Exercise: Enable Versioning and Check Output**

#### **Step 1: Create Bucket**

* $\longrightarrow$ **Bucket name:** `tg-bucket-04-26`
* $\longrightarrow$ **Bucket Versioning:** Enable

---

#### **Step 2: Upload File 1 (Initial Version)**

```
                     ┌───────────┐
                     │  Upload   │
                     └─────┬─────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Add files   │
                    └─────┬─────┘
                           │
                           ▼
                      Code File 1
               (Upload to S3 Bucket)
                           │
                           ▼
                    [ Version ID ]
                          │
                          ▼
            (Version ID generated for file)

```

---

#### **Step 3: Modify and Upload Updated File (New Version)**

* Modify `Code File 1` and upload it again to the same bucket.

```
                Modified Code File 1
                         │
                         ▼
             Upload to same S3 Bucket
                         │
                         ▼
        ┌────────────────────────────────┐
        │   Show Versions Toggle Switch  │
        └────────────────┬───────────────┘
                         │
                         ▼
              [ Toggle Switch ON ✓ ]
                         │
                         ▼
     Both Versions (Old & New) are visible!

```

---

#### **Step 4: Delete Behavior with Versioning Enabled**

```
             Delete Current Object File
                         │
                         ▼
              [ Show Versions: OFF ]
                         │
                         ▼
             File disappears / Hidden ✗
                         │
                         ▼
              [ Show Versions: ON ]
                         │
                         ▼
          Delete Marker is placed on top!
                         │
                         ▼
        Delete the "Delete Marker" object
                         │
                         ▼
            Original File Recovered! ✓

```


---------------------xxxxxxxxxxxxxxxxxxxxx-----------------


Here is the beginner-friendly guide for the **4-Step S3 Cross-Region Replication (CRR) Lab** based on Page 19 of your AWS notes.

---

## 🎯 **Lab Overview**

### **Objective**

To set up automatic Cross-Region Replication (CRR) between two Amazon S3 buckets located in different geographical AWS regions.

### **Purpose**

This lab teaches you how to automatically back up and duplicate your data across different geographic locations for disaster recovery, lower-latency local data access, and data compliance.

---

## 🛠️ **4-Step Beginner-Friendly Lab Guide**

### **Step 1: Create the Source S3 Bucket**

1. Log in to your **AWS Management Console** and search for **S3**.
2. Click **Create bucket**.
3. Configure the following options:
* **Bucket Type:** General purpose
* **Bucket Name:** `crr-source-bucket-1`
* **AWS Region:** Choose a primary region (e.g., `ap-south-1` / Mumbai).
* **Bucket Versioning:** **Enable** *(Crucial: Versioning is strictly required for S3 Replication to work)*.


4. Click **Create bucket**.

---

### **Step 2: Create the Destination S3 Bucket**

1. Click **Create bucket** again.
2. Configure the destination options:
* **Bucket Type:** General purpose
* **Bucket Name:** `crr-destination-bucket-2`
* **AWS Region:** Choose a **different** region from your source bucket (e.g., `us-east-1` / N. Virginia).
* **Bucket Versioning:** **Enable**.


3. Click **Create bucket**.

---

### **Step 3: Configure the Replication Rule on Source Bucket**

1. Open your source bucket (`crr-source-bucket-1`).
2. Click on the **Management** tab.
3. Scroll to **Replication rules** and click **Create replication rule**.
4. Set up the rule details:
* **Replication rule name:** `CRR-Rule-1`
* **Status:** Enabled
* **Source bucket scope:** Choose **Apply to all objects in the bucket**.
* **Destination:** Choose **Choose a bucket in this account** and select `crr-destination-bucket-2`.
* **IAM Role:** Select **Create new role** *(AWS automatically grants the necessary permissions to copy files)*.


5. Click **Save**.
6. When prompted to replicate existing objects, choose **No, do not replicate existing objects** *(or Yes if you want existing files copied)*.

---

### **Step 4: Test and Verify Replication**

1. Go to the **Objects** tab of your source bucket (`crr-source-bucket-1`).
2. Click **Upload** $\rightarrow$ **Add files** and upload a new test file (e.g., `test-doc.pdf`).
3. Switch over to your destination bucket (`crr-destination-bucket-2`).
4. Refresh the page after a few seconds.
5. **Expected Result:** The `test-doc.pdf` file automatically appears in the destination bucket!

---

### **S3 Cross-Region Replication (CRR) Architecture Diagram:**

```
┌──────────────────────────────────────────┐          ┌──────────────────────────────────────────┐
│ Source Region (e.g., ap-south-1)          │          │ Destination Region (e.g., us-east-1)     │
│                                          │          │                                          │
│  ┌────────────────────────────────────┐  │          │  ┌────────────────────────────────────┐  │
│  │ Source Bucket: crr-source-bucket-1 │  │          │  │ Destination Bucket:                │  │
│  │ (Versioning: Enabled)              │  │          │  │ crr-destination-bucket-2             │  │
│  │                                    │  │          │  │ (Versioning: Enabled)                 │  │
│  │  1. Upload File ──► test-doc.pdf   │  │          │  │                                    │  │
│  └─────────────────┬──────────────────┘  │          │  └──────────────────▲─────────────────┘  │
│                    │                     │          │                     │                    │
└────────────────────┼─────────────────────┘          └─────────────────────┼────────────────────┘
                     │                                                      │
                     │                 Automatic Asynchronous               │
                     └──────────────────── Replication ─────────────────────┘
                                           (via IAM Role)

```

---

## 🔑 **Key Takeaways**

* **Versioning Requirement:** Bucket versioning **must** be enabled on both the source and destination buckets before replication can work.
* **IAM Permissions:** S3 requires an IAM service role to grant authorization to read from the source bucket and write to the destination bucket.
* **Asynchronous Copying:** Replication happens automatically in the background (asynchronously), so files usually show up in the target region within seconds to a few minutes.

---

## 🧹 **Post-Lab Cleanup**

To prevent ongoing storage or transfer charges on your AWS account:

1. **Delete Replication Rule:**
* Open `crr-source-bucket-1` $\rightarrow$ **Management** tab $\rightarrow$ **Replication rules**.
* Select `CRR-Rule-1` and click **Delete**.


2. **Empty & Delete Source Bucket:**
* Open `crr-source-bucket-1`.
* Click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, select `crr-source-bucket-1`, click **Delete**, type the bucket name, and confirm.


3. **Empty & Delete Destination Bucket:**
* Open `crr-destination-bucket-2`.
* Click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, select `crr-destination-bucket-2`, click **Delete**, type the bucket name, and confirm.



------------------xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-----------------


![alt text](20a.png)


![alt text](20b.png)


![alt text](20c.png)


![alt text](20d.png)



---

## **Page: 20**

### **LAB Exercise: Cross-Region Replication (CRR)**

#### **Step 1: Create Source and Destination Buckets**

* **Source Bucket:** `tg-source-mumbai-04-26` *(Region: ap-south-1 / Mumbai)*
* **Versioning:** Enable


* **Destination Bucket:** `tg-dest-singapore-04-26` *(Region: ap-southeast-1 / Singapore)*
* **Versioning:** Enable



---

#### **Step 2: Setup Replication Rule**

$$\text{Source Bucket (tg-source-mumbai-04-26)} \longrightarrow \text{Management} \longrightarrow \text{Replication rules} \longrightarrow \text{Create replication rule}$$

```
                 Replication Rule Configuration
                               │
                               ▼
                    Rule Name: [ My-CRR-Rule ]
                               │
                               ▼
                   Status: [ Enabled ✓ ]
                               │
                               ▼
                    Source Bucket: [ Choose ]
                               │
                               ▼
              Destination: [ tg-dest-singapore-04-26 ]
                               │
                               ▼
                  IAM Role: [ Create New Role ]

```

---

#### **Step 3: Verification & Output Check**

```
         Upload file to Source Bucket (tg-source-mumbai-04-26)
                                 │
                                 ▼
                     Wait a few seconds...
                                 │
                                 ▼
      Check Destination Bucket (tg-dest-singapore-04-26)
                                 │
                                 ▼
         File automatically replicated to Singapore! ✓

```


-----------------------xxxxxxxxxxxxxxxxxxxxx--------------------


Here is the beginner-friendly guide for the **S3 Cross-Region Replication (CRR) Lab** spanning pages 20 to 23 of your AWS notes.

---

## 🎯 **Lab Overview**

### **Objective**

To configure automatic **Cross-Region Replication (CRR)** between a source S3 bucket in one region (e.g., Mumbai - `ap-south-1`) and a destination S3 bucket in a completely different region (e.g., Singapore - `ap-southeast-1`), utilizing bucket versioning and IAM role permissions.

### **Purpose**

This lab demonstrates how to maintain automated, asynchronous backups of critical data across different geographic regions. This provides **disaster recovery**, ensures **data compliance**, and lowers latency for end-users located in different parts of the world.

---

## 🛠️ **Step-by-Step Beginner-Friendly Lab Guide**

### **Step 1: Create the Source S3 Bucket (Mumbai Region)**

1. Log in to the **AWS Management Console** and navigate to the **S3** service console.
2. Click **Create bucket**.
3. Configure the following details:
* **Bucket type:** General purpose
* **Bucket name:** `crr-source-mumbai-bucket` *(Names must be globally unique)*
* **AWS Region:** `Asia Pacific (Mumbai) ap-south-1`
* **Bucket Versioning:** Select **Enable** *(Replication requires versioning to track file changes)*.


4. Scroll to the bottom and click **Create bucket**.

---

### **Step 2: Create the Destination S3 Bucket (Singapore Region)**

1. Click **Create bucket** again.
2. Configure the target bucket details:
* **Bucket type:** General purpose
* **Bucket name:** `crr-destination-singapore-bucket`
* **AWS Region:** `Asia Pacific (Singapore) ap-southeast-1` *(Must be a different region from the source)*
* **Bucket Versioning:** Select **Enable**.


3. Scroll down and click **Create bucket**.

---

### **Step 3: Configure the Replication Rule on Source Bucket**

1. Click on your source bucket: **`crr-source-mumbai-bucket`**.
2. Go to the **Management** tab.
3. Scroll down to **Replication rules** and click **Create replication rule**.
4. Configure the replication parameters:
* **Replication rule name:** `CRR-Rule-Mumbai-to-Singapore`
* **Status:** Enabled
* **Source bucket scope:** Choose **Apply to all objects in the bucket**.
* **Destination:** Select **Choose a bucket in this account**.
* **Destination Bucket:** Click **Browse S3** and pick `crr-destination-singapore-bucket`.
* **IAM Role:** Select **Create new role** *(AWS will automatically attach the correct policy giving S3 permission to copy files)*.


5. Click **Save**.
6. When asked whether to replicate existing objects, select **No, do not replicate existing objects** (or *Yes* if you want older files copied).

---

### **Step 4: Verify Cross-Region Replication**

1. Go to the **Objects** tab inside **`crr-source-mumbai-bucket`**.
2. Click **Upload** $\rightarrow$ **Add files**, choose a test document or image, and click **Upload**.
3. Open a new browser tab or navigate to the S3 Console and open **`crr-destination-singapore-bucket`**.
4. Refresh the page after a few seconds.
5. **Expected Result:** The file uploaded to Mumbai automatically appears inside the Singapore bucket!

---

### **S3 Cross-Region Replication (CRR) Architecture Diagram:**

```
┌──────────────────────────────────────────┐          ┌──────────────────────────────────────────┐
│ Source Region: ap-south-1 (Mumbai)       │          │ Destination Region: ap-southeast-1      │
│                                          │          │ (Singapore)                              │
│  ┌────────────────────────────────────┐  │          │  ┌────────────────────────────────────┐  │
│  │ Source Bucket:                     │  │          │  │ Destination Bucket:                │  │
│  │ crr-source-mumbai-bucket           │  │          │  │ crr-destination-singapore-bucket   │  │
│  │ (Versioning: Enabled)              │  │          │  │ (Versioning: Enabled)                 │  │
│  │                                    │  │          │  │                                    │  │
│  │  1. Upload File ──► file.pdf       │  │          │  │  2. Automatically Replicated       │  │
│  └─────────────────┬──────────────────┘  │          │  └──────────────────▲─────────────────┘  │
│                    │                     │          │                     │                    │
└────────────────────┼─────────────────────┘          └─────────────────────┼────────────────────┘
                     │                                                      │
                     │                 Automatic Asynchronous               │
                     └──────────────────── Replication ─────────────────────┘
                                           (via IAM Role)

```

---

## 🔑 **Key Takeaways**

* **Versioning Requirement:** Bucket versioning **must** be turned on for both the source and target buckets before CRR can operate.
* **Asynchronous Copying:** Replication takes place asynchronously in the background. It does not slow down your initial file upload speed.
* **Automatic IAM Role:** AWS creates an IAM role behind the scenes that grants `s3:GetObjectVersion` permissions on the source and `s3:ReplicateObject` permissions on the destination.

---

## 🧹 **Post-Lab Cleanup**

To prevent unexpected storage or cross-region data transfer charges on your AWS account:

1. **Delete the Replication Rule:**
* Go to `crr-source-mumbai-bucket` $\rightarrow$ **Management** tab $\rightarrow$ **Replication rules**.
* Select your rule and click **Delete**.


2. **Empty & Delete Source Bucket:**
* Select `crr-source-mumbai-bucket`, click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, click **Delete**, type the bucket name, and confirm.


3. **Empty & Delete Destination Bucket:**
* Select `crr-destination-singapore-bucket`, click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, click **Delete**, type the bucket name, and confirm.




------------------xxxxxxxxxxxxxxxxxxxxxxxxxxxx-----------------



![alt text](21a.png)



![alt text](21b.png)



![alt text](21c.png)



---

## **Page: 21**

### **LAB Topics Covered:**

* **LAB for:** How to enable encryption on S3 bucket
* **LAB for:** AWS S3 Server Access Logging
* **LAB for:** S3 Access logs and Transfer Acceleration
* **LAB for:** Configure Lifecycle from S3 to Glacier

---

#### **Step 1: Create Bucket**

* $\longrightarrow$ **Bucket Type**
* General purpose


* $\longrightarrow$ **Bucket Namespace**
* Global Namespace


* $\longrightarrow$ **Bucket Name**
* `1-jan-2026-aws`


* $\longrightarrow$ **Object ownership**
* ACLs enabled


* $\longrightarrow$ **Block public Access settings for this bucket**
* [ $\mathbf{\times}$ ] Block all public Access


* $\longrightarrow$ **Bucket Versioning**
* Enable



---

#### **Step 2: Upload File & Permissions**

```
                     ┌───────────┐
                     │  Upload   │
                     └─────┬─────┘
                           │  (Upload a file: AWS Diploma syllabus)
                           ▼
                    ┌─────────────┐
                    │ Add files   │
                    └─────┬─────┘
                           │
                           ▼
                 AWS Diploma Syllabus
                           │
                           ▼
                      Permissions
                           │
                           ▼
          Access control list (ACL)
                           │
                           ▼
          Choose from predefined ACLs
                           │
                           ▼
                 Predefined ACLs
                           │
                           ▼
                 Private (recommended)

```

---

* $\longrightarrow$ **Properties Configuration:**
* **Storage class:** Standard *(By default)*



------------------xxxxxxxxxxxxxxxxxx----------------------


![alt text](22a.png)



![alt text](22b.png)


![alt text](22c.png)


![alt text](22d.png)


---

## **Page: 22**

#### **Step 3: Using Key Management Service (KMS)**

* $\longrightarrow$ Using symmetric key encrypt our S3 data.

```
                     Bucket
                       │
                       ▼
               1-jan-2026-aws
                       │
                       ▼
             AWS Diploma Syllabus
                       │
                       ▼
                  Properties
                       │
                       ▼
               Default Encryption
                       │
                       ▼
                      Edit
                       │
                       ▼
                Encryption type
                       │
                       ▼
 Server-side encryption with AWS Key Management service keys (SSE-KMS)
                       │
                       ▼
                 AWS KMS Key
                       │
                       ▼
       Choose from your AWS KMS keys
                       │
                       ▼
           ┌───────────────────────┐
           │                       │  ◄─── (Select Key from Step 4)
           └───────────────────────┘

```

---

#### **Step 4: For create a key, for Encryption**

$$\longrightarrow \text{Key Management Service (KMS)}$$

```
                   Create key
                       │
                       ▼
                   Key type
                       │
                       ▼
                   Symmetric
                       │
                       ▼
                   Key usage
                       │
                       ▼
              Encrypt and decrypt
                       │
                       ▼
                     Alias
                       │
                       ▼
            1-jan-2026-aws-key-123  ────────┐
                       │                    │
                       ▼                    │
                    Finish                  │
                                            ▼
                             (Selects in Step 3 dropdown)

```



----------------xxxxxxxxxxxxxxxxx----------------------



Here is the beginner-friendly guide for the **4-Step S3 Server-Side Encryption with AWS KMS (SSE-KMS) Lab** covering pages 21 and 22 of your notes.

---

## 🎯 **Lab Overview**

### **Objective**

To create a custom KMS (Key Management Service) encryption key and configure an Amazon S3 bucket to automatically encrypt all uploaded objects using **Server-Side Encryption with AWS KMS (SSE-KMS)**.

### **Purpose**

This lab demonstrates how to secure sensitive data stored in S3 at rest. By creating your own Customer Managed Key (CMK) in AWS KMS, you gain full control over who can encrypt, decrypt, and manage the keys used to protect your storage data.

---

## 🛠️ **4-Step Beginner-Friendly Lab Guide**

### **Step 1: Create a Custom KMS Encryption Key**

1. Log in to the **AWS Management Console**.
2. Search for **KMS** (Key Management Service) in the top search bar and open it.
3. In the left navigation menu, click **Customer managed keys** and then click **Create key**.
4. Configure key options:
* **Key type:** Select **Symmetric** *(Single key used for both encryption and decryption)*.
* **Key usage:** Select **Encrypt and decrypt**.
* Click **Next**.


5. Add an alias/name:
* **Alias:** Enter `s3-kms-encryption-key` *(or your preferred alias)*.
* Click **Next**.


6. Define Key Administrative and Usage Permissions:
* **Key administrators:** Select your current IAM user/role.
* **Key usage permissions:** Select your IAM user/role so you can use the key for S3.


7. Review the key configuration and click **Finish**.

---

### **Step 2: Create the S3 Bucket**

1. Search for **S3** in the top search bar and navigate to the S3 Console.
2. Click **Create bucket**.
3. Configure bucket parameters:
* **Bucket type:** General purpose
* **Bucket name:** `kms-encrypted-s3-bucket-1` *(Names must be globally unique)*
* **AWS Region:** Select your preferred region (e.g., `ap-south-1` / Mumbai).
* **Bucket Versioning:** Enable


4. Scroll to **Default encryption**:
* **Encryption type:** Select **AWS Key Management Service key (SSE-KMS)**.
* **AWS KMS key:** Choose **Choose from your AWS KMS keys**.
* Select the key alias created in Step 1 (`s3-kms-encryption-key`).


5. Click **Create bucket**.

---

### **Step 3: Upload an Object to Test Automatic Encryption**

1. Click on your newly created bucket: **`kms-encrypted-s3-bucket-1`**.
2. Click **Upload** $\rightarrow$ **Add files**.
3. Choose a test document from your local computer (e.g., `sample-file.txt`).
4. Click **Upload**.

---

### **Step 4: Verify KMS Server-Side Encryption**

1. Inside your bucket, click on the file name (`sample-file.txt`) to open its **Properties**.
2. Scroll down to the **Server-side encryption details** section.
3. **Expected Result:** * **Encryption type:** AWS Key Management Service keys (SSE-KMS)
* **AWS KMS key ARN:** Displays the exact Amazon Resource Name (ARN) of the custom key (`s3-kms-encryption-key`) created in Step 1!



---

### **S3 Server-Side Encryption (SSE-KMS) Workflow Diagram:**

```
┌─────────────────────────────────────────────────────────────┐
│ 1. AWS KMS (Key Management Service)                         │
│                                                             │
│    ┌──────────────────────────────────────────────────┐     │
│    │ Customer Managed Key: s3-kms-encryption-key      │     │
│    └────────────────────────┬─────────────────────────┘     │
└─────────────────────────────┼───────────────────────────────┘
                              │
                              │ Used for Encryption
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Amazon S3 Bucket (kms-encrypted-s3-bucket-1)             │
│                                                             │
│    ┌────────────────────┐     ┌──────────────────────────┐  │
│    │ User Uploads File  ├────►│ Auto-encrypts file using │  │
│    │ (sample-file.txt)  │     │ KMS Key before storing   │  │
│    └────────────────────┘     └─────────────┬────────────┘  │
│                                             │               │
│                                             ▼               │
│                               ┌──────────────────────────┐  │
│                               │ Encrypted File Stored    │  │
│                               │ Securely at Rest ✓       │  │
│                               └──────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 **Key Takeaways**

* **Encryption at Rest:** SSE-KMS encrypts your data after receiving it on AWS disks and decrypts it automatically when you download or access it.
* **Customer Control:** Using a Customer Managed Key (CMK) allows you to audit key access logs via AWS CloudTrail and disable/revoke key permissions at any time.
* **Seamless S3 Integration:** Once default bucket encryption is configured with your KMS key, every uploaded object is automatically protected without requiring extra upload parameters.

---

## 🧹 **Post-Lab Cleanup**

To prevent clutter and avoid unnecessary KMS key costs ($1/month per key):

1. **Empty and Delete the S3 Bucket:**
* Go to **S3 Console** $\rightarrow$ select `kms-encrypted-s3-bucket-1`.
* Click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, select `kms-encrypted-s3-bucket-1`, click **Delete**, type the bucket name, and confirm.


2. **Schedule KMS Key Deletion:**
* Navigate to **KMS Console** $\rightarrow$ **Customer managed keys**.
* Select `s3-kms-encryption-key`.
* Click **Key actions** $\rightarrow$ **Schedule key deletion**.
* Set the waiting period (7 days minimum) and confirm deletion.




------------xxxxxxxxxxxxxxxxxxxxx----------------------


![alt text](23a.png)


![alt text](23b.png)



![alt text](23c.png)



---

## **Page: 23**

### **LAB Exercise: AWS S3 Server Access Logging**

#### **Step 1: Create Target Bucket for Logs**

* Create a separate target bucket named `target-log-bucket-aws-01`.

---

#### **Step 2: Enable Server Access Logging on Source Bucket**

```
                 Source Bucket (1-jan-2026-aws)
                               │
                               ▼
                           Properties
                               │
                               ▼
                     Server Access Logging
                               │
                               ▼
                             Edit
                               │
                               ▼
                            [ Enable ]
                               │
                               ▼
                         Target Bucket
                               │
                               ▼
              [ Choose: target-log-bucket-aws-01 ]

```

---

#### **Step 3: Access Logging Architecture Flow**

```
 User Performs Actions ───> Source Bucket ───> Generates Logs ───> Target Bucket
(GET / PUT / Delete)      (1-jan-2026-aws)                        (target-log-bucket-aws-01)
                                                                               │
                                                                               ▼
                                                                     *(Avoids Infinite Loop)*

```




-------------------------xxxxxxxxxxxxxxxxxxxxxx--------------------


Here is the beginner-friendly guide for the **3-Step S3 Server Access Logging Lab** based on Page 23 of your notes.

---

## 🎯 **Lab Overview**

### **Objective**

To create a dedicated **Target Logging Bucket** and configure **Server Access Logging** on a **Source S3 Bucket** so that every request (GET, PUT, DELETE) made to the source bucket is automatically recorded and saved as log files in the target bucket.

### **Purpose**

This lab teaches you how to perform security audits, track access patterns, and monitor user traffic on your S3 resources. By storing access logs in a separate target bucket, you ensure complete auditability while avoiding an **infinite logging loop** (where a bucket generates log entries about its own logs).

---

## 🛠️ **3-Step Beginner-Friendly Lab Guide**

### **Step 1: Create the Target Logging Bucket**

1. Log in to the **AWS Management Console** and navigate to the **S3** service console.
2. Click **Create bucket**.
3. Configure the logging bucket details:
* **Bucket type:** General purpose
* **Bucket name:** `target-log-bucket-aws-01` *(Must be in the **same region** as your main bucket)*
* **AWS Region:** Select your default region (e.g., `ap-south-1` / Mumbai)
* **Block Public Access:** Keep **[✓] Block *all* public access** checked (logs should stay private).


4. Click **Create bucket**.

---

### **Step 2: Enable Server Access Logging on the Source Bucket**

1. From the S3 Buckets list, click on your main/source bucket (e.g., `1-jan-2026-aws`).
2. Select the **Properties** tab at the top.
3. Scroll down to the **Server access logging** section and click **Edit**.
4. Configure the logging settings:
* **Status:** Choose **Enable**.
* **Target bucket:** Choose **Browse S3** and select `target-log-bucket-aws-01` (created in Step 1).
* **Target prefix (optional):** Enter `logs/` to group all incoming log files inside a specific folder.


5. Click **Save changes**.

---

### **Step 3: Perform Actions & Verify Log Delivery**

1. Open your source bucket (`1-jan-2026-aws`) and perform a few routine actions:
* Upload a small text file or image.
* Download the uploaded file.
* Delete or view object properties.


2. Navigate to your target bucket (`target-log-bucket-aws-01`).
3. Open the `logs/` folder (if a prefix was configured) and click **Refresh**.
4. **Expected Result:** Text files containing detailed HTTP access records (showing requester IP, timestamp, action type like `REST.GET.OBJECT`, and HTTP status codes) will begin populating in the target bucket. *(Note: AWS S3 log delivery can take anywhere from 10–15 minutes to appear)*.

---

### **S3 Server Access Logging Architecture Diagram:**

```
┌─────────────────────────────────────────────────────────────┐
│ 1. User / Application Action                                │
│                                                             │
│    ┌──────────────────────────────────────────────────┐     │
│    │ Performs GET, PUT, or DELETE requests            │     │
│    └────────────────────────┬─────────────────────────┘     │
└─────────────────────────────┼───────────────────────────────┘
                              │
                              │ Access Request
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Source S3 Bucket (1-jan-2026-aws)                        │
│                                                             │
│    ┌──────────────────────────────────────────────────┐     │
│    │ Properties: Server Access Logging Enabled        │     │
│    └────────────────────────┬─────────────────────────┘     │
└─────────────────────────────┼───────────────────────────────┘
                              │
                              │ Generates Access Log Files
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Target S3 Bucket (target-log-bucket-aws-01)              │
│                                                             │
│    ┌──────────────────────────────────────────────────┐     │
│    │ Stores raw text log files (logs/2026-07-20-...)  │     │
│    │ Details: Requester IP, Timestamp, API Operation  │     │
│    └──────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 **Key Takeaways**

* **Same Region Requirement:** The target log bucket **must** reside in the same AWS Region as the source bucket.
* **Preventing Infinite Loops:** Always log to a **separate** target bucket. If a bucket is configured to write log files to itself, each new log file write generates another log entry, causing an exponential, costly loop.
* **Log Delivery Delay:** Server access logs are delivered on a best-effort basis and generally take a few minutes to show up in the target destination.

---

## 🧹 **Post-Lab Cleanup**

To prevent accumulating log storage costs over time:

1. **Disable Logging on Source Bucket:**
* Go to `1-jan-2026-aws` $\rightarrow$ **Properties** tab $\rightarrow$ **Server access logging**.
* Click **Edit**, select **Disable**, and click **Save changes**.


2. **Empty & Delete Target Logging Bucket:**
* Open `target-log-bucket-aws-01`.
* Select all generated log files/folders, click **Delete**, type `permanently delete`, and confirm.
* Return to the **S3 > Buckets** page, select `target-log-bucket-aws-01`, click **Delete**, enter the bucket name, and confirm.


----------------xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx------------------



![alt text](24a.png)


![alt text](24b.png)



![alt text](24c.png)


---

## **Page: 24**

### **LAB Exercise: Event Notifications with Amazon SNS**

#### **Step 1: Configure Event Destination**

* $\longrightarrow$ **Destination:** SNS topic
* $\longrightarrow$ **Specify SNS topic:** Choose from your SNS topics

---

#### **Step 2: Simple Notification Service (SNS) Setup**

```
             Simple Notification Service (SNS)
                             │
                             ▼
                     Create SNS topic
                             │
                             ▼
                          Topics
                             │
                             ▼
                      Create topic
                             │
                             ▼
                         Type: Standard
                             │
                             ▼
              Name: S3-delete-event-SNS123 ────────┐
                             │                    │
                             ▼                    │ (Select ✓)
                   Display Name:                  │
             object removal notification          │
                             │                    │
                             ▼                    │
                        Subscription              │
                             │                    │
                             ▼                    │
                    Create subscription           │
                             │                    │
                             ▼                    │
                  Topic ARN: <────────────────────┘
               [ S3-delete-event-SNS123 ]
                             │
                             ▼
                      Protocol: Email
                             │
                             ▼
                         Endpoint:
                paragdongre997@gmail.com
                             │
                             ▼
                        Go to Gmail
                             │
                             ▼
                   Confirm Subscription ✓

```


---------------xxxxxxxxxxxxxxxxxxxxxxxxxxxx-----------------------


![alt text](25a.png)


![alt text](25b.png)


![alt text](25c.png)


---

## **Page: 25**

### $\longrightarrow$ **For Testing / Verification**

#### **Testing Object Deletion Notification:**

```
                     Buckets
                        │
                        ▼
                 1-jan-2026-aws
                        │
                        ▼
                     Upload  ───> (Upload a file: linux.cmd.ncws)
                        │
                        ▼
                    Add files
                        │
                        ▼
                  linux.cmd.ncws
                        │
                        ▼
                 After upload: Delete
                        │
                        ▼
                     Delete ✓
                        │
                        ▼
            Check Gmail (For delete)

```

---

#### **Testing Object Upload Notification:**

```
                     Buckets
                        │
                        ▼
                 1-jan-2026-aws
                        │
                        ▼
                     Upload  ───> (Upload AWS Diploma syllabus)
                        │
                        ▼
                    Add files
                        │
                        ▼
               AWS Diploma syllabus
                        │
                        ▼
            Check Gmail (For Upload)
                        │
                        ▼
            Google ───> What is my IP

```


------------------xxxxxxxxxxxxxxxxxxxxx-------------------



![alt text](26a.png)



![alt text](26b.png)



![alt text](26c.png)



---

## **Page: 26**

### **Step 8: For Lifecycle Management**

```
                     Buckets
                        │
                        ▼
                 1-jan-2026-aws
                        │
                        ▼
                    Management
                        │
                        ▼
             Create lifecycle rule

```

---

* $\longrightarrow$ **Lifecycle rule name**
* `1-jan-2026-aws-lifecycle-rule123`


* $\longrightarrow$ **Choose rule scope**
* Apply to all objects in the bucket


* $\longrightarrow$ **Lifecycle rule actions**
* [ $\mathbf{\checkmark}$ ] Transition current versions of objects between storage classes.
* [ $\mathbf{\checkmark}$ ] Permanently delete noncurrent versions of objects.



---

#### **Choose storage class transitions**

```
                 Lock-in Period
Standard-IA ────> (30 days)  ───┐
                                │ ───> 75  ────> 30 ───┐
Glacier Instant ──> (90 days) ──┼───> 150 ───> 60 ───┼───> [ 90 ] ─── (+30) ───┐
Retrieval                       │                    │                         │
Glacier Deep ────> (180 days) ──┴───> 365 ───> 150 ──┴───> 250 ───────── (+90) ──┴──> [  ]
Archive

```

* **Standard-IA** *(Lock-in period: 30 days)*
* **Glacier Instant Retrieval** *(Lock-in period: 90 days)*
* **Glacier Deep Archive** *(Lock-in period: 180 days)*

---

* $\longrightarrow$ **Days after objects become noncurrent**
* `365`


* $\longrightarrow$ **Number of newer versions to retain - optional**
* `3`



-----------------xxxxxxxxxxxxxxxxxxxxxxxxxx-----------------------



Here is the complete **S3 Event Notifications with Amazon SNS Lab (Pages 24–26)** formatted in clean Markdown. You can easily copy the block below directly into Visual Studio Code for your notes:

```markdown
# AWS Lab: S3 Event Notifications with Amazon SNS (Pages 24–26)

---

## 🎯 Lab Overview

### Objective
To set up **Amazon S3 Event Notifications** integrated with **Amazon Simple Notification Service (SNS)** so that whenever an object is uploaded or deleted in an S3 bucket, an automated email alert is sent to your inbox.

### Purpose
This lab teaches you how to build real-time, event-driven workflows in AWS. Instead of manually checking an S3 bucket for changes, S3 automatically publishes events to an SNS topic, which immediately notifies users via email.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create an Amazon SNS Topic
1. Log in to the **AWS Management Console** and search for **SNS (Simple Notification Service)**.
2. In the left menu, click **Topics**, then click **Create topic**.
3. Configure the topic settings:
   * **Type:** Select **Standard**.
   * **Name:** Enter `S3-delete-event-SNS123` *(or your preferred topic name)*.
   * **Display name:** Enter `S3-Alerts`.
4. Click **Create topic**.

---

### Step 2: Create and Confirm Email Subscription
1. Inside your newly created topic details page, scroll down to **Subscriptions** and click **Create subscription**.
2. Set up the subscription parameters:
   * **Protocol:** Select **Email**.
   * **Endpoint:** Enter your email address (e.g., `paragdongre997@gmail.com`).
3. Click **Create subscription**.
4. **Confirm Subscription:**
   * Open your email inbox.
   * Look for an email from **AWS Notifications**.
   * Click the **Confirm subscription** link inside the email.

---

### Step 3: Update SNS Topic Access Policy
To allow Amazon S3 to publish notification events to your SNS topic, update the access policy:
1. In the SNS Topic page, click **Edit** and expand **Access policy**.
2. Add a permission statement allowing the S3 service principal (`s3.amazonaws.com`) to execute `sns:Publish` on your SNS topic.
3. Click **Save changes**.

---

### Step 4: Configure S3 Event Notifications
1. Search for **S3** in the top search bar and open the S3 Console.
2. Click on your bucket (e.g., `1-jan-2026-aws`).
3. Select the **Properties** tab.
4. Scroll down to **Event notifications** and click **Create event notification**.
5. Configure the event settings:
   * **Event name:** Enter `S3-Upload-And-Delete-Notification`.
   * **Event types:** Check the boxes for:
     * **All object create events** (`s3:ObjectCreated:*`)
     * **All object removal events** (`s3:ObjectRemoved:*`)
   * **Destination:** Select **SNS topic**.
   * **SNS Topic:** Choose **Select from your SNS topics** and select `S3-delete-event-SNS123`.
6. Click **Save changes**.

---

### Step 5: Test and Verify Notifications

#### Test 1: Object Creation (Upload)
1. Go to the **Objects** tab of your bucket `1-jan-2026-aws`.
2. Click **Upload** $\rightarrow$ **Add files** and upload a file (e.g., `AWS Diploma syllabus`).
3. Click **Upload**.
4. Check your email inbox for an automated notification detailing the object creation event (`ObjectCreated:Put`).

#### Test 2: Object Deletion
1. Select a file in your bucket (e.g., `linux.cmd.ncws`) and click **Delete**.
2. Type `delete` or `permanently delete` to confirm.
3. Check your email inbox for an automated notification detailing the object deletion event (`ObjectRemoved:Delete`).

---

## 🏗️ Architecture Flow


```

┌─────────────────────────────────────────┐
│ 1. User Action in S3                    │
│                                         │
│   Upload File (e.g., AWS Diploma)       │
│   OR                                    │
│   Delete File (e.g., linux.cmd.ncws)    │
└────────────────────┬────────────────────┘
│
│ Triggers Event (ObjectCreated / ObjectRemoved)
▼
┌─────────────────────────────────────────┐
│ 2. Amazon S3 Bucket (1-jan-2026-aws)    │
│                                         │
│   Publishes JSON payload to SNS Topic   │
└────────────────────┬────────────────────┘
│
│ sns:Publish
▼
┌─────────────────────────────────────────┐
│ 3. Amazon SNS Topic                     │
│    (S3-delete-event-SNS123)             │
│                                         │
│   Routes message to Email Subscribers   │
└────────────────────┬────────────────────┘
│
│ Sends Email Alert
▼
┌─────────────────────────────────────────┐
│ 4. User Email Inbox                     │
│    (paragdongre997@gmail.com)           │
│                                         │
│   Receives Real-time AWS Notification ✓ │
└─────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Same Region Rule:** The Amazon S3 bucket and the Amazon SNS topic **must** reside in the exact same AWS Region for event notifications to work.
* **Access Policy Permission:** S3 cannot publish events to SNS by default. The SNS topic's Access Policy must explicitly allow `s3.amazonaws.com` permission to call `sns:Publish`.
* **Subscription Confirmation:** Email notifications will not be delivered until you explicitly click the **Confirm subscription** link sent to your inbox.

---

## 🧹 Post-Lab Cleanup

To avoid cluttering your account and receiving unwanted event emails:

1. **Delete S3 Event Notification:**
   * Go to S3 Bucket `1-jan-2026-aws` $\rightarrow$ **Properties** tab $\rightarrow$ **Event notifications**.
   * Select `S3-Upload-And-Delete-Notification` and click **Delete**.

2. **Delete SNS Topic & Subscription:**
   * Open the **SNS Console** $\rightarrow$ **Subscriptions**. Select your subscription and click **Delete**.
   * Go to **Topics**, select `S3-delete-event-SNS123`, and click **Delete**.

3. **Empty & Delete S3 Bucket:**
   * Open `1-jan-2026-aws`, delete all remaining test files, and then delete the bucket from the S3 main page.

```


-----------------xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx--------------------


![alt text](27a.png)



![alt text](27b.png)


![alt text](27c.png)




---

## **Page: 27**

### **LAB Exercise: S3 Transfer Acceleration**

#### **Step 1: Configure Acceleration Endpoint**

```
                 Source Bucket (1-jan-2026-aws)
                               │
                               ▼
                           Properties
                               │
                               ▼
                     Transfer acceleration
                               │
                               ▼
                             Edit
                               │
                               ▼
                            [ Enable ]
                               │
                               ▼
                        Save changes ✓

```

---

#### **Step 2: Compare Transfer Speeds**

$$\longrightarrow \text{Transfer Acceleration speed comparison tool}$$

```
   User Location
         │
         ├─── Direct to S3 Bucket (Standard Internet) ───────> [ Standard Speed ]
         │
         └─── Via Edge Location ───> AWS Backbone Network ───> [ Accelerated Speed (Faster) ✓ ]

```

---

#### **Step 3: Access via Accelerated Endpoint**

* $\longrightarrow$ **Accelerated Endpoint Format:**
`1-jan-2026-aws.s3-accelerate.amazonaws.com`



-------------------xxxxxxxxxxxxxxxxxxxx-----------------------


![alt text](28a.png)



![alt text](28b.png)


![alt text](28c.png)


![alt text](28d.png)



---

## **Page: 28**

* $\longrightarrow$ **Status:**
* Enabled


* $\longrightarrow$ **Source Bucket:**
* **Source bucket name:** `1-jan-2026-aws`
* **Source Region:** Asia Pacific (Mumbai) `ap-south-1`


* $\longrightarrow$ **Choose rule scope:**
* Apply to all objects in the bucket


* $\longrightarrow$ **Destination:**
* Choose a bucket in this account
* **Bucket Name:** `Singapore-crr-01` *(Browse S3)*
* **IAM role:** Create new role



---

### **Verification / Testing Cross-Region Replication**

#### **Source Region (Mumbai):**

```
                     Buckets
                        │
                        ▼
                 1-jan-2026-aws
                        │
                        ▼
                     Upload  ───> (Upload a file User-Data-script)
                        │
                        ▼
                    Add file
                        │
                        ▼
                User-Data-script
                        │
                        ▼
                    Uploaded ✓

```

---

#### **Destination Region (Singapore):**

```
                 In Singapore-Region
                        │
                        ▼
                     Buckets
                        │
                        ▼
                 Singapore-crr-01
                        │
                        ▼
                User-Data-script
            (Same file received ✓)

```

---

$$\mathbf{—\mathbf{X}—}$$


-----------------xxxxxxxxxxxxxxxxxxxx------------------------



Here is the beginner-friendly guide for the **S3 Transfer Acceleration Lab** covering pages 27 and 28, formatted in clean Markdown for easy note-taking:

```markdown
# AWS Lab: S3 Transfer Acceleration (Pages 27–28)

---

## 🎯 Lab Overview

### Objective
To enable **Amazon S3 Transfer Acceleration** on an S3 bucket and test how AWS CloudFront's globally distributed Edge Locations speed up file uploads and downloads over long geographic distances.

### Purpose
This lab demonstrates how to optimize data transfers for globally distributed users. Standard uploads travel over the public internet, which can be slow and unreliable across long distances. S3 Transfer Acceleration routes traffic to the nearest AWS Edge Location, carrying data over AWS's optimized private backbone network to the destination bucket.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create the S3 Bucket
1. Log in to the **AWS Management Console** and navigate to **S3**.
2. Click **Create bucket**.
3. Configure the bucket details:
   * **Bucket type:** General purpose
   * **Bucket name:** `accelerated-storage-bucket-1` *(Names must be globally unique)*
   * **AWS Region:** Choose a region far from your physical location (e.g., `us-east-1` / N. Virginia) to clearly observe speed improvements.
4. Click **Create bucket**.

---

### Step 2: Enable Transfer Acceleration
1. Select your bucket: **`accelerated-storage-bucket-1`**.
2. Open the **Properties** tab.
3. Scroll down to the **Transfer acceleration** section and click **Edit**.
4. Select **Enable**.
5. Click **Save changes**.

---

### Step 3: Run the AWS Speed Comparison Tool
1. In the **Transfer acceleration** section, click the **Speed comparison tool** link (or visit `https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparision.html`).
2. Select your current region and test an upload.
3. **Observe Results:** The tool evaluates direct upload speeds vs. accelerated speeds from various global locations, showing the percentage increase in speed (e.g., *50% to 200% faster* via Edge Locations).

---

### Step 4: Access Objects via Accelerated Endpoint
1. Upload a file to your bucket (e.g., `sample-video.mp4`).
2. Compare the standard endpoint URL with the accelerated endpoint URL:
   * **Standard URL:** `https://accelerated-storage-bucket-1.s3.us-east-1.amazonaws.com/sample-video.mp4`
   * **Accelerated Endpoint URL:** `https://accelerated-storage-bucket-1.s3-accelerate.amazonaws.com/sample-video.mp4`
3. Use the **`s3-accelerate`** URL structure in your applications or CLI commands to route uploads through AWS Edge Locations.

---

## 🏗️ Architecture Flow


```

┌─────────────────────────────────────────────────────────────┐
│ Global User / Application                                   │
│                                                             │
│  Uploads File via:                                          │
│  accelerated-storage-bucket-1.s3-accelerate.amazonaws.com   │
└─────────────────────────────┬───────────────────────────────┘
│
│ 1. Connects to Nearest Edge Location
▼
┌─────────────────────────────────────────────────────────────┐
│ AWS Edge Location (Closest to User)                         │
│                                                             │
│  Routes data onto the AWS Private Backbone Network          │
└─────────────────────────────┬───────────────────────────────┘
│
│ 2. High-Speed Direct Transit
▼
┌─────────────────────────────────────────────────────────────┐
│ Target Amazon S3 Bucket                                     │
│ (accelerated-storage-bucket-1 in us-east-1)                 │
│                                                             │
│  File Saved Securely ✓                                       │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **AWS Backbone Network:** Transfer Acceleration uses AWS CloudFront Edge Locations to route traffic over AWS's fast, optimized internal network rather than the public internet.
* **Naming Constraint:** S3 Transfer Acceleration requires that the bucket name comply with DNS naming rules and **must not contain dots (`.`)**.
* **Billing:** Additional charges apply for data transferred via Transfer Acceleration. If AWS determines that Transfer Acceleration is not faster than a standard upload for a specific request, you are not charged for acceleration.

---

## 🧹 Post-Lab Cleanup

To avoid unexpected charges on your AWS account:

1. **Disable Transfer Acceleration:**
   * Go to `accelerated-storage-bucket-1` $\rightarrow$ **Properties** tab $\rightarrow$ **Transfer acceleration**.
   * Click **Edit**, select **Disable**, and click **Save changes**.

2. **Empty and Delete the S3 Bucket:**
   * Go to **S3 Console**, select `accelerated-storage-bucket-1`, and click **Empty**.
   * Type `permanently delete` to confirm and delete all files.
   * Return to the bucket list, select `accelerated-storage-bucket-1`, click **Delete**, enter the bucket name, and confirm.

```



-------------xxxxxxxxxxxxxxxxxxxxxxxxx-------------------



![alt text](29a.png)


![alt text](29b.png)


![alt text](29c.png)


![alt text](29d.png)


![alt text](29e.png)


---

## **Page: 29**

**Date:** 10/05/26 | **Day:** 31

### $\longrightarrow$ **S3 Static Website Hosting**

#### **Architecture Flowchart:**

```
                                 ┌─────────────────────────────────────────────────┐
                                 │                 (1) S3 Bucket                   │
                                 │   Name: technicalguruju.co.in                   │
                                 │   • Versioning: Enabled                         │
                                 │   • Static Website Hosting: Enabled             │
                                 │   • Stores: Web Content                         │
                                 └────────────────────────┬────────────────────────┘
                                                          ▲
                                                          │ (4)
                                                          │
 ┌──────────────────────┐   Forward to Route 53 (2) ┌─────┴─────────────┐
 │       GoDaddy        ├──────────────────────────>│     Route 53      │
 └──────────▲───────────┘                           └──────┬────────────┘
            │                                              │
            │ Update Name Servers                          │ (3)
            │ in GoDaddy                                   ▼
            │                                       ┌──────────────┐
            │                                       │ Hosted Zone  │
            │                                       └──────┬───────┘
            │                                              │
            │                                              ▼
            │                                       ┌──────────────┐
            │                                       │ Record Set   │
            │                                       └──────┬───────┘
            │                                              │
            │                                              ▼
            │                                       ┌──────────────────────┐
            │                                       │ 4 Name Servers       │
            └───────────────────────────────────────┤                      │
                                                    │ Create Record Set 53 │
                                                    └──────────────────────┘

                                     ▲
                                     │ technicalguruju.co.in
                                     │
                             ┌───────┴────────┐
                             │    Internet    │
                             └───────▲────────┘
                                     │ technicalguruju.co.in
                                     │
                                   [User]

```

---

#### **Workflow Overview:**

1. **S3 Bucket Configuration:**
* Bucket Name: `technicalguruju.co.in`
* Versioning $\longrightarrow$ Enabled
* Static website hosting $\longrightarrow$ Enabled


2. **Domain Forwarding:** Domain registered at GoDaddy forwards traffic to AWS Route 53.
3. **Route 53 Setup:**
* Create Hosted Zone $\longrightarrow$ Create Record Set
* Retrieve the 4 AWS Name Servers generated in Route 53 and update them back inside GoDaddy.


4. **User Access:** User requests `technicalguruju.co.in` over the internet, which routes through Route 53 to serve the website content stored in the S3 bucket.



-----------------xxxxxxxxxxxxxxxxxx----------------------


![alt text](30a.png)


![alt text](30b.png)


![alt text](30c.png)


---

## **Page: 30**

### $\longrightarrow$ **VPC Endpoint for S3**

> **Note (Translated from Hindi):** > *Internally, two AWS services communicate with each other with the help of Endpoints without needing the internet.*

#### **Overview Diagram:**

```
┌─────────────────────────────────────────────────────────────┐
│ AWS Cloud                                                   │
│                                                             │
│   ┌────────────────────────────────┐                        │
│   │ VPC                            │                        │
│   │   ┌────────────────────────┐   │                        │
│   │   │ Subnet                 │   │                        │
│   │   │   ┌────────┐           │   │    (Blocked)           │
│   │   │   │  EC2   ├───────────┼───┼───────────X──────────> Internet
│   │   │   └───┬────┘           │   │                        │
│   │   └───────┼────────────────┘   │                        │
│   │           │                    │                        │
│   │           ▼                    │                        │
│   │   ┌───────────────┐            │                        │
│   │   │ VPC Endpoint  │            │                        │
│   │   └───────┬───────┘            │                        │
│   └───────────┼────────────────────┘                        │
│               │ (Secure)                                    │
│               ▼                                             │
│   ┌──────────────────────┐                                  │
│   │    S3 Bucket         │                                  │
│   │  (URL / Data)        │                                  │
│   └──────────────────────┘                                  │
└─────────────────────────────────────────────────────────────┘

```

---

* An AWS VPC endpoint for Amazon S3 allows resources within a Virtual Private Cloud (VPC) to connect privately to S3 without traversing the public internet.
* This enhances security by keeping traffic within the AWS network and can reduce costs by avoiding NAT gateway charges.

---

#### **Detailed Network Architecture:**

```
User ───> Internet ───> IGW ───> [ VPC 1 : 10.0.0.0/16 ]
                                   │
                                   ├───> Public Subnet
                                   │       └─── SSH ───> [ EC2 (Public IP) ] ───(Jump Service)──┐
                                   │                                                            │
                                   └───> Private Subnet                                         │
                                           └───> [ EC2 (Private IP) ] <─────────────────────────┘
                                                       │
                                                       │ (Direct connection blocked X)
                                                       ▼
                                                ┌───────────────┐
                                                │ VPC Endpoint  │ ───> (Update in Route Table)
                                                └───────┬───────┘
                                                        │
                                                        ▼
                                                 ┌─────────────┐
                                                 │  S3 Bucket  │
                                                 └─────────────┘

```


------------------xxxxxxxxxxxxxxxxxxxxx--------------------


![alt text](31a.png)


![alt text](31b.png)


![alt text](31c.png)


![alt text](31d.png)



---

## **Page: 31**

### $\longrightarrow$ **EFS - Elastic File Share**

* **For Linux:** EFS
* **For Windows Server:** FSx

#### **Architecture Diagram:**

```
┌─────────────────────────────────────────────────────────────┐
│ Default VPC                                                 │
│                                                             │
│   ┌───────────────────────────┐   ┌─────────────────────┐   │
│   │ Subnet 1                  │   │ Subnet 2            │   │
│   │  ┌───────────────┐        │   │  ┌───────────────┐  │   │
│   │  │ Linux Server 1│──┐     │   │  │ Linux Server 2│  │   │
│   │  └───────┬───────┘  │     │   │  └───────┬───────┘  │   │
│   └──────────┼──────────┼─────┘   └──────────┼──────────┘   │
│              │          │ mount              │ mount        │
│              │          │                    │              │
│              │          ▼                    │              │
│              │   ┌───────────────┐           │              │
│              │   │   EFS         │           │              │
│              └──>│ Common Storage│<──────────┘              │
│                  └───────────────┘                          │
└─────────────────────────────────────────────────────────────┘

```

---

### $\longrightarrow$ **S3 - Granular - Policies (Bucket Access Control)**

#### **Access Flow Diagram:**

```
   [ Allowed Developer IP ]
             │
             ├──────> Only he accesses the bucket ✓
             │
             ▼
      ┌──────────────┐                             ┌───────────────────────────────────────┐
      │     User     │                             │ AWS                                   │
      │  /Developer  │                             │                                       │
      └──────┬───────┘                             │  Owner                                │
             │                                     │    │                                  │
             │ Policy:                             │    ▼                                  │
             ├── AWS User                          │  ┌─────────────┐                      │
             └── AWS Account ID                    │  │  S3 Bucket  │ Allow IP of           │
             │                                     │  │ ┌─────────┐ │ developer            │
             ▼                                     │  │ │  File   │ │                      │
      ┌──────────────┐                             │  │ └─────────┘ │                      │
      │   Internet   ├────────────────────────────>│  └──────┬──────┘                      │
      └──────▲───────┘                             │         │                             │
             │                                     │         ├── Private  ✗                │
     ┌───────┴───────┐                             │         └── Public   ✓                │
     │               │                             │         │                             │
  [ User 1 ]     [ User 2 ]                        │         └── Policy ──> IP allow       │
     (Blocked ✗)    (Blocked ✗)                    └───────────────────────────────────────┘

```

---

#### **Key Components:**

* **Developer Identification:** Policy matches specific AWS User / AWS Account ID / IP Address.
* **Bucket Access Restrictions:**
* **Private:** Disabled
* **Public:** Enabled *(with IP allowance rule)*


* **Policy Rule:** Explicit IP allowance that restricts bucket operations to authorized user IPs while blocking all unauthorized internet requests.



___________________xxxxxxxxxxxxxxxx_________________



![alt text](32a.png)


![alt text](32b.png)


![alt text](32c.png)


![alt text](32d.png)


![alt text](32e.png)



---

## **Page: 32**

### **LAB Exercise: AWS S3 Bucket Policy (Restricting Bucket Access by IP Address)**

#### **Step 1: Buckets Setup**

```
                     Buckets
                        │
                        ▼
                 1-jan-2026-aws
                        │
                        ▼
                   Permissions
                        │
                        ▼
                  Bucket policy
                        │
                        ▼
                      Edit

```

---

#### **Step 2: Policy Generator Setup**

$$\longrightarrow \text{Policy generator}$$

* $\longrightarrow$ **Select Policy Type:** S3 Bucket Policy
* $\longrightarrow$ **Effect:** Deny
* $\longrightarrow$ **Principal:** `*`
* $\longrightarrow$ **AWS Service:** Amazon S3
* $\longrightarrow$ **Actions:** All Actions `(*)`
* $\longrightarrow$ **Amazon Resource Name (ARN):** `arn:aws:s3:::1-jan-2026-aws/*`

---

#### **Step 3: Add Condition (IP Restriction)**

$$\longrightarrow \text{Add Condition (Optional)}$$

```
                 Add Condition Setup
                          │
                          ▼
             Condition: NotIpAddress
                          │
                          ▼
            Key: aws:SourceIp
                          │
                          ▼
            Value: [ Enter Your IP ]  ───> (e.g. 103.159.253.30/32)
                          │
                          ▼
                  Add Condition ✓

```

---

#### **Step 4: Generate & Save Policy**

```
               Add Statement
                     │
                     ▼
              Generate Policy
                     │
                     ▼
          Copy JSON Policy Text
                     │
                     ▼
          Paste into Bucket Policy
                     │
                     ▼
               Save Changes ✓

```



-----------------xxxxxxxxxxxxxxxxxxxx--------------------




![alt text](33a.png)


![alt text](33b.png)



![alt text](33c.png)


![alt text](33d.png)


---

## **Page: 33**

#### **Step 3: Access Control Setup**

```
                     Bucket
                        │
                        ▼
                paragdongre.shop
                        │
                        ▼
                   Permissions
                        │
                        ▼
            Access control list (ACL)
                        │
                        ▼
                      Edit

```

* **Everyone (public access):**
* **Objects:** Read ✓
* **Bucket ACL:** Read ✓



---

#### **Step 4: Go to Route 53 (for Domain Name Service)**

```
                  Hosted zones
                       │
                       ▼
              Create Hosted zone

```

* $\longrightarrow$ **Domain Name:** `paragdongre.shop` *(Same as purchased from GoDaddy)*
* $\longrightarrow$ **Type:** Public hosted zone

---

#### **DNS Configuration Flow:**

$$\longrightarrow \text{Copy name servers and paste into GoDaddy}$$

```
┌──────────────────────────────────────┐          ┌──────────────────────────────────────┐
│ AWS Route 53 (Hosted Zone)           │          │ GoDaddy DNS Management               │
│                                      │          │                                      │
│  Name Servers (NS Records):          │          │  Custom Nameservers:                 │
│  1. ns-xxxx.awsdns-xx.org ───────────┼─────────>│  1. ns-xxxx.awsdns-xx.org            │
│  2. ns-xxxx.awsdns-xx.co.uk ─────────┼─────────>│  2. ns-xxxx.awsdns-xx.co.uk          │
│  3. ns-xxxx.awsdns-xx.com ───────────┼─────────>│  3. ns-xxxx.awsdns-xx.com            │
│  4. ns-xxxx.awsdns-xx.net ───────────┼─────────>│  4. ns-xxxx.awsdns-xx.net            │
│                                      │          │                                      │
└──────────────────────────────────────┘          └──────────────────┬───────────────────┘
                                                                     │
                                                                     ▼
                                                                [ Save ] ✓

```



--------------------xxxxxxxxxxxxxxxxxxxxxx-------------------


![alt text](34a.png)


![alt text](34b.png)



![alt text](34c.png)


![alt text](34d.png)



![alt text](34e.png)




---

## **Page: 34**

#### **Step 5: Free Template Website Folder Upload**

```
                     Upload
                        │
                        ▼
                    Add files
                        │
                        ▼
          Free template website folder ───> (drag and drop each single folder)

```

* $\longrightarrow$ **Permissions:**
* $\longrightarrow$ **Access Control List (ACL):** Choose from predefined ACLs
* $\longrightarrow$ **Predefined ACLs:** Grant public-read access



---

#### **Step 6: Route 53 Configuration**

```
                  Route 53
                     │
                     ▼
               Create Record

```

* $\longrightarrow$ **Record Name:** `www.paragdongre.shop`
* $\longrightarrow$ **Record Type:** `A` – Routes traffic to an IPv4 address and some AWS resources
* $\longrightarrow$ **Alias:** Enabled ✓

##### **Traffic Routing Flow:**

```
┌─────────────────────────────────────────┐
│ Route 53 Alias Record                   │
│ Record Name: www.paragdongre.shop       │
└────────────────────┬────────────────────┘
                     │
                     │ Route traffic to
                     ▼
┌─────────────────────────────────────────┐
│ Alias to S3 Website Endpoint            │
│ Region: US East (N. Virginia)           │
│ Endpoint: s3-website-us-east-1.         │
│           amazonaws.com                 │
└─────────────────────────────────────────┘

```

---

#### **Step 7: Upload Files & Set Permissions**

```
                     Upload
                        │
                        ▼
                    Add files
                        │
                        ▼
             index.html OR syllabus file

```

* $\longrightarrow$ **Permissions:**
* $\longrightarrow$ **Access Control List (ACL):** Choose from predefined ACLs
* $\longrightarrow$ **Predefined ACLs:** Grant public-read access



------------------xxxxxxxxxxxxxxxxxxxxxxxxxxxx----------------------



Here is the complete, beginner-friendly Markdown guide combining **Pages 29 to 34** into one unified end-to-end lab.

You can copy the code block below directly into Visual Studio Code for your notes:

```markdown
# AWS Lab: S3 Static Website Hosting with Route 53 Custom Domain (Pages 29–34)

---

## 🎯 Lab Overview

### Objective
To host a static website on Amazon S3 using a custom domain name (e.g., `technicalguruju.co.in`) purchased from a domain registrar like GoDaddy, and route both the root domain (`technicalguruju.co.in`) and subdomain (`www.technicalguruju.co.in`) to the S3 bucket using **AWS Route 53**.

### Purpose
In a real-world scenario, clients want their websites accessible via their official web domain names rather than long, complex default AWS S3 endpoints. This lab demonstrates how to seamlessly map custom domain names to S3 static websites using public DNS hosted zones in Route 53.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Phase 1: Create and Configure S3 Buckets

> **Crucial Rule:** The S3 bucket name **MUST** exactly match your domain name!

#### Step 1: Create the Primary Root Bucket
1. Open the **Amazon S3 Console** and click **Create bucket**.
2. Configure settings:
   * **Bucket name:** Enter your exact root domain name (e.g., `technicalguruju.co.in`).
   * **AWS Region:** Select your preferred region (e.g., `ap-south-1` / Mumbai).
   * **Object Ownership:** Keep **ACLs disabled (recommended)** or enable if using ACLs.
   * **Block Public Access:** **Uncheck [ ] Block *all* public access** (Acknowledge the warning).
3. Click **Create bucket**.

#### Step 2: Upload Website Files to the Primary Bucket
1. Click on the `technicalguruju.co.in` bucket.
2. Click **Upload** $\rightarrow$ **Add files**.
3. Upload your website files (e.g., `index.html`, `error.html`, CSS/images).
4. Click **Upload**.

#### Step 3: Enable Static Website Hosting on Primary Bucket
1. Open the **Properties** tab of `technicalguruju.co.in`.
2. Scroll to the bottom to **Static website hosting** and click **Edit**.
3. Select **Enable**.
4. **Hosting type:** Choose **Host a static website**.
5. **Index document:** Type `index.html`.
6. Click **Save changes** and copy the generated S3 website endpoint URL.

#### Step 4: Create the Subdomain Bucket for Redirection
1. Click **Create bucket** again to set up the `www` redirect.
2. **Bucket name:** Enter `www.technicalguruju.co.in`.
3. Click **Create bucket**.
4. Open the **Properties** tab of `www.technicalguruju.co.in`.
5. Scroll to **Static website hosting** and click **Edit**.
6. Select **Enable**.
7. **Hosting type:** Choose **Redirect requests for an object**.
8. **Host name:** Enter your primary domain name (`technicalguruju.co.in`).
9. **Protocol:** Select `http` or `https`.
10. Click **Save changes**.

---

### Phase 2: Configure Route 53 Public Hosted Zone

#### Step 5: Create a Hosted Zone in Route 53
1. Search for **Route 53** in the top search bar and open the console.
2. Click **Hosted zones** in the left menu, then click **Create hosted zone**.
3. Configure settings:
   * **Domain name:** Enter your domain name (e.g., `technicalguruju.co.in`).
   * **Type:** Select **Public hosted zone**.
4. Click **Create hosted zone**.
5. AWS will automatically generate two records:
   * **NS Record** (Name Server records - contains 4 AWS name servers).
   * **SOA Record** (Start of Authority).

#### Step 6: Update Name Servers on Domain Registrar (GoDaddy)
1. Copy the 4 AWS Name Server addresses from the **NS Record** in Route 53.
2. Log in to your domain registrar account (e.g., GoDaddy / Namecheap).
3. Go to **DNS Management / Domain Settings** for `technicalguruju.co.in`.
4. Locate the **Nameservers** section and click **Change / Custom Nameservers**.
5. Replace the default registrar name servers with the 4 AWS Name Servers copied from Route 53.
6. Save the changes. *(Note: DNS propagation can take anywhere from a few minutes up to 24-48 hours)*.

---

### Phase 3: Create DNS Record Sets in Route 53

#### Step 7: Create 'A' Record for the Root Domain
1. In Route 53, open your hosted zone for `technicalguruju.co.in`.
2. Click **Create record**.
3. Leave **Record name** blank (this targets the root domain `technicalguruju.co.in`).
4. **Record type:** Select **A – Routes traffic to an IPv4 address and some AWS resources**.
5. Toggle the **Alias** switch to **ON**.
6. **Route traffic to:** Choose **Alias to S3 website endpoint**.
7. **Region:** Select the region where your bucket was created.
8. **S3 Endpoint:** Select your `technicalguruju.co.in` bucket.
9. Click **Create records**.

#### Step 8: Create 'A' Record (Alias) for the 'www' Subdomain
1. Click **Create record** again.
2. **Record name:** Type `www`.
3. **Record type:** Select **A – Routes traffic to an IPv4 address and some AWS resources**.
4. Toggle the **Alias** switch to **ON**.
5. **Route traffic to:** Choose **Alias to S3 website endpoint**.
6. **Region:** Select your bucket's region.
7. **S3 Endpoint:** Select your `www.technicalguruju.co.in` bucket.
8. Click **Create records**.

---

### Phase 4: Test & Verification

#### Step 9: Test Domain Resolution
1. Open a web browser and visit `http://technicalguruju.co.in`.
   * **Expected Result:** Your `index.html` page stored in S3 loads successfully!
2. Visit `http://www.technicalguruju.co.in`.
   * **Expected Result:** Traffic automatically redirects to `technicalguruju.co.in` and serves your website!

---

## 🏗️ Architecture Flow


```

┌─────────────────────────────────────────────────────────────┐
│ End User Browser Request                                    │
│ ([http://technicalguruju.co.in](https://www.google.com/url?sa=E&source=gmail&q=http://technicalguruju.co.in) OR [www.technicalguruju.co](https://www.google.com/search?q=https://www.technicalguruju.co).in) │
└─────────────────────────────┬───────────────────────────────┘
│
│ 1. DNS Query
▼
┌─────────────────────────────────────────────────────────────┐
│ AWS Route 53 (Public Hosted Zone)                           │
│                                                             │
│  - Root A Record Alias  ──►  S3 Bucket: technicalguruju.co.in
│  - www A Record Alias   ──►  S3 Bucket: [www.technicalguruju.co](https://www.google.com/search?q=https://www.technicalguruju.co).in
└─────────────────────────────┬───────────────────────────────┘
│
│ 2. Resolves to S3 Website Endpoint
▼
┌─────────────────────────────────────────────────────────────┐
│ Amazon S3 Bucket (Static Website Hosting)                   │
│                                                             │
│  - www Bucket Redirects ──► Root Bucket                     │
│  - Root Bucket Serves   ──► index.html Content ✓            │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Naming Matching:** S3 requires the bucket name to **exactly match** the domain name in Route 53 for Alias routing to work properly.
* **Alias Records vs CNAME:** AWS Route 53 Alias records allow you to point the root/apex domain (e.g., `example.com` without `www`) directly to S3 endpoints, which standard CNAME records cannot do.
* **Domain Propagation:** Updating name servers at your registrar transfers DNS management authority to AWS Route 53.

---

## 🧹 Post-Lab Cleanup

To avoid charges for public hosted zones ($0.50/month per zone):

1. **Delete Route 53 Records & Hosted Zone:**
   * Open **Route 53 Hosted zones** $\rightarrow$ select `technicalguruju.co.in`.
   * Delete the custom **A records** you created.
   * Click **Delete zone** to remove the hosted zone.

2. **Revert Name Servers at Registrar:**
   * Log into GoDaddy/Namecheap and switch the domain's name servers back to Default.

3. **Empty and Delete S3 Buckets:**
   * Open the **S3 Console**.
   * Empty and delete `www.technicalguruju.co.in`.
   * Empty and delete `technicalguruju.co.in`.

```




---------------------xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx---------------------------



![alt text](35a.png)


![alt text](35b.png)


![alt text](35c.png)


![alt text](35d.png)



---

## **Page: 35**

### $\longrightarrow$ **LAB for VPC Gateway Endpoint For S3**

#### **Step 1: Create VPC $\longrightarrow$ CIDR Setup**

1. **Create VPC** $\longrightarrow$ `10.0.0.0/16` (`VPC-1`)
2. **Create Subnet:**
* **public subnet** $\longrightarrow$ `10.0.1.0/24` $\longrightarrow$ `1a`
* **private subnet** $\longrightarrow$ `10.0.2.0/24` $\longrightarrow$ `1b`


3. **Create Internet Gateway:**
* `IGW-1` $\longrightarrow$ *(Attach to VPC: `VPC-1`)*


4. **Create Route Table:**

```
                     VPC-1 Route Tables
                             │
            ┌────────────────┴────────────────┐
            ▼                                 ▼
    Main Route Table                 Custom Route Table
    (Main-RT) [By default]           (custom-RT) [Create]

```

* $\longrightarrow$ **Create Custom Route Table:** `custom-RT`
* **Two important steps (a & b):**
* **a** $\longrightarrow$ **Routes**
* **b** $\longrightarrow$ **Subnet association:** `public subnet` ✓





---

#### **Step 2: Create Linux Server**

| Configuration Parameter | Public Server Configuration | Private Server Configuration |
| --- | --- | --- |
| **Server Type** | Public Server | Private Server |
| **VPC** | `VPC-1` | `VPC-1` |
| **Subnet** | `public subnet` | `private subnet` |
| **Auto-Assign Public IP** | **Enable** | **Disable** |
| **Security Group (SG)** | `VPC-Endpoint-SG` *(SSH allow)* | `VPC-Endpoint-SG` *(SSH allow)* |

---

#### **VPC Infrastructure Diagram:**

```
┌──────────────────────────────────────────────────────────────────┐
│ VPC-1 (10.0.0.0/16)                                              │
│                                                                  │
│  ┌──────────────────────────────┐ ┌───────────────────────────┐  │
│  │ Public Subnet (10.0.1.0/24)  │ │ Private Subnet            │  │
│  │                              │ │ (10.0.2.0/24)             │  │
│  │  ┌────────────────────────┐  │ │  ┌─────────────────────┐  │  │
│  │  │ Public Linux Server    │  │ │  │ Private Linux Server│  │  │
│  │  │ (Auto Public IP: Enable) │  │ │  │ (Auto IP: Disable)  │  │  │
│  │  │ Security Group:        │  │ │  │ Security Group:     │  │  │
│  │  │ VPC-Endpoint-SG        │  │ │  │ VPC-Endpoint-SG     │  │  │
│  │  └────────────────────────┘  │ │  └─────────────────────┘  │  │
│  └──────────────┬───────────────┘ └─────────────┬─────────────┘  │
│                 │                               │                │
│                 ▼                               ▼                │
│            custom-RT                         Main-RT             │
│                 │                                                │
└─────────────────┼────────────────────────────────────────────────┘
                  │
                  ▼
          Internet Gateway (IGW-1)

```


----------------------xxxxxxxxxxxxxxxxxxxxxxx-------------------------


![alt text](36a.png)



![alt text](36b.png)



![alt text](36c.png)


![alt text](36d.png)



---

## **Page: 36**

### **Step 3: Jump server from public server to private server**

```
Public Server (Public Subnet) ──► Public IP ✓
       │
       │ (From) [Hindi: से]
       ▼
Private Server (Private Subnet) ──► Public IP: Not Available ✗ [Hindi: public IP नहीं है]

```

* **Public Server** (`public subnet`)
* **Connect** $\longrightarrow$
```bash
vim key1.pem
chmod 700 key1.pem

```


* **SSH Command** *(for private server)* $\longrightarrow$ `key1.pem` $\longrightarrow$ *(Rename old key pair to `key1.pem`)*



---

### **Step 4: In private server**

```bash
sudo su
aws configure

```

| Prompt Field | Value / Action |
| --- | --- |
| **AWS Access Key ID [None]:** | `_____________________` *(Create Access Key and copy & paste ✓)* |
| **AWS Secret Access Key [None]:** | `_____________________` |
| **Default region name [None]:** | `ap-south-1` |
| **Default output format [None]:** | `json` |

---

* $\longrightarrow$ **For checking whether buckets show up or not:**
```bash
aws s3 ls

```


$\longrightarrow$ *(Does not show any bucket)* ✗

```
                     ┌──────────────────────────────┐
                     │     aws s3 ls returns        │
                     │  No buckets shown / Time out  │
                     └──────────────┬───────────────┘
                                    │ (?)
                                    ▼
                     ┌──────────────────────────────┐
                     │    Create VPC-Endpoint       │
                     │          (Step 5)            │
                     └──────────────────────────────┘

```


-------------------xxxxxxxxxxxxxxxxxxx----------------------


![alt text](37a.png)


![alt text](37b.png)


![alt text](37c.png)


![alt text](37d.png)


![alt text](37e.png)



---

## **Page: 37**

### **Verification (After creating VPC Endpoint):**

* $\longrightarrow$ **List Buckets:**
```bash
aws s3 ls

```


* `paragdongre.shop` *(Shows bucket in S3 ✓)*


* $\longrightarrow$ **To create bucket for Testing:**
```bash
aws s3 mb s3://vpcendpoint-bucket-test111

```



---

### **Step 5: Create Gateway VPC Endpoint**

```
                       VPC
                        │
                        ▼
                    Endpoints
                        │
                        ▼
                 Create Endpoint

```

* $\longrightarrow$ **Name tag:** `S3 endpoint`
* $\longrightarrow$ **Type:** AWS Services
* $\longrightarrow$ **Services:**
* **Service Name:** `com.amazonaws.ap-south-1.s3`


* $\longrightarrow$ **Type:** Gateway
* $\longrightarrow$ **VPC:** `VPC-1`

---

### **Step 6: Route Table Association**

```
                    Endpoints
                        │
                        ▼
                   S3 endpoint
                        │
                        ▼
                   Route tables
                        │
                        ▼
               Manage Route tables
                        │
                        ▼
            Main-RT (Private subnet)

```

---

### **Complete Endpoint Architecture Diagram:**

```
┌──────────────────────────────────────────────────────────┐
│ VPC-1                                                    │
│                                                          │
│  ┌──────────────────────────┐                            │
│  │ Private Subnet           │                            │
│  │                          │                            │
│  │  ┌────────────────────┐  │      Route Table Entry     │
│  │  │ Private Server     │  │     (Main-RT)              │
│  │  │  aws s3 ls ────────┼──┼───┐                        │
│  │  └────────────────────┘  │   │                        │
│  └──────────────────────────┘   │                        │
│                                 ▼                        │
│                       ┌──────────────────┐               │
│                       │ S3 VPC Endpoint  │               │
│                       │    (Gateway)     │               │
│                       └────────┬─────────┘               │
└────────────────────────────────┼─────────────────────────┘
                                 │ Private AWS Network
                                 ▼
                        ┌──────────────────┐
                        │ Amazon S3 Bucket │
                        │ paragdongre.shop │
                        └──────────────────┘

```

-------------------xxxxxxxxxxxxxxxxxxxxxxxxx---------------------


Here is the complete **VPC Gateway Endpoint for Amazon S3 Lab (Pages 35–37)** formatted in clean Markdown. You can easily copy the code block below directly into Visual Studio Code for your notes:

```markdown
# AWS Lab: VPC Gateway Endpoint for Amazon S3 (Pages 35–37)

---

## 🎯 Lab Overview

### Objective
To securely connect an EC2 instance residing in a **Private Subnet** to an **Amazon S3 Bucket** without using an Internet Gateway or NAT Gateway, utilizing an **AWS VPC Gateway Endpoint**.

### Purpose
In enterprise cloud architecture, databases and private application servers must not have direct public internet access for security reasons. However, these private servers often need to store or retrieve data from Amazon S3. A VPC Gateway Endpoint acts as a private bridge, routing traffic between your VPC and S3 entirely over AWS's secure internal network.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Phase 1: Network & EC2 Setup (Page 35)

#### Step 1: Create a Custom VPC Setup
1. Log in to the **AWS Management Console** and open the **VPC Console**.
2. Click **Create VPC** and set up the network components:
   * **VPC CIDR:** `10.0.0.0/16`
   * **Public Subnet:** `10.0.1.0/24` (Associated with an Internet Gateway)
   * **Private Subnet:** `10.0.2.0/24` (No Internet Gateway / No public access)
   * **Route Tables:** * `Public-Route-Table` (Route `0.0.0.0/0` $\rightarrow$ Internet Gateway)
     * `Private-Route-Table` (No route to `0.0.0.0/0`)

#### Step 2: Launch EC2 Instances
1. **Public EC2 Instance (Jump Server / Bastion Host):**
   * Launch a Linux EC2 instance inside the **Public Subnet**.
   * Enable **Auto-assign Public IP**.
2. **Private EC2 Instance:**
   * Launch a Linux EC2 instance inside the **Private Subnet**.
   * Disable Public IP assignment.

---

### Phase 2: Test Private Server Access (Page 36)

#### Step 3: Connect to Private Server via Jump Server
1. SSH into the **Public EC2 Instance** (Bastion Host) using its Public IP address.
2. From the Public Instance, SSH into the **Private EC2 Instance** using its Private IP (`10.0.2.x`).

#### Step 4: Verify S3 Access Fails (Without Endpoint)
1. On the Private EC2 instance, configure temporary AWS CLI credentials using `aws configure`.
2. Run the AWS CLI command to list S3 buckets:
   ```bash
   aws s3 ls

```

3. **Expected Result:** The command hangs and eventually times out. Because the instance is in a private subnet with no internet route or NAT Gateway, it cannot reach S3 over the public internet.

---

### Phase 3: Create & Verify Gateway Endpoint (Page 37)

#### Step 5: Create the VPC Gateway Endpoint for S3

1. Open the **VPC Console** $\rightarrow$ Click **Endpoints** in the left menu.
2. Click **Create endpoint**.
3. Configure the parameters:
* **Name tag:** `s3-vpc-gateway-endpoint`
* **Service category:** Choose **AWS services**.
* **Services:** Search for `s3` and select `com.amazonaws.<region>.s3` (Type: **Gateway**).
* **VPC:** Select your custom VPC (`10.0.0.0/16`).
* **Route tables:** Select your **`Private-Route-Table`**.
* **Policy:** Choose **Full Access**.


4. Click **Create endpoint**.

#### Step 6: Test & Verify S3 Access

1. Return to your SSH terminal on the **Private EC2 Instance**.
2. Run the S3 list command again:
```bash
aws s3 ls

```


3. **Expected Result:** The command returns instantly, listing all S3 buckets in your account!
4. Test uploading a file from the private server to S3:
```bash
aws s3 cp test-file.txt s3://your-bucket-name/

```


* **Result:** Upload succeeds over the private AWS network connection **✓**.



---

## 🏗️ Architecture Flow

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ Custom VPC (10.0.0.0/16)                                                        │
│                                                                                 │
│   ┌──────────────────────────────┐              ┌────────────────────────────┐  │
│   │ Public Subnet (10.0.1.0/24)  │              │ Private Subnet             │  │
│   │                              │              │ (10.0.2.0/24)              │  │
│   │   [ Public EC2 ]             │  SSH Access  │                            │  │
│   │   (Bastion Host)  ───────────┼─────────────►│   [ Private EC2 ]          │  │
│   └──────────────┬───────────────┘              └─────────────┬──────────────┘  │
│                  │                                            │                 │
│                  │ Internet Gateway                           │ Gateway         │
│                  ▼                                            │ Endpoint        │
│          (Public Internet)                                    ▼                 │
└───────────────────────────────────────────────────────────────┼─────────────────┘
                                                                │
                                                                │ Private Internal
                                                                │ AWS Network
                                                                ▼
                                                ┌────────────────────────────────┐
                                                │ Amazon S3 Storage              │
                                                │ (Secure Private Access ✓)      │
                                                └────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **No Extra Charges:** VPC Gateway Endpoints for Amazon S3 and DynamoDB are provided completely **free of charge** by AWS (unlike Interface Endpoints).
* **Automatic Route Updating:** When you create a Gateway Endpoint, AWS automatically inserts a destination prefix list entry into your selected Route Table pointing S3 traffic directly to the endpoint target (`vpce-xxx`).
* **Security & Isolation:** Sensitive workloads in private subnets can interact with S3 without opening any inbound or outbound internet ports.

---

## 🧹 Post-Lab Cleanup

To avoid charges for running EC2 instances:

1. **Delete VPC Gateway Endpoint:**
* Go to **VPC Console** $\rightarrow$ **Endpoints**.
* Select `s3-vpc-gateway-endpoint` and click **Delete endpoint**.


2. **Terminate EC2 Instances:**
* Go to **EC2 Console** $\rightarrow$ **Instances**.
* Select both the Public (Bastion) and Private instances, click **Instance state** $\rightarrow$ **Terminate instance**.


3. **Delete Custom VPC:**
* Go to **VPC Console** $\rightarrow$ **Your VPCs**.
* Select your custom VPC and click **Delete VPC** (this automatically cleans up associated subnets, route tables, and internet gateways).



```

```


---------------------xxxxxxxxxxxxxxxxxxxxxxxxxx---------------------------

![alt text](38a.png)


![alt text](38b.png)


![alt text](38c.png)



![alt text](38d.png)



![alt text](38e.png)


---

## **Page: 38**

### $\longrightarrow$ **LAB for Elastic File Storage (EFS)**

### **LAB for Create EFS and mount to linux machine**

#### **Step 1: Create Linux Server**

| Configuration Parameter | Linux Server-1 Configuration | Linux Server-2 Configuration |
| --- | --- | --- |
| **Server Name** | `Linux server-1` | `Linux server-2` |
| **VPC** | `Default VPC` | `Default VPC` |
| **Subnet** | `Subnet-1a` | `Subnet-1b` |
| **Auto-Assign Public IP** | **Enable** | **Enable** |
| **Security Group (SG)** | `EFS-SG`<br>

<br>• SSH allow<br>

<br>• NFS allow | `EFS-SG`<br>

<br>• SSH allow<br>

<br>• NFS allow |

---

#### **Step 2: Create EFS File System**

```
                   EFS
                    │
                    ▼
           Create file system

```

* $\longrightarrow$ **Name:** `EFS-Mumbai-1`
* $\longrightarrow$ **VPC:** `Default VPC`

---

#### **Step 3: Configure EFS Security Group**

```
                   EFS
                    │
                    ▼
             EFS-Mumbai-1
                    │
                    ▼
                 Network
                    │
                    ▼
                  Manage
                    │
                    ▼
                  EFS-SG

```

* **For EFS file system:**

$$\downarrow$$



`EFS-Mumbai-1`

$$\downarrow$$



Select a security group (SG): **`EFS-SG` only** ✓

---

#### **EFS Multi-Subnet Architecture Diagram:**

```
┌─────────────────────────────────────────────────────────────┐
│ Default VPC                                                 │
│                                                             │
│  ┌────────────────────────┐     ┌────────────────────────┐  │
│  │ Subnet-1a              │     │ Subnet-1b              │  │
│  │                        │     │                        │  │
│  │  ┌──────────────────┐  │     │  ┌──────────────────┐  │  │
│  │  │ Linux Server-1   │  │     │  │ Linux Server-2   │  │  │
│  │  │ SG: EFS-SG       │  │     │  │ SG: EFS-SG       │  │  │
│  │  │ (SSH + NFS)      │  │     │  │ (SSH + NFS)      │  │  │
│  │  └────────┬─────────┘  │     │  └────────┬─────────┘  │  │
│  └───────────┼────────────┘     └───────────┼────────────┘  │
│              │                              │               │
│              │       NFS Traffic (Port 2049)│               │
│              └──────────────┬───────────────┘               │
│                             │                               │
│                             ▼                               │
│                  ┌──────────────────────┐                   │
│                  │ EFS-Mumbai-1         │                   │
│                  │ SG: EFS-SG           │                   │
│                  └──────────────────────┘                   │
└─────────────────────────────────────────────────────────────┘

```


------------------xxxxxxxxxxxxxxxxxxxx---------------------



![alt text](39a.png)



![alt text](39b.png)


![alt text](39c.png)


![alt text](39d.png)



---

## **Page: 39**

### **Step 4: Linux Server-1 $\longrightarrow$ Connect**

```bash
sudo su
yum install amazon-efs-utils -y
mkdir efs

```

> **Note:** Connect this directory or folder to EFS.

```bash
sudo mount...

```

> **Instruction to paste command:**
> Copy `sudo mount` command from **S3** $\rightarrow$ **File systems** $\rightarrow$ **EFS-Mumbai-1** $\rightarrow$ **Attach using the EFS mount helper**:
> `sudo mount...` *(Copy and paste)*

```bash
cd efs
touch file1

```

---

### **Step 5: Linux Server-2 $\longrightarrow$ Connect**

```bash
sudo su
yum install amazon-efs-utils -y
ls
mkdir efs
ls
sudo mount...    (Paste)
cd efs
ls
file1 ──────────────────────► Visible ✓

```

---

### **Shared EFS Mounting Workflow Diagram:**

```
┌──────────────────────────────────────────────┐
│             Linux Server-1                   │
│                                              │
│ 1. yum install amazon-efs-utils -y           │
│ 2. mkdir efs                                 │
│ 3. sudo mount [EFS Mount Helper Command]     │
│ 4. cd efs && touch file1                     │
└──────────────────────┬───────────────────────┘
                       │
                       │ Creates 'file1' in shared storage
                       ▼
            ┌─────────────────────┐
            │  EFS (EFS-Mumbai-1) │
            └──────────┬──────────┘
                       ▲
                       │ Reads shared data
                       │
┌──────────────────────┴───────────────────────┐
│             Linux Server-2                   │
│                                              │
│ 1. yum install amazon-efs-utils -y           │
│ 2. mkdir efs                                 │
│ 3. sudo mount [EFS Mount Helper Command]     │
│ 4. cd efs && ls ──► file1 (Visible ✓)         │
└──────────────────────────────────────────────┘

```

--------------------xxxxxxxxxxxxxxxxxxxxxxxxxx----------------------



Here is the complete **Amazon Elastic File System (EFS) Lab (Pages 38–39)** formatted in clean Markdown for your Visual Studio Code notes:

```markdown
# AWS Lab: Amazon Elastic File System (EFS) Shared Storage (Pages 38–39)

---

## 🎯 Lab Overview

### Objective
To create an **Amazon Elastic File System (EFS)** and mount it simultaneously onto two separate Linux EC2 instances so both instances can share, read, and write to a common file system in real time.

### Purpose
Unlike Amazon EBS (Elastic Block Store) volumes, which are typically attached to a single EC2 instance at a time, **Amazon EFS** provides serverless, network-attached file storage using the **NFSv4** protocol. This allows hundreds of EC2 instances to access the exact same files at the same time, making it ideal for web server farms, content management systems (like WordPress), and shared data repositories.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create a Security Group for EFS
Before creating the file system, set up a security group that allows Network File System (NFS) traffic on port `2049`.

1. Open the **EC2 Console** $\rightarrow$ Click **Security Groups** in the left menu.
2. Click **Create security group**.
3. Configure details:
   * **Security group name:** `efs-sg`
   * **Description:** Allow NFS traffic for EFS
   * **VPC:** Select your default VPC.
4. **Inbound rules:** Click **Add rule**:
   * **Type:** Select **NFS** (Port `2049`).
   * **Source:** Select **Anywhere-IPv4** (`0.0.0.0/0`) or choose your EC2 security group.
5. Click **Create security group**.

---

### Step 2: Launch Two Linux EC2 Instances
1. Open the **EC2 Console** $\rightarrow$ Click **Launch instance**.
2. Launch **Server 1**:
   * **Name:** `Linux-Server-1`
   * **AMI:** Amazon Linux 2 or Amazon Linux 2023
   * **Instance Type:** `t2.micro` (Free Tier eligible)
   * **Key Pair:** Select your SSH key pair.
   * **Network Settings:** Assign to Subnet A / Availability Zone 1.
3. Launch **Server 2**:
   * **Name:** `Linux-Server-2`
   * **Network Settings:** Assign to Subnet B / Availability Zone 2 *(to test multi-AZ shared access)*.

---

### Step 3: Create the Amazon EFS File System
1. Open the **EFS Console** by searching for **EFS** in the top search bar.
2. Click **Create file system**.
3. Configure file system parameters:
   * **Name:** `my-shared-efs`
   * **Virtual Private Cloud (VPC):** Select your default VPC.
4. Click **Customize** to verify Mount Targets:
   * Under **Network**, ensure Mount Targets are created for each Availability Zone.
   * Replace default security groups with the **`efs-sg`** security group created in Step 1.
5. Click **Create**.

---

### Step 4: Mount EFS on Linux Server 1
1. Connect to **`Linux-Server-1`** via SSH or EC2 Instance Connect.
2. Install the Amazon EFS helper utility:
   ```bash
   sudo yum install -y amazon-efs-utils

```

3. Create a mount directory:
```bash
sudo mkdir /efs

```


4. Copy the EFS mount helper command from the EFS Console (click **Attach** on your EFS details page):
```bash
sudo mount -t efs -o tls fs-12345678:/ /efs

```


5. Create a test file in the shared directory:
```bash
echo "Hello from Linux Server 1" | sudo tee /efs/shared-test.txt

```



---

### Step 5: Mount EFS on Linux Server 2 & Verify Shared Access

1. Connect to **`Linux-Server-2`** via SSH.
2. Install the EFS helper utility and create the directory:
```bash
sudo yum install -y amazon-efs-utils
sudo mkdir /efs

```


3. Run the exact same mount command on **`Linux-Server-2`**:
```bash
sudo mount -t efs -o tls fs-12345678:/ /efs

```


4. Check the contents of the `/efs` folder on Server 2:
```bash
cat /efs/shared-test.txt

```


5. **Expected Result:** The file created by Server 1 (`Hello from Linux Server 1`) instantly appears on Server 2 **✓**!

---

## 🏗️ Architecture Flow

```
┌─────────────────────────────────────────────────────────────┐
│ AWS VPC                                                     │
│                                                             │
│   ┌─────────────────────────┐   ┌─────────────────────────┐ │
│   │ Availability Zone A     │   │ Availability Zone B     │ │
│   │                         │   │                         │ │
│   │  [ Linux Server 1 ]     │   │  [ Linux Server 2 ]     │ │
│   │  Mount point: /efs      │   │  Mount point: /efs      │ │
│   └────────────┬────────────┘   └────────────┬────────────┘ │
│                │                             │              │
│                │ Port 2049 (NFS)             │ Port 2049    │
│                ▼                             ▼              │
│   ┌───────────────────────────────────────────────────────┐ │
│   │ Amazon EFS (Elastic File System)                      │ │
│   │ Shared Storage: /efs/shared-test.txt                  │ │
│   └───────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Shared Access Across AZs:** Unlike Amazon EBS (which is limited to a single Availability Zone), EFS automatically replicates data across multiple Availability Zones in a region for concurrent access.
* **Security Group Traffic:** To allow instances to talk to EFS, the EFS Security Group **must** explicitly allow inbound **NFS traffic on Port 2049**.
* **Elastic Scaling:** EFS automatically grows and shrinks as files are added or removed—you do not need to pre-provision storage capacity.

---

## 🧹 Post-Lab Cleanup

To avoid charges for running EC2 instances and stored EFS data:

1. **Unmount EFS on Both Servers:**
```bash
sudo umount /efs

```


2. **Terminate EC2 Instances:**
* Open the **EC2 Console** $\rightarrow$ Select `Linux-Server-1` and `Linux-Server-2`.
* Click **Instance state** $\rightarrow$ **Terminate instance**.


3. **Delete Amazon EFS File System:**
* Open the **EFS Console** $\rightarrow$ Select `my-shared-efs`.
* Click **Delete** and enter the file system ID to confirm deletion.


4. **Delete Security Group:**
* Delete the `efs-sg` security group from the EC2 Security Groups page.



```

```


--------------------xxxxxxxxxxxxxxxxxxxxxxx-------------------------------

![alt text](40a.png)


![alt text](40b.png)


![alt text](40c.png)


![alt text](40d.png)


![alt text](40e.png)



---

## **Page: 40**

### $\rightarrow$ **LAB for S3 Granular Policies**

### $\rightarrow$ **LAB for Managing S3 Bucket Policies for granular access.**

---

#### **Step 1: Create Bucket**

* $\rightarrow$ **Bucket Type:** General purpose
* $\rightarrow$ **Bucket Namespace:** Global Namespace
* $\rightarrow$ **Bucket Name:** `granular-access-bucket`
* $\rightarrow$ **Object ownership:** ACLs disabled
* $\rightarrow$ **Block public Access settings for this bucket:**
* [✓] **Block all public access**


* $\rightarrow$ **Bucket Versioning:** Enabled

---

#### **Step 2: Configure Bucket Policy**

```
                 Bucket
                   │
                   ▼
        granular-access-bucket
                   │
                   ▼
              Permissions
                   │
                   ▼
             Bucket policy
                   │
                   ▼
                 Edit

```

* $\rightarrow$ **Copy and paste code:**
* How to give access of S3 object to specific IP Address:
* Enter/edit IP Address *(For those given access ✓)*


* $\rightarrow$ **Change:**
* **Bucket ARN** *(Copy & paste in code)*



---

#### **Step 3: Upload Object**

* **Upload** $\longrightarrow$ *(Upload a file)*

$$\downarrow$$



**Add files**

$$\downarrow$$



`AWS Diploma syllabus`

---

#### **Step 4: Verification**

* Those IPs that are allowed *(given access)* can view/access the files. **✓**
* All other IP addresses are denied. **✗**

---

### **S3 Granular IP-Based Access Architecture Diagram:**

```
                  ┌─────────────────────────────────┐
                  │          Internet               │
                  └──────────────┬──────────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
                 ▼                               ▼
       ┌──────────────────┐            ┌──────────────────┐
       │   Allowed IP     │            │  Other IP        │
       │   (Your IP)      │            │  (Unauthorized)  │
       └────────┬─────────┘            └────────┬─────────┘
                │                               │
                │ Request Access                │ Request Access
                ▼                               ▼
     ┌──────────────────────────────────────────────────┐
     │ Amazon S3 Bucket: granular-access-bucket         │
     │                                                  │
     │  ┌────────────────────────────────────────────┐  │
     │  │ Bucket Policy (IP Condition Verification) │  │
     │  └─────────────────────┬──────────────────────┘  │
     │                        │                         │
     │         ┌──────────────┴──────────────┐          │
     │         ▼                             ▼          │
     │   [ IP Match ]                 [ IP Mismatch ]   │
     │         │                             │          │
     │         ▼                             ▼          │
     │  Access Granted ✓             Access Denied ✗    │
     │  (AWS Diploma syllabus)       (403 Forbidden)    │
     └──────────────────────────────────────────────────┘

```

-------------------xxxxxxxxxxxxxxxxxxxxxxxxx--------------------



Here is the complete **S3 Granular Bucket Access Policy Lab (Page 40)** formatted in clean Markdown for your Visual Studio Code notes:

```markdown
# AWS Lab: S3 Granular Access Control using Bucket Policies (Page 40)

---

## 🎯 Lab Overview

### Objective
To configure an **Amazon S3 Bucket Policy** that explicitly restricts bucket access based on specific client IP addresses, granting access to an authorized developer IP while denying access to all other unauthorized IP addresses.

### Purpose
While S3 Block Public Access provides high-level security, real-world enterprise applications often require **granular access control**. Bucket policies allow you to write JSON-based policy rules to enforce strict security boundaries—such as restricting S3 access exclusively to your corporate office network or specific developer IP addresses.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create the S3 Bucket
1. Log in to the **AWS Management Console** and navigate to **S3**.
2. Click **Create bucket**.
3. Configure the bucket settings:
   * **Bucket type:** General purpose
   * **Bucket name:** `ip-restricted-s3-bucket-40` *(Names must be globally unique)*
   * **AWS Region:** Select your preferred region (e.g., `ap-south-1` / Mumbai).
   * **Bucket Versioning:** Select **Enable**.
   * **Block Public Access:** Keep **[✓] Block *all* public access** enabled.
4. Click **Create bucket**.

---

### Step 2: Identify Your Public IP Address
Before writing the bucket policy, find your current public IP address:
1. Open a new browser tab and go to `https://checkip.amazonaws.com` or search Google for `"what is my ip"`.
2. Note down your IPv4 address (e.g., `203.0.113.25`).

---

### Step 3: Configure the IP-Restricting Bucket Policy
1. Open your newly created bucket: **`ip-restricted-s3-bucket-40`**.
2. Go to the **Permissions** tab.
3. Scroll down to the **Bucket policy** section and click **Edit**.
4. Paste the following JSON policy (replace `YOUR_PUBLIC_IP` with your actual IP address from Step 2, and update the bucket name):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowSpecificIPOnly",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::ip-restricted-s3-bucket-40",
                "arn:aws:s3:::ip-restricted-s3-bucket-40/*"
            ],
            "Condition": {
                "NotIpAddress": {
                    "aws:SourceIp": "YOUR_PUBLIC_IP/32"
                }
            }
        }
    ]
}

```

5. Click **Save changes**.

---

### Step 4: Test & Verify Granular Access

#### Test 1: Access from Authorized Developer IP

1. Go to the **Objects** tab of `ip-restricted-s3-bucket-40`.
2. Click **Upload** $\rightarrow$ **Add files** and upload a test file (e.g., `AWS Diploma syllabus.pdf`).
3. Click on the uploaded file and click **Download** or view its properties.
4. **Expected Result:** Upload and download operations succeed because your current IP matches the allowed `aws:SourceIp` condition.

#### Test 2: Access from Unauthorized IP (Mobile Hotspot / VPN)

1. Switch your computer's internet connection to a mobile hotspot or connect via a VPN service (this changes your public IP address).
2. Refresh the S3 bucket console or attempt to list/download the object.
3. **Expected Result:** AWS returns an **`AccessDenied` (403 Forbidden)** error! The explicit `Deny` condition blocks all requests originating from any IP other than your designated IP.

---

## 🏗️ Architecture Flow

```
┌─────────────────────────────────────────────────────────────┐
│ Incoming Request to Amazon S3 Bucket                        │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              │ Evaluates Source IP Address
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ S3 Bucket Policy (Condition: NotIpAddress)                  │
│                                                             │
│   Is Request IP == Developer Allowed IP (e.g., 203.0.113.25)?│
└──────────────┬──────────────────────────────┬───────────────┘
               │                              │
               │ YES                          │ NO
               ▼                              ▼
┌───────────────────────────┐  ┌──────────────────────────────┐
│ Access Granted ✓          │  │ Access Denied (403) ✗        │
│ (Upload / Download Allowed│  │ (Blocked by Explicit Deny)   │
└───────────────────────────┘  └──────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Explicit Deny Overrides All:** In AWS IAM and bucket policies, an explicit `"Effect": "Deny"` always overrides any `"Allow"` permissions.
* **`NotIpAddress` Condition:** Using `"NotIpAddress"` combined with `"Deny"` is a powerful security pattern that blocks everyone in the world *except* the trusted IP range defined in your rule.
* **Lockout Caution:** Be careful when applying strict Deny policies! If you enter the wrong IP address, you can lock yourself out of the bucket until an AWS account root user updates the policy.

---

## 🧹 Post-Lab Cleanup

To avoid leaving restrictive policies or unwanted data in your AWS account:

1. **Delete the Bucket Policy:**
* Open `ip-restricted-s3-bucket-40` $\rightarrow$ **Permissions** tab.
* Scroll down to **Bucket policy** and click **Delete**.


2. **Empty and Delete the Bucket:**
* Go to the **Objects** tab, select all files, click **Delete**, type `permanently delete`, and confirm.
* Go to the main **S3 Buckets** list, select `ip-restricted-s3-bucket-40`, click **Delete**, type the bucket name, and confirm.



```

```



---------------------xxxxxxxxxxxxxxxxxxxxxxxxxxxx----------------------------


![alt text](41a.png)


![alt text](41b.png)


![alt text](41c.png)


![alt text](41d.png)




---

## **Page: 41**

### $\rightarrow$ **LAB for S3 Object Lock**

---

#### **Step 1: Create Bucket**

* $\rightarrow$ **Bucket Type:** General purpose
* $\rightarrow$ **Bucket Namespace:** Global Namespace
* $\rightarrow$ **Bucket Name:** `object-lock-s3-123`
* $\rightarrow$ **Object ownership:** ACLs disabled
* $\rightarrow$ **Block public object bucket for this bucket:**
* [✓] **Block all public access**


* $\rightarrow$ **Bucket Versioning:** Enabled

---

#### **Step 2: Configure Object Lock**

```
                 Bucket
                   │
                   ▼
          object-lock-s3-123
                   │
                   ▼
               Properties
                   │
                   ▼
              Object lock
                   │
                   ▼
             Default retention
                   │
                   ▼
                 Enable

```

* $\rightarrow$ **Default retention mode:** Compliance
* $\rightarrow$ **Default retention period:** 1 Days

> **Note (Translated from Hindi):**
> { Retention period is set for as many Days as specified; the bucket will **not** be deleted until those Days pass **✗**. It will be deleted **after** that period **✓**. }
> { Here, we select the Days up to which the bucket is **not** deleted up to this number of days. }

---

### **S3 Object Lock (Compliance Mode) Lifecycle Diagram:**

```
                     ┌──────────────────────────────────────┐
                     │ Bucket: object-lock-s3-123           │
                     │ Mode: Compliance | Period: 1 Day     │
                     └──────────────────┬───────────────────┘
                                        │
                                        │ Object Uploaded
                                        ▼
                   ┌──────────────────────────────────────────┐
                   │    Retention Period Active (Day 0 - 1)   │
                   └────────────────────┬─────────────────────┘
                                        │
             ┌──────────────────────────┴──────────────────────────┐
             │                                                     │
             ▼                                                     ▼
    [ Delete Attempt ]                                   [ After 1 Day Passes ]
             │                                                     │
             ▼                                                     ▼
     Access Denied ✗                                      Deletion Allowed ✓
(Cannot be overwritten or                              (Objects can now be
 deleted by ANY user, including                         overwritten or deleted)
  the root user in Compliance mode)

```


---------------xxxxxxxxxxxxxxxxxxxxxxxxxxxxx---------------------




![alt text](42a.png)



![alt text](42b.png)


![alt text](42c.png)



![alt text](42d.png)




---

## **Page: 42**

#### **Step 3: Upload**

$$\downarrow$$


**Add files**


$$\downarrow$$


`AWS Diploma syllabus`

---

#### **Step 4: Delete and Recovery Test**

```
                Bucket
                  │
                  ▼
          object-lock-s3-123
                  │
                  ▼
        AWS Diploma syllabus
                  │
                  ▼
                Delete

```

* $\longrightarrow$ `object-lock-s3-123`

$$\downarrow$$



[✓] **Show versions**

$$\downarrow$$



`AWS Diploma syllabus`

$$\downarrow$$



**Delete** *(Delete Marker)* $\longrightarrow$ (It recovers **✓**)

$$\downarrow$$



`AWS Diploma syllabus` **✓**

---

#### **Step 5: Bucket Deletion Comparison**

* $\longrightarrow$ **Bucket** $\longrightarrow$ **(Without Object Lock):**
* **Empty:** **✓ (Yes)**
* **Deleted:** **✓ (Yes)**


* $\longrightarrow$ **Bucket** $\longrightarrow$ **(With Object Lock):**
* `object-lock-s3-123`
* **Empty:** **✗ (NO)**
* **Deleted:** **✗ (NO)**



> **Note (Translated from Hindi):**
> { Individual objects will get deleted, but a **Delete Marker** will be created for them. }

---

### **Object Lock Deletion Behavior Diagram:**

```
Standard Bucket vs Object Lock Bucket Deletion Flow
─────────────────────────────────────────────────────────────────

[ STANDARD BUCKET ]
  1. Delete Files ──► Files Permanently Removed
  2. Empty Bucket ──► Success ✓
  3. Delete Bucket ──► Success ✓

─────────────────────────────────────────────────────────────────

[ BUCKET WITH OBJECT LOCK ]
  1. Delete File  ──► Creates "Delete Marker" (File hidden, not destroyed)
  2. Recover File ──► Delete "Delete Marker" ──► File restored ✓
  3. Empty Bucket ──► FAILS ✗ (Retention prevents deleting base versions)
  4. Delete Bucket ──► FAILS ✗ (Bucket must be empty first)

```

-----------------xxxxxxxxxxxxxxxxxxxxxxxxxx----------------------



Here is the complete **Amazon Macie Data Security and PII Discovery Lab (Pages 41–42)** formatted in clean Markdown for your Visual Studio Code notes:

```markdown
# AWS Lab: Discovering Sensitive Data (PII) using Amazon Macie (Pages 41–42)

---

## 🎯 Lab Overview

### Objective
To enable **Amazon Macie** on an AWS account and run a automated data discovery job against an Amazon S3 bucket to detect, classify, and protect **Personally Identifiable Information (PII)** (such as credit card numbers, social security numbers, or email addresses).

### Purpose
Organizations store massive amounts of unstructured data in Amazon S3. Manually searching millions of files for sensitive personal or financial information is impossible. Amazon Macie uses machine learning and pattern matching to automatically discover, classify, and generate security alerts for sensitive data stored in S3, ensuring compliance with data privacy regulations like GDPR and HIPAA.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create an S3 Bucket & Upload Sensitive Test Data
1. Log in to the **AWS Management Console** and open **S3**.
2. Click **Create bucket**.
   * **Bucket name:** `macie-pii-test-bucket-41` *(Must be globally unique)*
   * **AWS Region:** Select your default region (e.g., `ap-south-1` / Mumbai).
3. Click **Create bucket**.
4. Create a local sample text file on your computer named `customer_data.txt` with dummy test data:
   ```text
   John Doe, john.doe@example.com, Credit Card: 4532-1234-5678-9012
   Jane Smith, jane.smith@example.com, SSN: 000-12-3456

```

5. Open `macie-pii-test-bucket-41` $\rightarrow$ Click **Upload** $\rightarrow$ **Add files** $\rightarrow$ Upload `customer_data.txt`.

---

### Step 2: Enable Amazon Macie

1. Search for **Macie** in the top search bar and open the Amazon Macie Console.
2. Click **Get started**.
3. Click the orange **Enable Macie** button. *(Note: AWS provides a 30-day free trial for Macie)*.

---

### Step 3: Create and Run a Sensitive Data Discovery Job

1. In the Macie left navigation menu, click **Jobs**.
2. Click **Create job**.
3. **Select S3 Buckets:**
* Select your bucket: `macie-pii-test-bucket-41`.
* Click **Next**.


4. **Review bucket selection:** Confirm the selected bucket and click **Next**.
5. **Refine the scope:**
* **Job type:** Select **One-time job** *(Runs once immediately)*.
* Keep default sampling settings (100% data inspection).
* Click **Next**.


6. **Managed data identifiers:** Keep **All** selected so Macie checks for all standard PII types (credit cards, names, SSNs, national IDs).
7. **Job details:**
* **Job name:** `PII-Discovery-Job-01`


8. Click **Next**, review the configuration, and click **Submit**.

---

### Step 4: Review Macie Findings & PII Alerts

1. On the Jobs page, wait for the status of `PII-Discovery-Job-01` to change from *Running* to **Complete** *(Takes 3–5 minutes)*.
2. In the left navigation menu, click **Findings**.
3. **Expected Result:** Macie generates a high-severity finding alert:
* **Finding Type:** `Personal Data / Credentials / Financial Info`
* **Affected Resource:** `s3://macie-pii-test-bucket-41/customer_data.txt`
* **Detected Categories:** Credit Card Numbers, Email Addresses, Social Security Numbers **✓**.



---

## 🏗️ Architecture Flow

```
┌─────────────────────────────────────────────────────────────┐
│ 1. Amazon S3 Bucket (macie-pii-test-bucket-41)              │
│                                                             │
│    Stores unstructured files containing sample data          │
│    (customer_data.txt: Credit Cards, SSNs, Emails)          │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              │ Automated Scanning
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Amazon Macie (Machine Learning Data Discovery)           │
│                                                             │
│    - Evaluates data using Managed Data Identifiers          │
│    - Classifies PII & Sensitive Information Patterns         │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              │ Generates Security Alert
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Macie Findings Console                                   │
│                                                             │
│    Alert: PII Found in customer_data.txt                    │
│    Categories: Credit Cards, SSNs, Email Addresses ✓        │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Automated Data Classification:** Macie uses built-in pattern matching algorithms and machine learning to scan files (PDFs, CSVs, TXT, JSON, DOCX) for sensitive PII data without human manual review.
* **Proactive Security:** Macie helps organizations audit their S3 buckets to ensure compliance before sensitive data is accidentally exposed or leaked publicly.
* **Managed vs Custom Identifiers:** Macie provides out-of-the-box **Managed Identifiers** for standard PII (passports, SSNs, driver's licenses) and allows you to create **Custom Identifiers** (e.g., custom employee IDs).

---

## 🧹 Post-Lab Cleanup

To avoid charges after testing Macie:

1. **Delete the Discovery Job & Findings:**
* Open **Macie Console** $\rightarrow$ **Jobs** $\rightarrow$ Select `PII-Discovery-Job-01` $\rightarrow$ Click **Action** $\rightarrow$ **Delete**.


2. **Disable Amazon Macie:**
* Go to **Macie Console** $\rightarrow$ **Settings**.
* Scroll down and click **Disable Macie** to stop any background monitoring costs.


3. **Empty and Delete the S3 Bucket:**
* Open the **S3 Console**.
* Select `macie-pii-test-bucket-41`, click **Empty**, type `permanently delete`, and confirm.
* Return to the buckets list, select `macie-pii-test-bucket-41`, click **Delete**, enter the bucket name, and confirm.



```

```


------------------xxxxxxxxxxxxxxxxxxxxx-------------------------


![alt text](43a.png)


![alt text](43b.png)


![alt text](43c.png)




---

## **Page: 43**

### $\rightarrow$ **LAB for AWS CloudTrail Data Events**

---

#### **Step 1: Create Bucket**

---

#### **Step 2: Configure CloudTrail Data Events**

```
                 Bucket
                   │
                   ▼
          object-lock-s3-123
                   │
                   ▼
               Properties
                   │
                   ▼
     AWS CloudTrail data events
                   │
                   ▼
      Click on AWS CloudTrail
                   │
                   ▼
             Event history
                   │
                   ▼
               Check logs

```

---

### **AWS CloudTrail S3 Data Event Logging Workflow Diagram:**

```
┌────────────────────────────────────────────────────────┐
│               Amazon S3 Bucket                         │
│             (object-lock-s3-123)                       │
│                                                        │
│  [ Properties ] ──► [ Enable CloudTrail Data Events ]  │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Logs S3 actions
                            │ (GetObject, PutObject, DeleteObject, etc.)
                            ▼
┌────────────────────────────────────────────────────────┐
│                   AWS CloudTrail                       │
│                                                        │
│  1. Navigate to AWS CloudTrail Console                 │
│  2. Select 'Event history'                             │
│  3. Filter / Review S3 API activity logs               │
└────────────────────────────────────────────────────────┘

```

------------------xxxxxxxxxxxxxxxxxx---------------------



Here is the complete **AWS CloudTrail S3 Data Events Logging Lab (Page 43)** formatted in clean Markdown for your Visual Studio Code notes:

```markdown
# AWS Lab: Logging S3 Object-Level API Activity with CloudTrail (Page 43)

---

## 🎯 Lab Overview

### Objective
To configure **AWS CloudTrail** to log **Data Events** for an Amazon S3 bucket, capturing object-level operations such as `GetObject`, `PutObject`, and `DeleteObject`, and delivery of those logs to a central logging bucket for audit and compliance analysis.

### Purpose
By default, AWS CloudTrail only logs **Management Events** (e.g., creating or deleting an S3 bucket itself). It does **not** log object-level API actions performed inside the bucket due to high volume. Enabling **S3 Data Events** allows security and compliance teams to track exactly *who* uploaded, downloaded, or deleted specific files, *when* it occurred, and *from which IP address*.

---

## 🛠️ Step-by-Step Beginner-Friendly Lab Guide

### Step 1: Create Destination & Source S3 Buckets
1. Log in to the **AWS Management Console** and navigate to **S3**.
2. **Create Target Log Bucket:**
   * Click **Create bucket**.
   * **Bucket name:** `cloudtrail-logs-destination-43` *(Must be globally unique)*
   * Click **Create bucket**.
3. **Create Source Data Bucket:**
   * Click **Create bucket**.
   * **Bucket name:** `app-data-source-bucket-43`
   * Click **Create bucket**.

---

### Step 2: Create a CloudTrail Trail with Data Events
1. Open the **AWS CloudTrail Console** by searching for **CloudTrail** in the top search bar.
2. In the left menu, click **Trails**, then click **Create trail**.
3. **Step 1: Choose trail attributes**
   * **Trail name:** `S3-Object-Activity-Trail`
   * **Storage location:** Select **Create new S3 bucket** (or select **Use existing S3 bucket** and choose `cloudtrail-logs-destination-43`).
   * Click **Next**.
4. **Step 2: Choose log events**
   * Check **Management events** (Optional/Default).
   * Check **Data events**.
   * Under **Data events selection**:
     * **Data event source:** Select **S3**.
     * **Log selector template:** Choose **Custom** or **Log all events**.
     * Under **Individual bucket selection**, browse and select your source bucket: `app-data-source-bucket-43`.
     * **Event type:** Select both **Read** (`GetObject`) and **Write** (`PutObject`, `DeleteObject`).
   * Click **Next**.
5. **Step 3: Review and create**
   * Review all configurations and click **Create trail**.

---

### Step 3: Perform API Operations (Upload/Download/Delete)
1. Open the **S3 Console** and click on your source bucket: `app-data-source-bucket-43`.
2. **Upload Operation (`PutObject`):**
   * Click **Upload** $\rightarrow$ **Add files** $\rightarrow$ Upload a sample file (e.g., `audit_test.txt`).
3. **Download Operation (`GetObject`):**
   * Select `audit_test.txt` and click **Download**.
4. **Delete Operation (`DeleteObject`):**
   * Select `audit_test.txt`, click **Delete**, type `permanently delete`, and confirm.

---

### Step 4: Verify CloudTrail Log Delivery
1. Open the destination bucket: `cloudtrail-logs-destination-43`.
2. Navigate through the folder hierarchy:
   `AWSLogs/ <ACCOUNT_ID> / CloudTrail / <REGION> / <YEAR> / <MONTH> / <DAY> /`
3. Download and open one of the `.json.gz` log files.
4. **Expected Result:** The JSON log record contains detailed object-level entries showing:
   * **`eventName`**: `PutObject`, `GetObject`, or `DeleteObject`
   * **`resources`**: `arn:aws:s3:::app-data-source-bucket-43/audit_test.txt`
   * **`sourceIPAddress`**: The public IP address of the user who performed the action **✓**.

---

## 🏗️ Architecture Flow




```

┌─────────────────────────────────────────────────────────────┐
│ 1. User Action on S3 Object                                 │
│                                                             │
│    Performs PutObject, GetObject, or DeleteObject          │
│    on Source Bucket (app-data-source-bucket-43)             │
└─────────────────────────────┬───────────────────────────────┘
│
│ Triggers Object-Level API Event
▼
┌─────────────────────────────────────────────────────────────┐
│ 2. AWS CloudTrail (Data Events Logging Enabled)             │
│                                                             │
│    Captures JSON metadata:                                  │
│    - IAM Identity / User ARN                                │
│    - Action Type & Timestamp                                │
│    - Source IP Address                                      │
└─────────────────────────────┬───────────────────────────────┘
│
│ Delivers Log Files (.json.gz)
▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Destination Log Bucket (cloudtrail-logs-destination-43)  │
│                                                             │
│    Stores immutable audit trail files for compliance ✓       │
└─────────────────────────────────────────────────────────────┘

```

---

## 🔑 Key Takeaways

* **Management vs. Data Events:** Management events log bucket creation and policy changes; Data events log file-level activities (`PutObject`, `GetObject`, `DeleteObject`).
* **Cost & Volume:** Data events generate high volume and incur additional costs per 100,000 events logged. Always use advanced event selectors to filter for specific high-value S3 buckets.
* **Auditability & Compliance:** CloudTrail Data Events provide complete forensic evidence required for regulatory frameworks (such as PCI-DSS, HIPAA, and SOC 2).

---

## 🧹 Post-Lab Cleanup

To avoid continuous logging storage charges:

1. **Delete the CloudTrail Trail:**
   * Open **CloudTrail Console** $\rightarrow$ **Trails**.
   * Select `S3-Object-Activity-Trail` and click **Delete**.

2. **Empty & Delete S3 Buckets:**
   * Open **S3 Console**.
   * Empty and delete `app-data-source-bucket-43`.
   * Empty and delete `cloudtrail-logs-destination-43`.

```

[AWS S3 CloudTrail Logging Guide](https://www.youtube.com/watch?v=kcFoqZ8_G8w)

This video demonstrates how CloudTrail records S3 actions into JSON logs and walks through retrieving and analyzing those event files.