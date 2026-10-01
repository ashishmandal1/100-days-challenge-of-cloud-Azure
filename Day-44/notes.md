# Azure Day 44 — Integrate Azure VM with Event Hubs

## Objective

Integrate the existing `nautilus-vm` with Azure Event Hubs for centralized log collection.

The task required:

- Create an Event Hubs namespace named `nautilus-namespace`
- Use **East US**
- Use **Standard** pricing tier
- Enable **Auto-inflate**
- Create an Event Hub named `nautilus-hub`
- Verify the existing `nautilus-vm`
- Configure and execute `/home/azureuser/send_logs.py`
- Verify incoming messages using Azure Event Hubs metrics

---

## Environment

| Resource | Value |
|---|---|
| Cloud | Microsoft Azure |
| Region | East US |
| VM | `nautilus-vm` |
| Event Hubs Namespace | `nautilus-namespace` |
| Event Hub | `nautilus-hub` |
| Namespace SKU | Standard |
| Auto-inflate | Enabled |
| Maximum Throughput Units | 20 |
| Event Hub Partitions | 4 |
| Resource Group | `KML_RG_MAIN-11C4765C668B4B0F` |

---

## Steps Performed

### 1. Verified Existing VM

Verified that the existing VM `nautilus-vm` was available in East US.

```bash
az vm show \
  --resource-group "$RG" \
  --name "nautilus-vm" \
  -o table