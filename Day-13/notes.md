# Azure Day 13: Configure Root SSH Key Access

## Task

Add the root user's SSH public key from the Azure client (landing) host to the `authorized_keys` file of the root user on the Azure VM.

## VM Details

* **VM Name:** `xfusion-vm`
* **Region:** `westus`
* **Default SSH User:** `azureuser`
* **Source Host:** Azure client/landing host
* **Source Public Key:** `/root/.ssh/id_rsa.pub`
* **Destination:** `/root/.ssh/authorized_keys`

## Steps Performed

### 1. Verified the VM

```bash
az vm list -d -o table
```

Verified that `xfusion-vm` was running in the `westus` region.

### 2. Connected to the VM

```bash
ssh azureuser@<VM_PUBLIC_IP>
```

### 3. Created the root SSH directory

```bash
sudo mkdir -p /root/.ssh
sudo chmod 700 /root/.ssh
```

### 4. Copied the root public key

The public key from the Azure client host was copied to the VM:

```text
/root/.ssh/id_rsa.pub
```

Destination:

```text
/root/.ssh/authorized_keys
```

### 5. Set correct permissions

```bash
sudo chmod 700 /root/.ssh
sudo chmod 600 /root/.ssh/authorized_keys
```

### 6. Resolved the Azure root-login restriction

The original Azure-generated key entry contained a forced command that displayed:

```text
Please login as the user "azureuser" rather than the user "root".
```

The restricted entry was removed, while the actual root public key was retained in:

```text
/root/.ssh/authorized_keys
```

### 7. Verified Passwordless Root SSH

From the Azure client host:

```bash
ssh root@<VM_PUBLIC_IP>
```

Successfully logged in as:

```text
root@xfusion-vm:~#
```

Verified the user:

```bash
whoami
```

Output:

```text
root
```

## Key Concepts Learned

* SSH public keys are stored in `authorized_keys`.
* The root user's SSH configuration is located at `/root/.ssh/authorized_keys`.
* The `.ssh` directory should have permission `700`.
* The `authorized_keys` file should have permission `600`.
* SSH key authentication allows passwordless login.
* Azure may create restricted SSH key entries that prevent direct root login.
* A forced command in `authorized_keys` can restrict what happens after authentication.

## Result

✅ Successfully configured passwordless SSH access to `xfusion-vm` as the `root` user using the root user's public key from the Azure client host.
