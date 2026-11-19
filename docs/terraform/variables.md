# Variables and configuration

The starter takes a small number of root inputs and then builds a large internal configuration from them.

## Root inputs

The main inputs live in `variables.tf`:

- `starter_locations`: Azure regions used for platform resources.
- `subscription_ids`: map from platform roles to subscription IDs. The allowed keys are `management`, `connectivity`, `identity`, and `security`.
- `required_subscription_keys`: which subscription roles must have valid GUIDs. The upstream default is `["connectivity", "management"]`.
- `root_parent_management_group_id`: parent management group for the landing-zone hierarchy. If empty, the hierarchy is placed under the tenant root group.
- `enable_telemetry`: sends deployment telemetry to Microsoft.
- `tags`: default tags applied to resources.
- `custom_replacements`: names and identifiers used to keep generated names consistent.

The starter validates subscription IDs and starter locations before deployment, so many mistakes fail early.

## Configuration assembly

`main.config.tf` calls the local `config-templating` module to combine:

- Locations and subscription IDs
- Connectivity resource group definitions
- Hub-and-spoke or Virtual WAN settings
- Management resource settings
- Management group settings
- Tags
- Optional body-change ignore rules

The module output is then consumed by the management group, governance, and connectivity resources. This is why one `tfvars` file can drive a large platform deployment.

## Example configuration files

The examples under `terraform/examples/full-multi-region/` show full-platform choices for both network topologies. They contain placeholders such as:

- `<region-1>`
- `<tenant-id>`
- `replace_me@replace_me.com`

They are examples, not ready-to-apply values. Replace them with our tenant, subscriptions, regions, and network ranges before planning a deployment.

## Important validation

`subscription_ids` is constrained to the four platform keys. The management and connectivity subscriptions are required by default, while identity and security can be deferred by changing `required_subscription_keys`. Microsoft recommends all four for a full platform landing zone, but the starter can be adapted when some platform subscriptions are not yet available.
