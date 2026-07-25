# Azure Day 14 – Create Managed Disk

## Task
Create a managed disk in Microsoft Azure with the specified requirements.

## Requirements

- Disk Name: `xfusion-disk`
- Disk Type: `Standard_LRS`
- Disk Size: `2 GiB`

## Configuration

- Subscription: Azure Free Labs
- Resource Group: `kml_rg_main-f7df47a334274fcc`
- Region: East US
- Availability Zone: 1
- Source Type: None
- Size: 2 GiB
- Storage Type: Standard HDD LRS
- Encryption: Platform-managed key
- Shared Disk: No

## Steps Performed

1. Opened the Azure Portal.
2. Navigated to **Disks**.
3. Clicked **Create**.
4. Selected the required subscription and resource group.
5. Set the disk name to `xfusion-disk`.
6. Selected the `East US` region.
7. Set the disk size to `2 GiB`.
8. Selected `Standard HDD LRS` as the storage type.
9. Left the source type as `None`.
10. Reviewed the configuration and created the disk.

## Result

The managed disk `xfusion-disk` was successfully created with a size of `2 GiB` and storage type `Standard_LRS`.

## Key Concept

Azure Managed Disks are block-level storage volumes managed by Azure and used with Azure Virtual Machines. Common disk types include:

- Standard HDD LRS
- Standard SSD LRS
- Premium SSD LRS
- Ultra Disk

`Standard_LRS` provides locally redundant, cost-effective storage suitable for workloads that do not require high performance.