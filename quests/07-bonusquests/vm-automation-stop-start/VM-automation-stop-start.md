# Azure Automation: Auto Start/Stop VM

Running a VM 24/7 adds up fast. If you don't need the server online around the clock,
scheduled runbooks are the right solution — set it and forget it.

## High-Level Steps

1. Create an Automation Account
2. Write start and stop scripts
3. Import scripts as Runbooks
4. Attach a schedule

---

## Create an Automation Account

Portal: search "Automation Accounts" and follow the prompts.

CLI alternative:
[New-AzAutomationAccount](https://learn.microsoft.com/en-us/powershell/module/az.automation/new-azautomationaccount?view=azps-13.3.0)

---

## Scripts

Both scripts use a User-Assigned Managed Identity for authentication.
Replace `[client ID]` and `[subscription ID]` with your values before importing.

**Stop VM**

Found a starting point on Stack Overflow and adapted it. This version targets VMs
by tag, which makes it reusable across environments without hardcoding VM names.

```powershell
workflow StopVMsByTag
{
    Param(
        [Parameter(Mandatory=$true)][String]$TagName,
        [Parameter(Mandatory=$true)][String]$TagValue,
        [Parameter(Mandatory=$true)][Boolean]$PowerState
    )

    $AzureContext = (Connect-AzAccount -Identity -AccountId "[client ID]").context
    $AzureContext = Set-AzContext -SubscriptionName $AzureContext.Subscription `
                                  -DefaultProfile $AzureContext

    $vms = Get-AzResource -ResourceType Microsoft.Compute/virtualMachines `
                          -TagName $TagName -TagValue $TagValue

    Foreach -Parallel ($vm in $vms) {
        if ($PowerState) {
            Start-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName
            Write-Output "Starting $($vm.Name)"
        } else {
            Stop-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName -Force
            Write-Output "Stopping $($vm.Name)"
        }
    }
}
```

**Start VM**

```powershell
Param(
    [string]$resourceGroup = "MinecraftRG",
    [string]$vmName        = "minecraft-vm"
)

Disable-AzContextAutosave -Scope Process

$clientId = "[client ID]"
Connect-AzAccount -Identity -AccountId $clientId

$subscriptionId = "[subscription ID]"
$AzureContext = Set-AzContext -SubscriptionId $subscriptionId

Start-AzVM -ResourceGroupName $resourceGroup -Name $vmName -DefaultProfile $AzureContext
```

---

## Add to Runbooks and Schedule

1. In the Automation Account, go to **Runbooks**
2. Create a new runbook and paste the script
3. Publish the runbook
4. Go to **Schedules** on the sidebar
5. Create a schedule (time, frequency, timezone) and link it to the runbook

Repeat for both start and stop scripts with schedules that match when you actually
need the server running.
