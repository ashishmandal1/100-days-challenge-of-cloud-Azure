# Day 25 — Azure VM Disk Expansion and Data Disk Mount

## 📌 Overview

On Day 25 of the Azure 100 Days Challenge, I expanded the existing OS disk of an Azure VM and added a new data disk.

The existing `nautilus-vm` OS disk was increased from **32 GiB to 64 GiB**. A new **64 GiB Standard HDD** managed disk named `nautilus-disk` was created, attached to the VM, formatted with `ext4`, and mounted at `/mnt/nautilus-disk`.

## 🎯 Objective

The task required:

* Expand the existing VM OS disk from 32 GiB to 64 GiB.
* Create a 64 GiB Standard HDD data disk.
* Name the disk `nautilus-disk`.
* Attach it to `nautilus-vm`.
* Mount it at `/mnt/nautilus-disk`.

## 🏗️ Environment

```text
VM:              nautilus-vm
Resource Group:  KML_RG_MAIN-542705920A2F417B
Region:           eastus
```

## 💾 OS Disk

Original size:

```text
32 GiB
```

New size:

```text
64 GiB
```

The VM had to be deallocated before the OS disk could be resized.

## 💽 Data Disk

```text
Name:       nautilus-disk
Size:       64 GiB
SKU:        Standard_LRS
Type:       Standard HDD
Device:     /dev/sdc
Filesystem: ext4
```

## 📂 Mount Configuration

The disk was mounted at:

```text
/mnt/nautilus-disk
```

The mount was also added to `/etc/fstab` using the disk UUID:

```text
UUID=1669afd1-b256-459d-a540-9e879c90d3f1 /mnt/nautilus-disk ext4 defaults,nofail 0 2
```

## 🔧 Main Commands

### Deallocate VM

```bash
az vm deallocate \
  --resource-group KML_RG_MAIN-542705920A2F417B \
  --name nautilus-vm
```

### Resize OS disk

```bash
az disk update \
  --resource-group KML_RG_MAIN-542705920A2F417B \
  --name nautilus-vm_disk1_af3173df993b4b8eb39e9cb653711808 \
  --size-gb 64
```

### Create data disk

```bash
az disk create \
  --resource-group KML_RG_MAIN-542705920A2F417B \
  --name nautilus-disk \
  --size-gb 64 \
  --sku Standard_LRS \
  --location eastus
```

### Attach data disk

```bash
az vm disk attach \
  --resource-group KML_RG_MAIN-542705920A2F417B \
  --vm-name nautilus-vm \
  --name nautilus-disk
```

### Format the disk

```bash
sudo mkfs.ext4 /dev/sdc
```

### Mount the disk

```bash
sudo mkdir -p /mnt/nautilus-disk
sudo mount /dev/sdc /mnt/nautilus-disk
```

### Verify

```bash
df -h /mnt/nautilus-disk
```

Final result:

```text
/dev/sdc   63G   24K   60G   1%   /mnt/nautilus-disk
```

### Configure Persistent Mount

```bash
echo 'UUID=1669afd1-b256-459d-a540-9e879c90d3f1 /mnt/nautilus-disk ext4 defaults,nofail 0 2' | sudo tee -a /etc/fstab
```

Test:

```bash
sudo mount -a
```

## 🧠 Key Learnings

* How to resize an Azure managed OS disk.
* Why a VM must be deallocated before resizing its OS disk.
* How to create a Standard HDD managed disk.
* How to attach a managed disk to an Azure VM.
* How to identify Linux block devices with `lsblk`.
* How to format a new disk using `mkfs.ext4`.
* How to mount a disk on Linux.
* How to configure persistent mounts using `/etc/fstab`.
* How to verify disk capacity and mount points using `df` and `lsblk`.

## ✅ Final Status

**Azure Day 25 — Completed successfully! 🎉**
