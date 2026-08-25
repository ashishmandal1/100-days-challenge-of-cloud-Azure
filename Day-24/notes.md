📝 Day 24 Notes — Azure VM with SSH Key Authentication
Objective

Create an Azure Virtual Machine named nautilus-vm in the westus region and configure secure, passwordless SSH access from the azure-client host using an SSH key.

Resources Created
Resource	Configuration
Resource Group	kml_rg_main-2edaf3caa2bb4ef9
VM Name	nautilus-vm
Region	westus
Image	Ubuntu 22.04
VM Size	Standard_B1s
Admin User	azureuser
Authentication	SSH Key
SSH Private Key	~/.ssh/id_rsa
Public Key	~/.ssh/id_rsa.pub
OS Disk	30 GB
Disk SKU	Standard_LRS
Public IP	20.253.147.115
Private IP	10.0.0.4
Steps Performed
1. Checked for an existing SSH key
ls -la ~/.ssh
test -f ~/.ssh/id_rsa.pub && echo "SSH key exists" || echo "SSH key does not exist"

No SSH key existed, so a new one was generated.

2. Generated RSA SSH key
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""

Generated:

~/.ssh/id_rsa
~/.ssh/id_rsa.pub
3. Checked Azure subscription and resource group
az account show \
  --query '[name,id,user.name]' \
  --output table

The lab-provided resource group was:

kml_rg_main-2edaf3caa2bb4ef9
4. Created the VM

The first deployment failed because Azure Policy rejected the default Premium OS disk.

The VM was then recreated using:

--storage-sku Standard_LRS
--os-disk-size-gb 30

Final command:

az vm create \
  --resource-group kml_rg_main-2edaf3caa2bb4ef9 \
  --name nautilus-vm \
  --location westus \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username azureuser \
  --ssh-key-values ~/.ssh/id_rsa.pub \
  --os-disk-size-gb 30 \
  --storage-sku Standard_LRS \
  --public-ip-sku Standard
5. Verified VM deployment

The VM successfully returned:

location:        westus
powerState:      VM running
privateIpAddress: 10.0.0.4
publicIpAddress: 20.253.147.115
6. Tested passwordless SSH
ssh -i ~/.ssh/id_rsa azureuser@20.253.147.115

Successfully connected using the SSH key without a password.

Key Learning
Generated an RSA SSH key pair using ssh-keygen.
Used an SSH public key during Azure VM creation.
Learned how Azure CLI configures SSH authentication.
Used Standard_LRS to comply with the lab's Azure Policy.
Verified passwordless SSH connectivity to an Azure VM.
Learned that the resource group location does not have to match the VM's region; the VM itself was correctly deployed in westus.