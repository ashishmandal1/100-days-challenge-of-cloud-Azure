# Day 43 – Azure Application Gateway with Ubuntu VM

## Task

Created an Azure Ubuntu VM running Nginx and configured an Azure Application Gateway to route HTTP traffic to the VM.

## Resources Created

| Resource                      | Name                          | Location         |
| ----------------------------- | ----------------------------- | ---------------- |
| Network Security Group        | `nautilus-nsg`                | West US          |
| NSG Rule                      | `Allow-HTTP`                  | TCP/80 Inbound   |
| Virtual Network               | `nautilus-vnet`               | West US          |
| VM Subnet                     | `nautilus-vm-subnet`          | `10.0.1.0/24`    |
| Application Gateway Subnet    | `nautilus-agw-subnet`         | `10.0.2.0/24`    |
| Virtual Machine               | `nautilus-vm`                 | West US          |
| VM Size                       | `Standard_B1s`                |                  |
| OS                            | Ubuntu 22.04                  |                  |
| OS Disk                       | Standard HDD (`Standard_LRS`) |                  |
| VM Public IP                  | `104.40.32.98`                |                  |
| VM Private IP                 | `10.0.1.4`                    |                  |
| Application Gateway           | `nautilus-agw`                | West US          |
| Application Gateway SKU       | Basic                         |                  |
| Application Gateway Public IP | `nautilus-agw-ip`             | `52.250.241.137` |
| Backend Pool                  | `nautilus-backendpool`        | `10.0.1.4`       |
| HTTP Settings                 | `nautilus-http-settings`      | Port 80          |
| Listener                      | `nautilus-listener`           | HTTP/80          |
| Routing Rule                  | `nautilus-routing-rule`       | HTTP → Backend   |

## NSG Configuration

Created `nautilus-nsg` and allowed inbound HTTP traffic:

* Rule: `Allow-HTTP`
* Protocol: TCP
* Direction: Inbound
* Priority: 100
* Source: Any (`*`)
* Destination Port: 80
* Access: Allow

## SSH Key

Generated a local RSA SSH key pair:

```bash
mkdir -p ~/.ssh
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""
```

The public key was used for VM SSH authentication.

> Never commit or share `~/.ssh/id_rsa`. Only the public key `~/.ssh/id_rsa.pub` should be shared.

## VM Configuration

Created `nautilus-vm` using Ubuntu 22.04 with:

* Size: `Standard_B1s`
* OS disk: Standard HDD
* Authentication: SSH public key
* NSG: `nautilus-nsg`
* Private IP: `10.0.1.4`

### Nginx User Data

```bash
#!/bin/bash
apt-get update
apt-get install -y nginx
systemctl enable nginx
systemctl start nginx
```

## Nginx Verification

Verified Nginx directly on the VM:

```bash
az vm run-command invoke \
  --resource-group "$RG" \
  --name "nautilus-vm" \
  --command-id RunShellScript \
  --scripts "systemctl is-active nginx && curl -I http://127.0.0.1"
```

Nginx returned:

```text
active
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
```

## Application Gateway

Created `nautilus-agw` with:

* Tier: Basic
* VNet: `nautilus-vnet`
* Subnet: `nautilus-agw-subnet`
* Frontend: `nautilus-agw-ip`
* Backend pool: `nautilus-backendpool`
* Backend target: `10.0.1.4`
* Backend HTTP port: 80
* Listener: `nautilus-listener`
* Routing rule: `nautilus-routing-rule`

The lab subscription only permitted the **Basic Application Gateway SKU**, so Basic was used.

## End-to-End Verification

Tested the Application Gateway public IP:

```bash
curl -i http://52.250.241.137
```

Result:

```text
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
```

The standard Nginx Welcome page was returned.

This confirmed the traffic path:

```text
Client
   |
   | HTTP :80
   v
nautilus-agw
   |
   | nautilus-routing-rule
   v
nautilus-backendpool
   |
   v
nautilus-vm (10.0.1.4)
   |
   v
Nginx :80
```

## Automated Validation

Located the lab validator:

```bash
find /usr/share -maxdepth 3 -type f -name "test.py" 2>/dev/null
```

Validator:

```text
/usr/share/test.py
```

Ran:

```bash
pytest -v /usr/share/test.py
```

The Azure Application Gateway test completed successfully.

## Result

**Azure Day 43 – Application Gateway + VM setup completed and validated successfully.**
