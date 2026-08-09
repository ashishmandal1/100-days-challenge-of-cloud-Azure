# Day 23 – Azure Virtual Machine with Nginx using Azure CLI

## Objective

The objective of this task was to create an Azure Virtual Machine using Azure CLI with an Ubuntu image, configure it to automatically install and start the Nginx web server using Cloud-Init (custom data), and ensure that HTTP traffic (port 80) is accessible from the internet through an Azure Network Security Group.

---

# What is Azure CLI?

Azure CLI is a command-line tool provided by Microsoft that allows users to create, manage, and configure Azure resources directly from a terminal or command-line environment.

It can be used to manage resources such as Virtual Machines, Networks, Storage Accounts, Resource Groups, and Network Security Groups.

---

# What is an Azure Virtual Machine?

An Azure Virtual Machine (VM) is an Infrastructure as a Service (IaaS) offering that allows users to deploy and manage virtual servers in the Microsoft Azure cloud.

Azure VMs support operating systems such as Windows and Linux and can be used for hosting web applications, databases, development environments, and enterprise workloads.

---

# What is Cloud-Init?

Cloud-Init is a standard method used to automatically configure Linux virtual machines during their first boot.

It can install software packages, configure services, create users, and execute commands automatically without requiring manual configuration after the VM is created.

---

# What is Nginx?

Nginx is a high-performance open-source web server commonly used for serving websites, acting as a reverse proxy, load balancing, and caching.

In this task, Nginx was configured as the web server running on the Azure VM.

---

# Services Used

* Microsoft Azure Virtual Machines
* Azure CLI
* Azure Virtual Network (VNet)
* Azure Network Security Group (NSG)
* Public IP Address
* Cloud-Init (Custom Data)
* Ubuntu Linux
* Nginx

---

# Task Performed

* Used Azure CLI to verify the Azure subscription.
* Used the existing KodeKloud resource group in the **East US** region.
* Created an Azure Network Security Group named **nautilus-nsg**.
* Created an inbound NSG rule allowing HTTP traffic on **TCP port 80**.
* Created an Ubuntu Azure Virtual Machine named **nautilus-vm**.
* Used Cloud-Init to automatically install Nginx.
* Configured Cloud-Init to enable and start the Nginx service.
* Assigned a Public IP address to the VM.
* Verified that Nginx was running.
* Verified that the web server was accessible from the internet.

---

# Cloud-Init Script Used

```yaml
#cloud-config
package_update: true
packages:
  - nginx

runcmd:
  - systemctl enable nginx
  - systemctl start nginx
```

The script was saved as:

```text
cloud-init.txt
```

---

# Azure Resources Used

| Resource               | Purpose                        |
| ---------------------- | ------------------------------ |
| Virtual Machine        | Hosts the Nginx web server     |
| Virtual Network        | Provides network connectivity  |
| Subnet                 | Provides network segmentation  |
| Public IP              | Allows internet access         |
| Network Security Group | Controls network traffic       |
| NSG Security Rule      | Allows HTTP traffic on port 80 |
| Cloud-Init             | Automates VM configuration     |

---

# Configuration Used

| Setting        | Value          |
| -------------- | -------------- |
| VM Name        | `nautilus-vm`  |
| Region         | East US        |
| Image          | Ubuntu 22.04   |
| VM Size        | Standard_B1s   |
| OS Disk        | Standard_LRS   |
| Authentication | SSH Public Key |
| Username       | `azureuser`    |
| NSG            | `nautilus-nsg` |
| HTTP Port      | TCP 80         |
| Web Server     | Nginx          |
| Public IP      | `20.25.77.165` |

---

# Network Security Group Configuration

An NSG named **nautilus-nsg** was created to control inbound network traffic.

An inbound rule named **Allow-HTTP** was configured with the following settings:

| Setting          | Value      |
| ---------------- | ---------- |
| Rule Name        | Allow-HTTP |
| Priority         | 100        |
| Direction        | Inbound    |
| Access           | Allow      |
| Protocol         | TCP        |
| Source           | Internet   |
| Destination Port | 80         |

This allows users from the internet to access the Nginx web server through HTTP.

---

# Azure CLI Commands Used

### Verify Azure Account

```bash
az account show
```

---

### List Resource Groups

```bash
az group list --output table
```

The KodeKloud lab provided the following resource group:

```text
kml_rg_main-fedc6484eb7c4881
```

---

### Create Network Security Group

```bash
az network nsg create \
  --resource-group kml_rg_main-fedc6484eb7c4881 \
  --name nautilus-nsg \
  --location eastus
```

---

### Allow HTTP Port 80

```bash
az network nsg rule create \
  --resource-group kml_rg_main-fedc6484eb7c4881 \
  --nsg-name nautilus-nsg \
  --name Allow-HTTP \
  --priority 100 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --source-address-prefixes Internet \
  --source-port-ranges '*' \
  --destination-address-prefixes '*' \
  --destination-port-ranges 80
```

---

### Create the Azure VM

```bash
az vm create \
  --resource-group kml_rg_main-fedc6484eb7c4881 \
  --name nautilus-vm \
  --location eastus \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --storage-sku Standard_LRS \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-sku Standard \
  --nsg nautilus-nsg \
  --custom-data cloud-init.txt
```

The `--storage-sku Standard_LRS` option was used because the lab environment did not allow Premium OS disks.

---

# Verification Steps

## Verify VM

The VM was successfully created and was in the running state.

```text
VM Name: nautilus-vm
Power State: VM running
Region: East US
Public IP: 20.25.77.165
```

---

## Verify Nginx Service

The Nginx service was checked using Azure VM Run Command:

```bash
az vm run-command invoke \
  --resource-group kml_rg_main-fedc6484eb7c4881 \
  --name nautilus-vm \
  --command-id RunShellScript \
  --scripts "systemctl is-active nginx"
```

Output:

```text
active
```

The `active` status confirms that Nginx is running successfully.

---

## Verify HTTP Access

The web server was tested using:

```bash
curl -I http://20.25.77.165
```

Output:

```text
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Content-Type: text/html
```

The `HTTP/1.1 200 OK` response confirms that the Nginx web server is accessible from the internet.

---

# Common Issues

## Authorization Failed While Creating Resource Group

**Error**

```text
AuthorizationFailed
```

**Cause**

The KodeKloud lab service principal did not have permission to create a new resource group.

**Solution**

Used the existing resource group provided by the lab:

```text
kml_rg_main-fedc6484eb7c4881
```

---

## Premium SSD Policy Error

**Error**

```text
RequestDisallowedByPolicy
```

**Cause**

The lab environment did not allow Premium OS disks.

The VM initially attempted to use:

```text
Premium_LRS
```

which was rejected by the Azure Policy.

**Solution**

The failed VM was removed and recreated using:

```bash
--storage-sku Standard_LRS
```

This successfully satisfied the lab policy.

---

## VM Deployment Failed

The first VM deployment reached:

```text
provisioningState: Failed
```

because the OS disk was configured with `Premium_LRS`.

The failed VM resource was removed using Azure CLI and recreated with the allowed Standard disk configuration.

---

## HTTP Not Accessible

If the Nginx server cannot be accessed from the internet, check:

* VM has a Public IP.
* NSG is attached to the VM/network interface.
* TCP port **80** is allowed.
* Nginx is installed.
* Nginx service is running.
* No additional network rule is blocking port 80.

---

# Best Practices

* Use Azure CLI to automate infrastructure deployment.
* Use Cloud-Init for automatic Linux VM configuration.
* Use SSH keys instead of password authentication.
* Open only the required ports in the NSG.
* Use Standard disk SKUs when required by the environment's policies.
* Verify services after deployment.
* Test public connectivity using tools such as `curl`.
* Keep infrastructure configuration documented in GitHub.
* Never commit private SSH keys or other secrets to GitHub.

---

# Key Concepts Learned

* Azure CLI VM deployment.
* Azure Virtual Machine provisioning.
* Ubuntu VM configuration.
* Cloud-Init and custom data.
* Automated Nginx installation.
* Linux service management using `systemctl`.
* Azure Network Security Groups.
* NSG inbound security rules.
* HTTP/TCP port 80.
* Public IP configuration.
* Azure VM disk SKUs.
* Azure Policy restrictions.
* VM Run Command.
* Testing internet connectivity using `curl`.

---

# Outcome

Successfully created an Azure Ubuntu Virtual Machine named **nautilus-vm** in the **East US** region using Azure CLI.

The VM was configured with Cloud-Init to automatically install and start the Nginx web server. An NSG named **nautilus-nsg** was configured to allow HTTP traffic on TCP port 80 from the internet.

The deployment was successfully verified by confirming that the Nginx service was **active** and that the public IP returned an **HTTP 200 OK** response.

```text
VM:        nautilus-vm
Region:    East US
OS:        Ubuntu 22.04
Web Server: Nginx
NSG:       nautilus-nsg
Port:      TCP 80
Status:    Running
HTTP:      200 OK
```

## Challenge

**100 Days of Azure – KodeKloud**

**Day:** 23

**Topic:** Azure VM Deployment using Azure CLI + Nginx + Cloud-Init + NSG

---

## Author

**Ashish Mandal**

Learning Azure, Cloud & DevOps through the **100 Days of Azure Challenge**.
