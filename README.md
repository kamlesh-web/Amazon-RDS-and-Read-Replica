# How to create an Amazon RDS and Read Replica

**Here's a detailed, step-by-step explanation of the entire process** to create an Amazon RDS MariaDB instance and then add a Read Replica.
<img width="1207" height="679" alt="screenshot_20260413142442" src="https://github.com/user-attachments/assets/9a7ee432-ef29-45b6-80b5-6d6a11a3c7a4" />

### Step 1 
– Click on the search box at the top of the AWS Management Console and type **"database"**.  
This opens the service search results. AWS shows popular database-related services (RDS, Aurora, Database Migration Service, etc.).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/19258e8d-c7fb-428b-9b46-07e06f1b2f8b" />

### Step 2 
– Click **"Show more"** under the Services section.  
This expands the full list so you can see every database service.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/1f5eff44-2f8f-4442-99bf-354cacfc9ce4" />

### Step 3 
– In the expanded list, click **"Aurora and RDS"**.  
This takes you directly to the Amazon RDS console (the page where you create and manage all RDS databases).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/bcf1ea37-fa87-47a1-8e86-a42d0b37dd80" />

### Step 4 
– On the RDS "Create database" page, choose your database engine.  
The guide selected **MariaDB** (a popular open-source MySQL-compatible engine). You can choose any engine, but MariaDB was used here.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/9ae84ef0-976a-4c6d-9326-6642b3e48159" />

### Step 5 
– Select **"Full configuration"** (instead of Easy create).  
"Easy create" uses pre-set defaults with very few options. Full configuration gives you full control over instance size, storage, networking, backups, encryption, etc.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/f1ea26df-522a-4e78-a894-a3b902955a0a" />

### Step 6 
– Choose the **Engine type** and **Engine version**.  
- Engine: MariaDB  
- Version: The guide used **MariaDB 11.4.5**.  
You can select any supported version from the dropdown.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/bb9a91f9-06f0-4b54-94af-2c98356a6798" />

### Step 7 
– Scroll down and choose the engine version. We went with "MariaDB 11.4.5".

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/0641667a-d1aa-4ffc-9fc7-0e5bca9573e7" />

### Step 8 
– Give your database a name in the **DB instance identifier** field.  
Default is something like "database-1". The guide changed it to **"my-database"** for clarity and easier identification later.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/1f4d026b-3580-415d-94c8-a86e6bff2b74" />

### Step 9 
– In **Credentials Settings**:  
- Leave **Master username** as the default (**admin**) or change it.  
- Under **Credentials management**, choose **Self managed** (so you create and know the password yourself).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/e2a95eba-08d2-4ee1-b957-ebe3dd917ba9" />

### Step 10 
– Set a strong **Master password**.  
- Type the password.  
- Confirm it in the next field.  
- AWS shows a password strength meter, make sure it is strong (mix of letters, numbers, symbols).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/81cc70f0-b0e5-4119-b5de-2f843b4d72fc" />

### Step 11 
– **Instance configuration** section:  
- Choose **Burstable classes** (this was the only free-tier eligible option).  
- Select the instance type (e.g., db.t3.micro or similar small instance).  
- Scroll down to the **Storage** section.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/905fa2c1-47e1-41ba-a20e-75d80f5d0296" />

### Step 12 
– Choose your **Storage type**.  
In this guide we selected **General Purpose SSD (gp3)** — a good balance of performance and cost for most workloads.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/55b59f87-8994-4b5d-a979-424410acd343" />

### Step 13 
– Set **Allocated storage**.  
The guide set it to **20 GB** (you can increase or decrease based on your needs). Minimum is usually 20 GB for MariaDB.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/3f44e9bb-6422-4e0a-90c2-d4d7a418cdb8" />

### Step 14 
– **Additional Storage Configuration** (very important):  
- Check **Enable storage autoscaling**.  
- Set **Maximum storage threshold** (the guide used **1000 GB**).  
This allows RDS to automatically grow your storage up to 1000 GB if your database needs more space.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/e24d1e11-0cef-4eb1-9894-d016b41b71a5" />

### Step 15 
– **Availability & durability**:  
In a free-tier account these options are greyed out.  
In a paid account you could enable a Multi-AZ standby instance (automatic failover for high availability).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/e00e87fe-cf88-4b96-b4d2-af87055c1463" />

### Step 16 
– **Connectivity** section:  
- Under **Compute resource** → choose **Don't connect to an EC2 compute resource** (standalone database).  
- **Virtual Private Cloud (VPC)** and **Subnet group** → leave as default.  
- **Database subnet group** → default is fine.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/bd3d2e0a-857e-44be-8a90-605206b2203d" />

### Step 17 
– **Public access**:  
- Select **No** (recommended for security — your database stays private inside the VPC).  
- **VPC security group** → choose the existing default security group (or create a new one).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/0f7e6fe6-869c-49bf-bc84-537047d5b59c" />

### Step 18 
– Expand **Additional configuration**:  
- In **Initial database name**, type **my-database** (or any name you want).  
This creates an actual database inside the RDS instance when it launches.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/2af46524-2370-4ad0-82c5-0bd776e403b2" />

### Step 19 
– **Backup** section:  
- Check **Enable automated backups**.  
- Set **Backup retention period** to **7 days** (or whatever you prefer). Our free-tier account is limited to **1 day**.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/e738266d-f616-40da-8797-8dd58fb26576" />

### Step 20 
– Scroll down and check **Enable encryption** (uses AWS KMS default key).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/bacbb69a-dbc3-4a6b-ba5e-d394315ccd4a" />

### Step 21 
– At the very bottom, click the orange button **Create database**.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/8906f095-84dc-432f-b8e8-272015df0ada" />

### Step 22 
– Click **Refresh** periodically on the Databases list until the status changes from **Creating** to **Available**.
<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/bd372e62-6df2-408c-afaa-533abc71570f" />

---


## Part 2: Creating a Read Replica

### Step 23 
– What is a Read Replica?  
Read replicas are read-only copies of a primary database, primarily used to enhance performance by offloading read traffic from the main database. They enable horizontal scaling of read-heavy workloads, decrease read latency by serving data from closer geographical locations, and can be promoted to standalone, writable databases if needed

Benefits:  
- Offloads read traffic from the primary (improves performance).  
- Horizontal scaling for read-heavy apps.  
- Lower latency if placed in a different region/AZ.  
- Can be promoted to a full writable database later if needed.

### Step 24 
– Once your primary database shows **Available**, you can create a read replica for read-heavy workloads.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/d613bd3e-a243-407c-bf9f-ef4dbc17f7f2" />

### Step 25 
– Click the **text link** of your primary database (**my-database**).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/8e72aff5-3f69-48f6-89d7-7b959d1c237f" />

### Step 26 
– On the database details page, click the **Actions** button (top right).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/e69c417f-8243-43d6-a785-8a17c71e7d75" />

### Step 27 
– From the dropdown menu, choose **Create read replica**.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/f0f1bf42-6d14-43dd-81d2-0cacbb717c01" />

### Step 28 
– On the "Create read replica" page:  
- **Replica source** is automatically set to your primary (my-database).  
- **DB instance identifier** → enter **my-database-replica** (or any name you like).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/57d02872-702e-4b97-af29-04b046f297c9" />

### Step 29 
– **Additional storage configuration**:  
- Make sure **Enable storage autoscaling** is checked (same as primary).  
- You can set a maximum storage threshold here too.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/581e16cf-8fdf-4792-b806-f717977354dd" />

### Step 30 
– Scroll to **DB subnet group** → leave as default.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/c4e9bc3e-5b01-4f34-8ba6-53c9e9702203" />

### Step 31 
– **Public access** → keep **No** (same security rule as primary).

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/3f6bb049-f0f5-42f7-a1a1-1baa02c865be" />

### Step 32 
– **Additional monitoring settings**:  
- Uncheck **Enable Enhanced Monitoring** (this saves cost in a demo/free-tier environment).
  
<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/cb903f5e-c9b7-4e5b-9cda-9131d4378930" />

### Step 33 
– Scroll to the bottom and click the orange **Create replica** button.

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/062d78d5-205d-43bd-8e78-ad3798dd716e" />

### Step 34 
– Wait a few minutes and refresh the Databases list.  
You will now see **two** databases:  
- **my-database** → Role: Primary  
- **my-database-replica** → Role: Replica  

<img width="1362" height="765" alt="image" src="https://github.com/user-attachments/assets/165a75a3-e34f-46f8-ae7c-f609bb02de31" />

Both should show **Available**.

We have now successfully created a fully functional Amazon RDS MariaDB instance with a Read Replica!

