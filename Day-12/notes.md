# Day 12 - Add Tags to an Azure Virtual Machine

## Objective
Add a tag to an existing Azure Virtual Machine for better resource organization and management.

## Resource Details
- Resource Type: Virtual Machine
- Virtual Machine Name: nautilus-vm
- Tag Name: Environment
- Tag Value: dev

## Steps Performed
1. Logged in to the Azure Portal.
2. Opened the Virtual Machine **nautilus-vm**.
3. Navigated to **Settings → Tags**.
4. Added the following tag:
   - Key: `Environment`
   - Value: `dev`
5. Saved the changes.
6. Verified that the tag was successfully applied.

## Why Tags are Important
- Organize Azure resources.
- Simplify resource management.
- Enable cost tracking and reporting.
- Improve automation using Azure Policy and scripts.
- Group resources by environment (Dev, Test, Production).

## Result
Successfully added the tag **Environment=dev** to the Azure Virtual Machine **nautilus-vm**.