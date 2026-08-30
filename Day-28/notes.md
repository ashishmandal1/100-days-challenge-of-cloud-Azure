# Day 28 - Azure Nginx VM Internet Access

## Task Overview

The Nautilus DevOps Team had an Azure VM named `datacenter-vm` in the public VNet `datacenter-vnet`, but the VM was not accessible from the internet.

The task was to troubleshoot the network configuration, attach the existing public IP, allow HTTP traffic, and install/configure Nginx.

## Resources

* **VNet:** `datacenter-vnet`
* **VNet Address Space:** `10.0.0.0/16`
* **Subnet:** `datacenter-subnet`
* **Subnet Address Space:** `10.0.0.0/24`
* **VM:** `datacenter-vm`
* **NIC:** `datacenter-vmVMNic`
* **Private IP:** `10.0.0.4`
* **Public IP:** `datacenter-pip`
* **Public IP Address:** `20.245.103.221`
* **NSG:** `datacenter-vmNSG`
* **Route Table:** `datacenter-rtb`
* **Region:** West US

## Troubleshooting

### 1. Verified VNet Configuration

The VNet was located in West US with the following configuration:

```text
VNet: datacenter-vnet
Address Space: 10.0.0.0/16
Subnet: datacenter-subnet
Subnet: 10.0.0.0/24
```

The subnet was associated with the route table:

```text
datacenter-rtb
```

### 2. Fixed Internet Route

The route table initially contained a blocking route:

```text
Block-Internet
0.0.0.0/0
Next Hop: None
```

This prevented the VM from reaching the internet.

The blocking route was deleted:

```bash
az network route-table route delete \
  --resource-group kml_rg_main-6844f1bc80c24488 \
  --route-table-name datacenter-rtb \
  --name Block-Internet
```

A correct internet route was then created:

```bash
az network route-table route create \
  --resource-group kml_rg_main-6844f1bc80c24488 \
  --route-table-name datacenter-rtb \
  --name Internet \
  --address-prefix 0.0.0.0/0 \
  --next-hop-type Internet
```

Final route:

```text
Internet
0.0.0.0/0
Next Hop: Internet
```

### 3. Attached Public IP

The existing public IP `datacenter-pip` was attached to the VM NIC.

NIC:

```text
datacenter-vmVMNic
```

IP configuration:

```text
ipconfigdatacenter-vm
```

Command used:

```bash
az network nic ip-config update \
  --name ipconfigdatacenter-vm \
  --nic-name datacenter-vmVMNic \
  --resource-group kml_rg_main-6844f1bc80c24488 \
  --public-ip-address datacenter-pip
```

The public IP was successfully attached:

```text
Public IP: datacenter-pip
IP Address: 20.245.103.221
```

### 4. Configured NSG for HTTP

The VM NIC was associated with:

```text
datacenter-vmNSG
```

Initially, only SSH port 22 was allowed.

An HTTP rule was created:

```bash
az network nsg rule create \
  --resource-group kml_rg_main-6844f1bc80c24488 \
  --nsg-name datacenter-vmNSG \
  --name allow-http \
  --priority 1100 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --source-address-prefixes '*' \
  --source-port-ranges '*' \
  --destination-address-prefixes '*' \
  --destination-port-ranges 80
```

Final relevant NSG rules:

```text
default-allow-ssh   1000   Inbound   Allow   Tcp   *   22
allow-http          1100   Inbound   Allow   Tcp   *   80
```

### 5. Installed Nginx

Nginx was installed using Azure VM Run Command:

```bash
az vm run-command invoke \
  --resource-group kml_rg_main-6844f1bc80c24488 \
  --name datacenter-vm \
  --command-id RunShellScript \
  --scripts "sudo apt-get update && sudo apt-get install -y nginx && sudo systemctl enable nginx && sudo systemctl start nginx"
```

Nginx installation completed successfully.

### 6. Verified Nginx

Nginx service status:

```text
active
```

Nginx startup configuration:

```text
enabled
```

Nginx was listening on port 80:

```text
0.0.0.0:80
[::]:80
```

Local HTTP test:

```text
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
```

### 7. Verified External Access

The VM's public IP was:

```text
20.245.103.221
```

External HTTP test:

```bash
curl -I --connect-timeout 10 http://20.245.103.221
```

Result:

```text
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Content-Type: text/html
```

This confirmed that the Nginx server was accessible from the internet.

## Final Architecture

```text
Internet
   |
   | HTTP :80
   v
Public IP
20.245.103.221
   |
   v
NIC: datacenter-vmVMNic
   |
   | NSG: datacenter-vmNSG
   | Allow TCP 80
   v
Subnet: datacenter-subnet
   |
   | Route: 0.0.0.0/0 -> Internet
   v
VM: datacenter-vm
   |
   | Nginx
   | Port 80
   v
HTTP 200 OK
```

## Key Learnings

* A public IP alone does not guarantee internet connectivity.
* User-defined routes can override normal internet routing.
* A `0.0.0.0/0` route with `Next Hop: None` can effectively block internet traffic.
* The correct internet route uses `Next Hop Type: Internet`.
* Public IPs are attached to NIC IP configurations, not directly to VMs.
* An NSG must allow inbound TCP port 80 for an internet-facing HTTP server.
* Nginx must be installed, enabled, running, and listening on port 80.
* External testing with `curl` is important because local `localhost` testing alone does not prove internet accessibility.

## Final Verification

| Requirement                   | Status |
| ----------------------------- | ------ |
| VNet allows internet access   | ✅      |
| Blocking route removed        | ✅      |
| Internet route configured     | ✅      |
| Public IP attached            | ✅      |
| HTTP port 80 allowed in NSG   | ✅      |
| Nginx installed               | ✅      |
| Nginx enabled                 | ✅      |
| Nginx running                 | ✅      |
| Nginx listening on port 80    | ✅      |
| External HTTP access verified | ✅      |

## Result

**Azure Nginx VM deployment and internet accessibility successfully completed.**
