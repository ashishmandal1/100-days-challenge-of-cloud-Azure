# Azure Day 15 - Create Network Security Group (NSG)

## Task

Create a Network Security Group (NSG) with inbound security rules for HTTP and SSH traffic.

## Requirements

* **NSG Name:** `devops-nsg`
* **HTTP Rule Name:** `Allow-HTTP`
* **HTTP Port:** `80`
* **SSH Rule Name:** `Allow-SSH`
* **SSH Port:** `22`
* **Source CIDR:** `0.0.0.0/0`

## What is a Network Security Group?

A Network Security Group (NSG) in Microsoft Azure acts as a virtual firewall that controls inbound and outbound network traffic to Azure resources.

NSGs use security rules to allow or deny traffic based on:

* Source
* Source port
* Destination
* Destination port
* Protocol
* Priority
* Action

## NSG Created

```text
Name: devops-nsg
```

## Inbound Security Rules

### 1. Allow-HTTP

```text
Name: Allow-HTTP
Service: HTTP
Protocol: TCP
Destination Port: 80
Source: 0.0.0.0/0
Action: Allow
```

### 2. Allow-SSH

```text
Name: Allow-SSH
Service: SSH
Protocol: TCP
Destination Port: 22
Source: 0.0.0.0/0
Action: Allow
```

For the **Source port ranges**, `*` was used because clients can connect from any source port. The destination ports are the service ports: `80` for HTTP and `22` for SSH.

## Result

Successfully created the Azure Network Security Group:

```text
devops-nsg
```

The following inbound rules were added:

```text
Allow-HTTP  -> TCP port 80
Allow-SSH   -> TCP port 22
```

Both rules allow traffic from:

```text
0.0.0.0/0
```

## Key Learnings

* An NSG acts as a virtual firewall in Azure.
* Inbound rules control traffic entering a resource or subnet.
* HTTP uses TCP port 80.
* SSH uses TCP port 22.
* `*` in source port ranges means any source port.
* The NSG must be associated with a subnet or network interface to control traffic for Azure resources.
* An NSG can be associated with a subnet or network interface.

## Azure Service

* **Service:** Azure Network Security Group
* **Resource:** `devops-nsg`
* **Rules:** HTTP and SSH inbound rules
* **Region:** As selected during resource creation
