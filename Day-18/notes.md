# Azure 100 Days of Cloud – Day 18 Notes

## Objective

The objective of today's lab was to upload a local file to an existing Azure Blob Storage container using the Azure CLI. This simulates a real-world scenario where organizations migrate files from on-premises storage systems to Azure Blob Storage.

---

## Services Used

* Azure Storage Account
* Azure Blob Storage
* Azure CLI

---

## Resources Used

| Resource        | Name              |
| --------------- | ----------------- |
| Storage Account | devopsst16984     |
| Blob Container  | devops-blob-24017 |
| Uploaded File   | /tmp/devops.txt   |
| Blob Name       | devops.txt        |
| Region          | East US           |

---

## What is Azure Blob Storage?

Azure Blob Storage is Microsoft's object storage service designed to store large amounts of unstructured data such as:

* Documents
* Images
* Videos
* Log files
* Backups
* Virtual machine disks

Blob Storage is commonly used for cloud applications, backups, disaster recovery, media hosting, and data migration.

---

## Blob Container

A Blob Container is similar to a folder. It is used to organize blobs (files) inside a storage account.

Structure:

Storage Account
→ Blob Container
→ Blob (File)

---

## Steps Performed

### Step 1 – Retrieved Azure Credentials

Used:

```bash
showcreds
```

Retrieved:

* Azure Portal URL
* Username
* Password

---

### Step 2 – Logged in to Azure

Used:

```bash
az login
```

Completed the device authentication process using the provided credentials.

Verified login:

```bash
az account show --output table
```

---

### Step 3 – Verified the Local File

Checked that the file existed before uploading.

Command:

```bash
ls -l /tmp/devops.txt
```

---

### Step 4 – Uploaded the File

Used the Azure CLI upload command:

```bash
az storage blob upload \
  --account-name devopsst16984 \
  --container-name devops-blob-24017 \
  --name devops.txt \
  --file /tmp/devops.txt \
  --auth-mode login
```

The upload completed successfully.

---

### Step 5 – Verified the Upload

Listed the blobs inside the container.

Command:

```bash
az storage blob list \
  --account-name devopsst16984 \
  --container-name devops-blob-24017 \
  --auth-mode login \
  --output table
```

Output confirmed that **devops.txt** was successfully uploaded.

---

## Azure CLI Commands Used

```bash
showcreds

az login

az account show --output table

ls -l /tmp/devops.txt

az storage blob upload \
  --account-name devopsst16984 \
  --container-name devops-blob-24017 \
  --name devops.txt \
  --file /tmp/devops.txt \
  --auth-mode login

az storage blob list \
  --account-name devopsst16984 \
  --container-name devops-blob-24017 \
  --auth-mode login \
  --output table
```

---

## Key Learnings

* Learned how Azure Blob Storage stores unstructured data.
* Learned how Blob Containers organize blobs.
* Used Azure CLI for authentication.
* Uploaded files to Azure Blob Storage using Azure CLI.
* Verified uploaded blobs using Azure CLI.
* Understood a basic cloud data migration workflow.

---

## Real-World Use Cases

* Migrating files from on-premises storage to Azure.
* Application file storage.
* Backup and disaster recovery.
* Media and document storage.
* Log and analytics data storage.
* Static website content hosting.

---

## Outcome

Successfully uploaded the local file **/tmp/devops.txt** to the existing Blob container **devops-blob-24017** in the storage account **devopsst16984** using the Azure CLI and verified the upload.
