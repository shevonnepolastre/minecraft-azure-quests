# Storage: Storage Account and Blob Container

## Storage Account — YAML Pipeline

Reused the Linux VM deployment YAML as a starting point and adapted it for the storage account. No reason to start from scratch when the structure is the same.

Reference: [Quickstart: Deploy Bicep files using GitHub Actions](http://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deploy-github-actions?tabs=CLI%2Copenid)

Changes made from the original VM pipeline:

- Added Bicep lint step to the workflow
- Updated the secret structure to reference a JSON file containing Tenant ID, Subscription ID, and Client ID

Ran the updated [YAML](https://github.com/shevonnepolastre/minecraft-azure-quests/blob/main/quests/02-storage/deploy-storage-account.yml) which deployed the [storage account Bicep template](https://github.com/shevonnepolastre/minecraft-azure-quests/blob/main/quests/02-storage/storage.bicep) successfully.

---

## Blob Container Creation

Portal creation is straightforward. To do it via PowerShell, use `New-AzStorageContainer` — but you need to pass a storage context first.

Create the context:

```powershell
New-AzStorageContext -StorageAccountName "storageaccountname" -StorageAccountKey "ends with =="
```

This returns the storage context object with endpoints for blob, table, queue, and file. The context is then passed into subsequent commands.

Two things to sort out before the container creation will succeed:

1. **Temporarily enable public IP access** — use `Add-AzStorageAccountNetworkRule` to whitelist your IP
2. **Use the correct storage account key** — had to switch to the second key before it worked

Full PowerShell script: [create-blob-container.ps1](https://github.com/shevonnepolastre/minecraft-azure-quests/blob/main/quests/02-storage/create-blob-container.ps1)

Container created successfully:

| Name | Public Access | Last Modified | 
|------|--------------|---------------|
| worldstorage | Off | 4/10/2025 2:38:29 AM UTC |

---

## Step 6: Install Geyser for Bedrock Cross-Play

[Guide here](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/docs/bedrock-support.md).

Used the Fabric mod version rather than the standalone. The standalone works but requires
restarting Geyser separately after every VM restart, and it needs its own terminal session.
The Fabric mod handles everything in a single launch — cleaner operationally.
