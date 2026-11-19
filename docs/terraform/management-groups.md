# Management groups

`main.management.groups.tf` deploys the management group hierarchy through the Azure Verified Module `Azure/avm-ptn-alz/azurerm`.

The module is controlled by `management_groups_enabled` and consumes settings assembled by `module.config`. That includes:

- The parent management group
- The architecture name
- The location
- Subscription placement
- Policy assignment modifications
- Role assignments
- Hierarchy settings
- Deployment dependencies and retry behavior

The upstream module creates the platform and workload management-group structure under the chosen parent. It also associates the platform subscriptions with their intended management groups.

## Why this matters

The management group hierarchy is the control plane for subscription organization. It is where shared policies and governance are attached, so getting this hierarchy right affects every subscription placed beneath it.

## Key review points

- `root_parent_management_group_id` decides where the hierarchy is anchored.
- Subscription placement can move subscriptions between management groups.
- Policy changes applied at the hierarchy level can affect all descendant subscriptions.
- Deployment ordering matters because policies and role assignments must exist before dependent resources are applied.

The management group module should be reviewed before any deployment because changes here are high-impact and broad.
