# Day 08 Notes - Azure Virtual Network

## What is an Azure Virtual Network (VNet)?

An Azure Virtual Network (VNet) is a private network in Azure that allows Azure resources such as Virtual Machines, Load Balancers, Databases, and App Services to securely communicate with each other.

A VNet is similar to a traditional network in an on-premises data center but is fully managed by Azure.

---

## Why use a VNet?

- Secure communication between Azure resources
- Isolation from other Azure customers
- Connect Azure to on-premises networks
- Internet access when required
- Control traffic using NSGs and routing

---

## Address Space

The VNet uses an IP address range called the address space.

Example:

192.168.0.0/24

This provides 256 IP addresses.

---

## Configuration Used

Virtual Network Name:
datacenter-vnet

Region:
East US

Address Space:
192.168.0.0/24

---

## Steps Performed

1. Open Azure Portal.
2. Navigate to Virtual Networks.
3. Click Create.
4. Enter the Virtual Network name:
   datacenter-vnet
5. Select Region:
   East US
6. Configure IPv4 Address Space:
   192.168.0.0/24
7. Review settings.
8. Click Create.

---

## Key Concepts Learned

- Virtual Network (VNet)
- Address Space
- IPv4 CIDR Notation
- Azure Networking Basics
- Resource Deployment in Azure

---

## Real-world Use Case

A company creates a Virtual Network before deploying Virtual Machines so that all servers can securely communicate within a private network while remaining isolated from public internet traffic.

---

## Summary

Today I learned how to create an Azure Virtual Network and configure its address space. VNets are one of the core networking services in Azure and form the foundation for securely deploying cloud resources.

## Outcome

✅ Lab Completed