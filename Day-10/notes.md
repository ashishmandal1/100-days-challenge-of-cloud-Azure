# Day 10 - Attach a Public IP to an Azure Virtual Machine

## Objective
Attach an existing Public IP address to the network interface (NIC) of an existing Azure Virtual Machine.

## Resources Used
- Azure Virtual Machine (VM)
- Network Interface (NIC)
- Public IP Address

## Task Details
- VM Name: `devops-vm-pip`
- Public IP: `devops-pip`

## Steps Performed
1. Stopped (deallocated) the virtual machine.
2. Opened the VM's Network Interface (NIC).
3. Navigated to **IP configurations**.
4. Selected the primary IP configuration.
5. Associated the existing Public IP `devops-pip`.
6. Saved the configuration.
7. Started the virtual machine.
8. Verified that the Public IP was successfully assigned.

## Key Learnings
- A Public IP is associated with a VM through its Network Interface.
- Some NIC changes require the VM to be stopped (deallocated).
- The IP configuration determines the public and private IP assignments for a NIC.

## Outcome
Successfully attached the existing Public IP `devops-pip` to the network interface of `devops-vm-pip`.

## Outcome

✅ Lab Completed