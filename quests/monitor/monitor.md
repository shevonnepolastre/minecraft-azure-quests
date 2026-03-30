# Monitoring

## Log Analytics Workspace

Deployed using an ARM template with a parameter file.

Initially tried the `Free` SKU — that's no longer supported in Azure, so switched to `pergb2018`.

Deployed via CLI:
```bash
az deployment group create \
  --name AzureMonitorDeployment \
  --resource-group MinecraftRG \
  --template-file log-analytics-creation.json \
  --parameters @log-analyticsws-param.json
```

Deployment succeeded. Workspace `minecraft-logs` created in `eastus2` with the following configuration:

| Parameter | Value |
|-----------|-------|
| SKU | pergb2018 |
| Retention | 30 days |
| Heartbeat table retention | 30 days |
| Resource permissions | Enabled |
| Location | eastus2 |

Two resources provisioned:
- `Microsoft.OperationalInsights/workspaces/minecraft-logs`
- `Microsoft.OperationalInsights/workspaces/minecraft-logs/tables/Heartbeat`
