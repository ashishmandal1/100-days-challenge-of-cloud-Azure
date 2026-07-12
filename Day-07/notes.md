# Day 07 - Create a Public IP Address in Azure

## Objective

Create a Public IP Address resource named **xfusion-pip** in Microsoft Azure.

## Resources

- Resource Type: Public IP Address
- Name: xfusion-pip
- IP Version: IPv4
- SKU: Standard
- Tier: Regional
- IP Assignment: Static

## Steps Performed

1. Logged in to the Azure Portal.
2. Navigated to **Public IP addresses**.
3. Clicked **Create**.
4. Selected the appropriate subscription and resource group.
5. Entered the name **xfusion-pip**.
6. Chose **IPv4** as the IP version.
7. Selected **Standard** SKU.
8. Set the Tier to **Regional**.
9. Configured the IP address assignment as **Static**.
10. Left the remaining settings as default.
11. Reviewed the configuration and created the Public IP resource.

## Result

- Successfully created a Public IP Address named **xfusion-pip**.

## Key Learnings

- A Public IP Address enables Azure resources to communicate with the internet.
- Standard SKU Public IPs provide enhanced security and availability.
- Static Public IPs retain the same IP address until the resource is deleted.
- Public IP resources can be associated with virtual machines, load balancers, Azure Firewall, NAT Gateway, and other Azure networking services.

## Outcome

✅ Lab Completed