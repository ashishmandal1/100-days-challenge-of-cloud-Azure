# Azure Day 26 — Create a Public VNet, Subnet and VM

## Objective

Create a public Azure VNet with a subnet that supports public-facing resources, then deploy a VM inside it with SSH access from the internet.

## Requirements

- VNet name: `nautilus-pub-vnet`
- Subnet name: `nautilus-pub-subnet`
- VM name: `nautilus-pub-vm`
- Region: `East US`
- SSH port: `22`
- Public IP must be assigned
- VM must be accessible over the internet

## Resources Created

| Resource | Name | Configuration |
|---|---|---|
| Resource Group | `kml_rg_main-b9efa9dc5a354da3` | East US |
| VNet | `nautilus-pub-vnet` | `10.0.0.0/16` |
| Subnet | `nautilus-pub-subnet` | `10.0.0.0/24` |
| Public IP | `nautilus-pub-pip` | Static, Standard |
| NSG | `nautilus-pub-nsg` | SSH allowed |
| NIC | `nautilus-pub-nic` | Connected to subnet and public IP |
| VM | `nautilus-pub-vm` | Ubuntu 24.04, Standard_B1s |
| OS Disk | VM OS disk | 30 GB, Standard_LRS |

## Network Configuration

- VNet CIDR: `10.0.0.0/16`
- Subnet CIDR: `10.0.0.0/24`
- VM private IP: `10.0.0.4`
- VM public IP: `20.169.211.65`

## NSG Rule

An inbound security rule was created:

```text
Name: Allow-SSH
Priority: 100
Direction: Inbound
Access: Allow
Protocol: TCP
Source: Internet
Destination Port: 22