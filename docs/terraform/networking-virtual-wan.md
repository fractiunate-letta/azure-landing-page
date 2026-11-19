# Virtual WAN networking

`main.connectivity.virtual.wan.tf` deploys the Azure Virtual WAN topology when `connectivity_type = "virtual_wan"`.

## What it uses

The module `Azure/avm-ptn-alz-connectivity-virtual-wan/azurerm` receives:

- `virtual_wan_settings`
- `virtual_hubs`
- `route_maps`
- Optional body-change ignore rules
- Shared tags
- The aliased connectivity providers

As with hub-and-spoke, connectivity resource groups are created first and then merged into the settings.

## What it can create

Depending on the example configuration, the Virtual WAN deployment can create shared networking resources such as:

- Azure Virtual WAN
- Virtual hubs in one or more regions
- Azure Firewall in hubs
- VPN or ExpressRoute gateways
- Private DNS zones
- Route maps and hub routing intent

## Deployment scope

These resources are deployed to the `connectivity` subscription.

## Example

See `terraform/examples/full-multi-region/virtual-wan.tfvars` for the full multi-region example.

## Review focus

- Confirm whether Virtual WAN or hub-and-spoke is the intended operating model.
- Confirm hub regions and IP ranges.
- Review firewall and routing intent in each hub.
- Review gateway and DNS designs before deployment.
