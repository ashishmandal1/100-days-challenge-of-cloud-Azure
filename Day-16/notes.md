# Azure Day 16 Notes
## Topic: Azure Storage Account & Blob Container

## What is Azure Storage?

Azure Storage is Microsoft's cloud storage service used to store different types of data securely, durably, and at massive scale.

Azure Storage can store:

- Files
- Images
- Videos
- Documents
- Virtual Machine Disks
- Application Data
- Backups
- Logs

---

# Storage Account

A Storage Account is the top-level resource that provides access to Azure Storage services.

It acts as a container for all storage services.

Example:

Storage Account
│
├── Blob Storage
├── File Shares
├── Queues
├── Tables

---

# Blob Storage

Blob stands for Binary Large Object.

Blob Storage is used for storing:

- Images
- Videos
- Documents
- Backups
- ISO Files
- Log Files
- Static Website Files

Blob Storage is one of the most commonly used Azure storage services.

---

# Blob Container

A Blob Container is similar to a folder.

It organizes blobs (files) inside a storage account.

Example:

Storage Account
└── Container
    ├── photo.jpg
    ├── backup.zip
    ├── notes.pdf

---

# Steps Performed

1. Logged into Azure Portal.
2. Opened Storage Accounts.
3. Clicked Create.
4. Selected Subscription.
5. Selected Resource Group.
6. Entered Storage Account Name.
7. Selected Region.
8. Selected Performance.
9. Selected Redundancy option.
10. Reviewed configuration.
11. Created the Storage Account.
12. Opened the Storage Account.
13. Navigated to Data Storage → Containers.
14. Clicked + Container.
15. Entered the Container Name.
16. Created the Blob Container.
17. Verified successful creation.

---

# Important Storage Account Settings

## Performance

### Standard

- HDD-based
- Lower cost
- Suitable for most workloads

### Premium

- SSD-based
- Higher performance
- Lower latency

---

## Redundancy Options

### LRS (Locally Redundant Storage)

- Stores 3 copies
- Same datacenter
- Lowest cost

---

### ZRS (Zone-Redundant Storage)

- Stores copies across multiple Availability Zones.
- Protects against zone failures.

---

### GRS (Geo-Redundant Storage)

- Replicates data to another Azure region.
- Better disaster recovery.

---

### RA-GRS

- Same as GRS
- Read access available from secondary region.

---

# Storage Services

Azure Storage provides:

1. Blob Storage
2. File Storage
3. Queue Storage
4. Table Storage

---

## Blob Access Levels

Private
- Owner only

Blob
- Public read access for blobs only

Container
- Public read access for container and blobs

---

# Uses of Blob Storage

- Website images
- Application uploads
- Backups
- Logs
- Videos
- Media files
- Big data
- Static website hosting

---

# Advantages

- Highly Durable
- Highly Available
- Secure
- Scalable
- Cost Effective
- Globally Accessible

---

# Real-Life Example

Imagine Google Drive.

Storage Account = Google Drive Account

Container = Folder

Blob = File

Example:

Storage Account
└── Photos
      ├── image1.jpg
      ├── image2.jpg
      └── holiday.png

---

# Commands (Azure CLI)

Create Storage Account

az storage account create

List Storage Accounts

az storage account list

Create Blob Container

az storage container create

List Containers

az storage container list

---

# Key Learning

✔ Azure Storage Account is the parent resource.

✔ Blob Storage stores unstructured data.

✔ Containers organize blobs.

✔ Blob Storage is ideal for storing files in the cloud.

✔ Storage Accounts support multiple redundancy options for high availability.

✔ Azure Storage is one of the core Azure services used by almost every cloud application.