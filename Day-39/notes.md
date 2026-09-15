# Day 39 — Azure Static Website Hosting

## Objective

Host a publicly accessible static website using Azure Storage.

## Resource Details

* Resource Group: `kml_rg_main-349cbea4d750432e`
* Location: `East US`
* Storage Account: `xfusionwebst474122346`
* Storage Type: `StorageV2`
* SKU: `Standard_LRS`
* Static Website: Enabled
* Index Document: `index.html`
* Container: `$web`

## Website File

Uploaded:

`/root/index.html`

Website content:

```html
<html><body><h1>Welcome to KKE labs!</h1></body></html>
```

## Static Website URL

`https://xfusionwebst474122346.z13.web.core.windows.net/`

## Verification

Verified the `$web` container:

* File: `index.html`
* Size: 56 bytes

Verified the public website using `curl`:

* HTTP Status: `200 OK`
* Content-Type: `text/html`
* Website content successfully displayed.

## Result

Day 39 completed successfully. Azure Storage static website hosting is enabled, the website file is uploaded to `$web`, and the public static website URL is accessible.
