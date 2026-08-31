# Day 29 - Azure Container Registry and Docker Image

## Objective

Create an Azure Container Registry (ACR), build a Docker image using the provided Dockerfile, and push the image to the ACR repository.

## Resources Created

* **ACR Name:** `devopsacr30543`
* **Region:** East US
* **Pricing Tier:** Basic
* **Login Server:** `devopsacr30543.azurecr.io`
* **Repository:** `devopsacr30543`
* **Image Tag:** `latest`

## Step 1 - Verify Azure Environment

Checked the active Azure subscription and confirmed the Azure CLI was authenticated.

```bash
az account show --query "{SubscriptionId:id, TenantId:tenantId, User:user.name}" -o table
```

The correct KodeKloud resource group was:

```text
kml_rg_main-73d40d4400d64878
```

## Step 2 - Verify Dockerfile

The Docker application was available under:

```text
/root/pyapp
```

Contents:

```text
app.py
Dockerfile
requirements.txt
```

Dockerfile:

```dockerfile
FROM python:3.8-slim
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

Docker was available on the Azure client:

```bash
docker --version
```

## Step 3 - Create Azure Container Registry

Created a Basic ACR in East US:

```bash
az acr create \
  --name devopsacr30543 \
  --resource-group kml_rg_main-73d40d4400d64878 \
  --location eastus \
  --sku Basic
```

Verified the registry:

```bash
az acr show \
  --name devopsacr30543 \
  --resource-group kml_rg_main-73d40d4400d64878 \
  --query "{Name:name,Location:location,Sku:sku.name,LoginServer:loginServer}" \
  -o table
```

Result:

```text
Name            Location    Sku    LoginServer
devopsacr30543  eastus      Basic  devopsacr30543.azurecr.io
```

## Step 4 - Login to ACR

Authenticated Docker with the Azure Container Registry:

```bash
az acr login --name devopsacr30543
```

Result:

```text
Login Succeeded
```

## Step 5 - Build Docker Image

Changed to the application directory:

```bash
cd /root/pyapp
```

Built the Docker image with the required registry and tag:

```bash
docker build -t devopsacr30543.azurecr.io/devopsacr30543:latest .
```

The image was successfully built.

## Step 6 - Push Image to ACR

Pushed the image:

```bash
docker push devopsacr30543.azurecr.io/devopsacr30543:latest
```

The push completed successfully with digest:

```text
sha256:746823b1b1bca7eb197d1af69779169a33a428f1bee58ffb2784d4d3e57d12b3
```

## Step 7 - Verify Repository

Verified that the image exists in the ACR repository:

```bash
az acr repository show-tags \
  --name devopsacr30543 \
  --repository devopsacr30543 \
  -o table
```

Output:

```text
Result
--------
latest
```

## Architecture

```text
Dockerfile
    |
    | docker build
    v
Docker Image
    |
    | docker push
    v
Azure Container Registry
devopsacr30543.azurecr.io
    |
    └── devopsacr30543:latest
```

## Key Concepts Learned

* Azure Container Registry (ACR)
* ACR pricing tiers
* Docker image building
* Docker image tagging
* Docker registry authentication
* Docker image pushing
* ACR repositories
* Image tags
* Azure CLI
* Container image management

## Final Status

**Day 29 Azure completed successfully. ✅**
