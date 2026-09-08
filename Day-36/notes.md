# Azure Day 36 — Blob Lifecycle Management

## Objective

Configure Azure Blob Lifecycle Management to automatically delete old blobs after 7 days of last modification.

## Resources Created

* Resource Group: `kml_rg_main-64de015eed6f47e5`
* Storage Account: `xfusionstor16231`
* Region: `East US`
* Performance: `Standard`
* Redundancy: `LRS`
* Storage Kind: `StorageV2`
* Container: `xfusion-container16231`
* Blob: `tempfile.txt`

## Storage Account Configuration

Created the storage account using Azure CLI:

```bash
az storage account create \
  --name xfusionstor16231 \
  --resource-group kml_rg_main-64de015eed6f47e5 \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2
```

Verified:

* Provisioning state: `Succeeded`
* Location: `eastus`
* SKU: `Standard_LRS`
* Kind: `StorageV2`

## Blob Container

Created:

```text
xfusion-container16231
```

## File Upload

Uploaded:

```text
/root/tempfile.txt
```

to the container as:

```text
tempfile.txt
```

Verified blob size:

```text
25 bytes
```

## Lifecycle Management Rule

Created the lifecycle management rule:

```text
Rule Name: xfusion-del-rule
Status: Enabled
Blob Type: blockBlob
Container Prefix: xfusion-container16231/
Delete After: 7 days after last modification
```

## Verification

The final Azure CLI verification returned:

```json
[
  {
    "BlobTypes": [
      "blockBlob"
    ],
    "DeleteAfterDays": 7.0,
    "Enabled": true,
    "Name": "xfusion-del-rule",
    "Prefix": [
      "xfusion-container16231/"
    ]
  }
]
```

This confirms that the lifecycle rule is correctly configured and scoped to the required container.

## Result

Azure Day 36 — Blob Lifecycle Management completed successfully and verified end-to-end.
