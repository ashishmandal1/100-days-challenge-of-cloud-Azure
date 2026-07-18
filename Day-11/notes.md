# Day 11 - Resize an Azure Virtual Machine

## Objective
Learn how to resize an Azure Virtual Machine by changing its VM size to provide additional compute resources.

## What I Learned
- Azure VMs can be resized to meet changing workload requirements.
- Most VM size changes require the VM to be stopped (deallocated) first.
- After resizing, the VM can be started again with the new configuration.
- Choosing the appropriate VM size helps optimize performance and resource utilization.

## Steps Performed
1. Logged in to the Azure Portal.
2. Opened the Virtual Machine **devops-vm**.
3. Stopped (deallocated) the VM.
4. Navigated to **Size** under the VM settings.
5. Changed the VM size from **Standard_B1s** to **Standard_B2s**.
6. Applied the resize operation.
7. Started the VM.
8. Verified the VM was in the **Running** state.

## Key Concepts
- Azure Virtual Machine
- VM Resize
- Compute Scaling
- VM Deallocation
- Resource Optimization

## Outcome
Successfully resized the Azure Virtual Machine from **Standard_B1s** to **Standard_B2s** and confirmed it was running after the resize.