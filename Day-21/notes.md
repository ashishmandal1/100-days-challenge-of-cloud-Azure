# Day 21 – Create an Azure VM with a Static Public IP

## Objective

Create an Azure Virtual Machine named **nautilus-vm** in the **Central US** region using an Ubuntu image and **Standard_B1s** VM size. Generate an SSH key pair on the `azure-client` host, associate the public key with the VM, attach a **Static Public IP** named **nautilus-pip**, and verify SSH connectivity.

---

## Services Used

* Azure Virtual Machines
* Azure Public IP Address
* Azure Virtual Network
* Azure Network Security Group (NSG)
* SSH

---

## Steps Performed

1. Logged in to Azure using the credentials provided by the lab.
2. Generated an SSH key pair on the `azure-client` host.
3. Created a Static Public IP named **nautilus-pip**.
4. Created an Ubuntu Virtual Machine named **nautilus-vm**.
5. Selected **Standard_B1s** as the VM size.
6. Configured SSH authentication using the generated public key.
7. Associated the existing Static Public IP during VM creation.
8. Allowed SSH (port 22) through the Network Security Group.
9. Connected to the VM successfully using SSH to verify access.

---

## Commands Used

Generate SSH key:

```bash
mkdir -p ~/.ssh
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""
```

Display the public key:

```bash
cat ~/.ssh/id_rsa.pub
```

Connect to the VM:

```bash
ssh azureuser@<PUBLIC_IP>
```

Exit the VM:

```bash
exit
```

---

## Key Learning

* Azure Virtual Machines can use SSH key authentication instead of passwords.
* Static Public IP addresses ensure the VM keeps the same public IP after restarts.
* The public key is added during VM creation, while the private key remains on the client machine.
* Network Security Groups control inbound and outbound network traffic.
* SSH is the recommended and secure method for managing Linux VMs in Azure.

---

## Common Mistakes to Avoid

* Creating resources in the wrong region (use **Central US**).
* Selecting the wrong VM size instead of **Standard_B1s**.
* Generating the SSH key on the local machine instead of the `azure-client`.
* Trying to attach the Public IP after the VM is already running instead of during VM creation.
* Selecting an unsupported OS disk type for the lab. Use **Standard SSD (StandardSSD_LRS)**.
* Forgetting to allow SSH (port 22) in the NSG.
