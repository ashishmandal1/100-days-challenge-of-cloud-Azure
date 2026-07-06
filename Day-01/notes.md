# Day 01 - Create an Azure SSH Key Pair

## Objective

Create an RSA SSH key pair named **nautilus-kp** using the Azure Portal.

---

## Lab Details

- Platform: KodeKloud
- Cloud Provider: Microsoft Azure

---

## Steps Performed

1. Logged in to the Azure Portal using the lab credentials.
2. Searched for **SSH keys**.
3. Clicked **Create**.
4. Selected **Generate new key pair**.
5. Entered the name:

```
nautilus-kp
```

6. Selected the key pair type:

```
RSA
```

7. Reviewed the configuration.
8. Clicked **Create**.
9. Downloaded the private key (.pem file).
10. Verified that the SSH key pair was successfully created.

---

## What I Learned

- What an SSH key pair is.
- Difference between Public Key and Private Key.
- Why RSA keys are commonly used.
- How Azure manages SSH keys.
- How to create SSH keys using the Azure Portal.

---

## Key Concepts

### SSH Key Pair

An SSH key pair consists of:

- Public Key
- Private Key

The public key is stored in Azure or on the virtual machine, while the private key remains securely with the user for authentication.

---

### RSA

RSA is one of the most widely used public-key cryptographic algorithms for secure authentication and encrypted communication.

---

## Outcome

Successfully created an Azure RSA SSH key pair named **nautilus-kp**.

✅ Lab Completed