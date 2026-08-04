# Day 22 – Azure Virtual Machine with Nginx (Cloud-Init)

## Objective

The objective of this task was to create an Azure Virtual Machine using an Ubuntu image, configure it to automatically install and start the Nginx web server during deployment using Cloud-Init (custom data), and ensure that HTTP traffic (port 80) is allowed from the internet.

---

# What is an Azure Virtual Machine?

An Azure Virtual Machine (VM) is an Infrastructure as a Service (IaaS) offering that allows users to deploy and manage virtual servers in the Microsoft Azure cloud. Azure VMs support various operating systems such as Windows and Linux and can be used for hosting web applications, databases, development environments, and enterprise workloads.

---

# What is Cloud-Init?

Cloud-Init is a standard method used to automatically configure Linux virtual machines during their first boot. It executes initialization scripts, installs software packages, creates users, configures networking, and performs other setup tasks without requiring manual intervention.

---

# What is Nginx?

Nginx is a high-performance open-source web server that is commonly used for serving websites, acting as a reverse proxy, load balancing, and caching.

---

# Services Used

- Microsoft Azure Virtual Machines
- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Public IP Address
- Cloud-Init (Custom Data)
- Ubuntu Linux
- Nginx

---

# Task Performed

- Created an Azure Virtual Machine named **nautilus-vm**.
- Selected an Ubuntu image.
- Used **Cloud-Init** to automatically install and start Nginx.
- Configured the VM to allow HTTP (Port 80) traffic.
- Assigned a Public IP address.
- Verified that the Nginx web server was running.

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

---

# Azure Resources Created

| Resource | Purpose |
|----------|---------|
| Virtual Machine | Hosts the web server |
| Virtual Network | Provides network connectivity |
| Subnet | Network segment for the VM |
| Public IP | Allows internet access |
| Network Security Group | Controls inbound and outbound traffic |
| Cloud-Init | Automates VM configuration |

---

# Configuration Used

| Setting | Value |
|---------|-------|
| VM Name | nautilus-vm |
| Region | East US |
| Image | Ubuntu Server (Any Ubuntu Image) |
| Authentication | SSH Public Key |
| Username | azureuser |
| Public Inbound Ports | SSH (22), HTTP (80) |
| Web Server | Nginx |

---

# Verification Steps

### Verify VM

- Open Azure Portal.
- Navigate to **Virtual Machines**.
- Confirm the VM status is **Running**.

---

### Verify HTTP Rule

- Open the VM.
- Go to **Networking**.
- Confirm that an inbound rule exists allowing **HTTP (Port 80)**.

---

### Verify Nginx

Open the VM's Public IP address in a browser:

```
http://<Public-IP>
```

The default **Welcome to nginx!** page confirms that Nginx is running successfully.

---

# Key Concepts Learned

- Azure Virtual Machine deployment.
- Ubuntu VM provisioning.
- Cloud-Init for automated server configuration.
- Automatic package installation during VM creation.
- Azure Network Security Groups (NSGs).
- Public IP configuration.
- Hosting a web server on Azure.

---

# Common Issues

## Premium SSD Policy Error

**Error**

```
RequestDisallowedByPolicy
```

**Cause**

The lab policy does not allow **Premium SSD** OS disks.

**Solution**

Change the OS disk type from:

```
Premium SSD LRS
```

to:

```
Standard SSD LRS
```

or

```
Standard HDD LRS
```

---

## VM Size Not Available

**Error**

```
SkuNotAvailable
```

**Solution**

Select another available VM size such as:

- Standard B1s
- Standard B2s
- Standard B1ms

Do not change the region from **East US**.

---

## HTTP Not Accessible

Ensure:

- The VM has a Public IP.
- Port **80** is allowed in the Network Security Group.
- Nginx is installed and running.

---

# Best Practices

- Use Cloud-Init to automate server provisioning.
- Use Standard SSD disks in restricted lab environments.
- Open only the required ports in the NSG.
- Keep the OS updated during deployment.
- Use SSH keys instead of passwords for authentication.

---

# Outcome

Successfully created an Azure Ubuntu Virtual Machine named **nautilus-vm**, configured it with Cloud-Init to automatically install and start the Nginx web server, allowed HTTP traffic through the Network Security Group, and verified that the web server was accessible over the internet.