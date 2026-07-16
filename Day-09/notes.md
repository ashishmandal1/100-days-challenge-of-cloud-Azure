# Day 09 Notes - Attach a Network Interface (NIC) to an Azure Virtual Machine

## What is a Network Interface (NIC)?
A Network Interface (NIC) is a virtual network adapter that enables an Azure Virtual Machine to communicate with other Azure resources and the internet.

## Why Attach an Additional NIC?
- Connect the VM to multiple networks.
- Separate application and management traffic.
- Improve network design and security.
- Support advanced networking scenarios.

## Steps Performed
1. Open the Azure Portal.
2. Navigate to **Virtual Machines**.
3. Select the virtual machine (`nautilus-vm`).
4. Stop (deallocate) the VM.
5. Open **Networking** settings.
6. Choose **Attach existing network interface**.
7. Select `nautilus-nic`.
8. Attach the NIC.
9. Verify the NIC status is **Attached**.
10. Start the VM and confirm it is in the **Running** state.

## Important Notes
- A VM must be **Stopped (deallocated)** before adding or removing NICs.
- The VM and NIC must be in the same Azure region.
- All NICs attached to a VM must belong to the same virtual network (VNet).
- The number of NICs supported depends on the VM size.

## Azure Concepts Learned
- Azure Virtual Machine (VM)
- Network Interface (NIC)
- Virtual Network (VNet)
- VM Networking
- Multi-NIC Configuration

## Result
Successfully attached an existing network interface (`nautilus-nic`) to the Azure Virtual Machine (`nautilus-vm`) and verified the NIC status as **Attached**.

## Outcome

✅ Lab Completed