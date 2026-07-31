# Day 19 - Convert Azure Blob Container from Public to Private

## Objective
Convert an existing public Azure Blob container into a private container while leaving another private container unchanged.

---

## Resources Used

- Microsoft Azure Portal
- Azure Storage Account
- Azure Blob Containers

Storage Account:
- devopsst16876

Blob Containers:
- devops-container-21930
- devops-priv-31169

Region:
- southcentralus

---

## Task Performed

Modified the access level of an existing Azure Blob container.

The container `devops-container-21930` was originally configured with public access.

Changed its access level to:

- Private (No anonymous access)

Verified that the second container `devops-priv-31169` remained private and no modifications were made to it.

---

## Steps Performed

1. Logged in to Azure Portal.
2. Opened the Storage Account.
3. Navigated to Blob Containers.
4. Selected `devops-container-21930`.
5. Clicked **Change access level**.
6. Changed access level from Public to:
   - Private (No anonymous access)
7. Saved the changes.
8. Verified that:
   - `devops-container-21930` is Private.
   - `devops-priv-31169` remains Private.

---

## Result

Successfully converted the public blob container into a private container.

No anonymous users can access the container or its blobs.

---

## Key Learnings

- Azure Blob containers support different public access levels.
- Private containers disable anonymous access.
- Public access can be modified at any time.
- Restricting public access improves storage security.
- Private containers require authenticated access using Azure AD, SAS Tokens, or Access Keys.

---

## Azure Services Used

- Azure Storage Account
- Azure Blob Storage
- Blob Container
- Azure Portal

---

## Security Best Practices

- Keep containers private unless public access is explicitly required.
- Regularly audit storage account permissions.
- Use Azure RBAC for controlled access.
- Prefer Azure AD authentication over account keys.
- Disable anonymous access whenever possible.
