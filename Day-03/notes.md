# Day 03 - Create an Azure Virtual Machine using Azure CLI

## Objective
Create an Azure Virtual Machine using the Azure CLI.

## Services Used
- Azure Virtual Machines
- Azure CLI
- Azure Managed Disks

## Configuration

- Resource Group: KML_RG_MAIN-2C31C2C8686844AC
- VM Name: datacenter-vm
- Image: Ubuntu2204
- VM Size: Standard_B2s
- Admin Username: azureuser
- Authentication: SSH Keys
- Storage SKU: Standard_LRS
- OS Disk Size: 30 GB
- Region: East US

## Commands Used

```bash
az group list -o table

az vm create \
  --resource-group kml_rg_main-2c31c2c8686844ac \
  --name datacenter-vm \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30

az vm list -d -o table
```

## Outcome

Successfully created an Azure Virtual Machine named **datacenter-vm** using the Azure CLI and verified that it is in the **Running** state.

## Key Learnings

- Azure CLI enables complete VM deployment without using the Azure Portal.
- SSH key authentication is more secure than password authentication for Linux VMs.
- Standard_LRS provides cost-effective locally redundant storage.
- Azure automatically provisions the required networking resources during VM creation.

## Outcome

✅ Lab Completed