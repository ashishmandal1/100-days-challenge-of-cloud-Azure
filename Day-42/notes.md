# Day 42 – Azure Blob Container Cleanup

## Task

Copied the contents of the private Azure Blob container `xfusion-blob-444739628` from storage account `xfusionst444739628` to `/opt` on the `azure-client` host, then deleted the container.

## Azure Resources

* Storage Account: `xfusionst444739628`
* Region: `westus`
* Blob Container: `xfusion-blob-444739628`
* Blob: `xfusion.txt`

## Steps Completed

1. Verified the Azure subscription and storage account.
2. Verified the private blob container existed.
3. Listed the blobs in the container.
4. Found `xfusion.txt` with a size of 33 bytes.
5. Downloaded the blob to:
   `/opt/xfusion.txt`
6. Verified the downloaded file:

   * Size: 33 bytes
   * Content: `Welcome to KKE Azure Cloud Labs!`
7. Deleted the blob container `xfusion-blob-444739628`.
8. Verified the container no longer exists.

## Verification

```bash
az storage container exists \
  --account-name xfusionst444739628 \
  --name xfusion-blob-444739628 \
  --query exists \
  -o tsv
```

Result:

```text
false
```

The file remains available at `/opt/xfusion.txt` after container deletion.
