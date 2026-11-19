# Terraform providers

The starter uses Terraform 1.12 and four providers in `terraform.tf`:

- `Azure/alz`
- `hashicorp/azurerm`
- `Azure/azapi`
- `hashicorp/local`

## Azure ALZ provider

The `alz` provider is configured with `library_overwrite_enabled = true` and points at the local `terraform/lib` directory. That local library carries the landing-zone architecture and archetype definitions used to generate the management group hierarchy and policy assignments.

This is important operationally: the starter is not only Terraform HCL. It also includes policy and architecture definitions under `terraform/lib`.

## AzureRM and AzAPI

The default AzureRM provider is not pinned to one subscription, but the starter also declares aliased providers for the management and connectivity subscriptions. That allows different resources to be deployed to the correct platform subscription.

`azapi` is similarly pinned to the management subscription and has a connectivity alias. `skip_provider_registration = true` avoids automatic resource provider registration, which keeps deployment behavior explicit.

## Backend

The backend block is commented out. Before real deployment, configure an Azure backend for state storage, locking, and encryption.

## Practical effect

The provider layout means subscription selection is built into the module. Platform resources are not all sent to whichever subscription happens to be active in the current shell.
