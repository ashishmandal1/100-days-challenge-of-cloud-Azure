# Day 27 - Azure Private VNet, Subnet, NSG and VM

## Task

Created a private Azure Virtual Network, subnet, Network Security Group, and Virtual Machine in the Central US region.

## Resources

* Resource Group: `kml_rg_main-efce6725521941d4`
* Region: `Central US`
* VNet: `nautilus-priv-vnet`
* VNet CIDR: `10.0.0.0/16`
* Subnet: `nautilus-priv-subnet`
* Subnet CIDR: `10.0.0.0/24`
* NSG: `nautilus-priv-nsg`
* VM: `nautilus-priv-vm`
* Private IP: `10.0.0.4`
* Public IP: None

## NSG Rule

Created an inbound SSH rule named `Allow-VNet-SSH`.

```text
Source:       10.0.0.0/16
Destination:  10.0.0.0/16
Port:         22
Protocol:     TCP
Action:       Allow
Priority:     100
Direction:    Inbound
```

The rule allows SSH access only from within the VNet CIDR block.

## VM Networking

The VM is attached to:

```text
VNet:   nautilus-priv-vnet
Subnet: nautilus-priv-subnet
NSG:    nautilus-priv-nsg
```

The VM has private IP `10.0.0.4` and no public IP address.

## Verification

Verified the VM provisioning state as `Succeeded`, the private IP address, the VNet/subnet association, the NSG association, and the SSH rule using Azure CLI.

## Result

Azure Day 27 successfully completed.
