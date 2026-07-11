# Day 06 - Create Virtual Network and Subnet

## Objective

Create a Virtual Network and a subnet in Microsoft Azure.

## Resources Created

| Resource | Name |
|----------|------|
| Virtual Network | `xfusion-vn` |
| Subnet | `xfusion-subnet` |

## Configuration

| Setting | Value |
|---------|-------|
| Region | Central US |
| Virtual Network Address Space | `10.0.0.0/16` |
| Subnet Address Range | Created within the VNet address space |

## Steps Performed

1. Logged in to the Azure Portal.
2. Navigated to **Virtual Networks**.
3. Clicked **Create**.
4. Entered the Virtual Network name as **xfusion-vn**.
5. Selected **Central US** as the region.
6. Configured the address space as **10.0.0.0/16**.
7. Added a subnet named **xfusion-subnet** within the VNet.
8. Reviewed the configuration and created the resources.

## Result

Successfully created the Virtual Network **xfusion-vn** and the subnet **xfusion-subnet** in the **Central US** region.

## Key Learnings

- A Virtual Network (VNet) provides an isolated network environment in Azure.
- Subnets divide a VNet into smaller logical network segments.
- Every subnet must use an IP address range that belongs to the parent VNet's address space.
- VNets and subnets are the foundation for deploying Azure virtual machines and other networked resources.

## Outcome

✅ Lab Completed