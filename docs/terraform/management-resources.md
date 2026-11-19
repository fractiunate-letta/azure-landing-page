# Management resources

`main.management.resources.tf` deploys shared management services into the `management` subscription.

## What it can create

The module `Azure/avm-ptn-alz-management/azurerm` is driven by `management_resource_settings` and can create:

- A management resource group
- A Log Analytics workspace
- Data collection rules for change tracking, VM insights, and Defender for SQL
- Log Analytics solution plans
- Microsoft Sentinel onboarding
- Azure Monitor Agent managed identities

The upstream starter leaves automation account creation disabled by default and provides names for the Log Analytics workspace and resource group if none are supplied.

## Where it deploys

The module uses the aliased `azurerm.management` provider, so these resources go to the `management` subscription rather than the currently selected shell subscription.

## Why review it carefully

Management resources create recurring cost and affect telemetry collection across the environment. Sentinel onboarding, data collection rules, retention, and daily quotas should be chosen deliberately.

## Related settings

See `variables.management.tf` for the full `management_resource_settings` schema and `docs/terraform/subscriptions.md` for the platform subscription model.
