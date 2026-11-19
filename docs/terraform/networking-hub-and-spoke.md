# Hub-and-spoke networking

`main.connectivity.hub.and.spoke.virtual.network.tf` deploys the hub-and-spoke network topology when `connectivity_type = "hub_and_spoke_vnet"`.

## What it uses

The module `Azure/avm-ptn-alz-connectivity-hub-and-spoke-vnet/azurerm` receives:

- `hub_and_spoke_networks_settings`
- `hub_virtual_networks`
- Shared tags
- The aliased connectivity providers

The resource groups used by networking are created first by `main.resource.groups.tf`, then merged into the connectivity settings as a dependency.

## What it can create

Depending on the example configuration, the hub-and-spoke deployment can create shared networking resources such as:

- Hub virtual networks
- Azure Firewall
- VPN or ExpressRoute gateways
- Azure DDoS Protection
- Private DNS zones
- Route tables and network security resources

## Deployment scope

These resources are deployed to the `connectivity` subscription, not the management subscription.

## Example

See `terraform/examples/full-multi-region/hub-and-spoke-vnet.tfvars` for the full multi-region example.

## Review focus

- Confirm hub and spoke IP ranges do not overlap with existing networks.
- Decide whether gateways, firewall, and private DNS are needed in every selected region.
- Confirm firewall and DDoS settings match the security requirements.
- Review peering and routing assumptions before applying changes.
