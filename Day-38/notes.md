# Day 38 — Azure VM Blob Storage Integration

## Objective

Configure an Azure Blob Storage account and private container, then use an existing Azure VM to create and upload a test file to Blob Storage.

## Resources

* VM: `devops-vm`
* VM Region: `East US`
* Resource Group: `KML_RG_MAIN-6B5F06B697FF42AC`
* Storage Account: `devopsstor91160621`
* Storage Region: `East US`
* Storage SKU: `Standard_LRS`
* Container: `devops-container91160621`

## Storage Account Configuration

Created the storage account using Azure CLI:

```bash
az storage account create \
  --name devopsstor91160621 \
  --resource-group KML_RG_MAIN-6B5F06B697FF42AC \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2 \
  --allow-blob-public-access false
```

Verified:

* Location: `eastus`
* SKU: `Standard_LRS`
* Kind: `StorageV2`
* Public Blob Access: `False`
* Provisioning State: `Succeeded`

## Blob Container

Created the private container:

```bash
az storage container create \
  --name devops-container91160621 \
  --account-name devopsstor91160621 \
  --auth-mode login \
  --public-access off
```

Container:

`devops-container91160621`

Public access was disabled.

## Storage Account Key

Retrieved the storage account access key using:

```bash
export STORAGE_KEY=$(az storage account keys list \
  --account-name devopsstor91160621 \
  --resource-group KML_RG_MAIN-6B5F06B697FF42AC \
  --query "[0].value" \
  --output tsv)
```

The key was kept private and was not displayed.

## Test File

SSH'd into `devops-vm` and created:

```text
/home/azureuser/testfile.txt
```

Command:

```bash
echo "this is a test file" > /home/azureuser/testfile.txt
```

Verified file content:

```text
this is a test file
```

File size:

`20 bytes`

## Blob Upload

Uploaded the file to the private Blob container using Azure CLI.

The upload completed successfully with:

```text
Finished [100.0000%]
```

The Blob Storage service also confirmed server-side encryption for the uploaded object.

## Upload Verification

Verified the uploaded blob with:

```bash
az storage blob show \
  --account-name devopsstor91160621 \
  --account-key "$STORAGE_KEY" \
  --container-name devops-container91160621 \
  --name testfile.txt \
  --query "{Name:name,Size:properties.contentLength}" \
  --output table
```

Result:

```text
Name          Size
------------  ----
testfile.txt  20
```

## Final Result

Azure VM successfully interacted with Azure Blob Storage.

The test file was created on `devops-vm`, uploaded to the private Blob container, and verified successfully.

## Key Concepts Learned

* Azure Storage Accounts
* Azure Blob Storage
* Storage redundancy with LRS
* Private Blob containers
* Storage account access keys
* Azure CLI Blob operations
* VM-to-Blob Storage interaction
* Blob upload verification
* Server-side encryption
* Secure handling of storage credentials

**Day 38: Completed and end-to-end verified.**
