# Azure Day 35 – VNet Peering

## Objective

Create VNet Peering between a public VNet and a private VNet to enable communication between their virtual machines.

## Existing Resources

* Public VM: `datacenter-pub-vm`
* Public VNet: `datacenter-pub-vnet`
* Public VM Private IP: `10.2.1.4`
* Public VM Public IP: `40.76.64.22`
* Private VM: `datacenter-priv-vm`
* Private VNet: `datacenter-priv-vnet`
* Private VM Private IP: `10.1.1.4`
* Private Subnet: `datacenter-priv-subnet`
* Region: `East US`

## VNet Address Spaces

* Public VNet: `10.2.0.0/16`
* Private VNet: `10.1.0.0/16`

## VNet Peering

Created the required public-to-private peering:

`datacenter-pub-to-priv-peering`

Also created the reciprocal peering:

`datacenter-priv-to-pub-peering`

Both peerings reached the `Connected` state with `Succeeded` provisioning status.

## Connectivity Test

SSH'd into `datacenter-pub-vm` using its public IP and tested connectivity to the private VM:

`ping -c 4 10.1.1.4`

## Verification Result

* 4 packets transmitted
* 4 packets received
* 0% packet loss
* Average latency: 1.425 ms

The successful ping confirmed communication between the public and private VNets through VNet Peering.

## Final Status

Azure Day 35 completed successfully.
