# Day 02 - Create an Azure Virtual Machine

## Lab Objective

Create an Azure Virtual Machine with the specified configuration and verify SSH connectivity.

---

## VM Configuration

| Property | Value |
|----------|-------|
| Virtual Machine Name | devops-vm |
| Resource Group | Existing Resource Group |
| Region | West US |
| Image | Ubuntu Server 24.04 LTS |
| Size | Standard_B1s |
| Authentication | Password |
| Network Security Group | Default NSG with SSH (Port 22) |
| OS Disk | 30 GB Standard HDD |
| Public IP | Automatically Assigned |

---

## Steps Performed

1. Logged in to the Azure Portal.
2. Selected the existing Resource Group.
3. Created a new Virtual Machine named **devops-vm**.
4. Selected **West US** as the deployment region.
5. Chose **Ubuntu Server 24.04 LTS** as the operating system.
6. Selected the **Standard_B1s** VM size.
7. Configured password authentication.
8. Allowed inbound SSH traffic (Port 22) using the default Network Security Group.
9. Used a **30 GB Standard HDD** OS disk.
10. Created and deployed the Virtual Machine.
11. Connected to the VM successfully using SSH.

---

## SSH Command Used

```bash
ssh azureuser@<public-ip>
```

Example:

```bash
ssh azureuser@52.225.85.27
```

---

## Result

Successfully deployed an Azure Virtual Machine and verified remote access through SSH.

---

## Key Takeaways

- Learned how to deploy an Azure Virtual Machine.
- Understood Azure VM configuration options.
- Configured Network Security Group rules for SSH.
- Connected securely to the VM using SSH.
- Verified successful deployment and remote access.

## Outcome

✅ Lab Completed