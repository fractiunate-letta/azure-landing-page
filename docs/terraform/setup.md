# Setup and provenance

The Terraform starter is a copy of Microsoft's `platform_landing_zone` template from `Azure/alz-terraform-accelerator` at revision `971521667191010072a3e0a3d8f300a72c701c08`, dated 2026-11-06.

This page records where the code came from and what setup is required before it can be reviewed or deployed.

## Source and license

- Upstream repository: `Azure/alz-terraform-accelerator`
- Copied template: `templates/platform_landing_zone`
- Upstream license: `terraform/LICENSE-upstream`

The license matters because the starter is Microsoft's published code, not code invented for this repository. Retain the license and provenance when updating the starter.

## What was copied

- The Terraform root module files under `terraform/`.
- Full multi-region examples under `terraform/examples/full-multi-region/` for both hub-and-spoke and Azure Virtual WAN.
- The upstream license file.

No organization-specific values were filled in. Subscription IDs, tenant IDs, regions, IP ranges, and deployment identities remain placeholders in the examples.

## Local tooling

Install Terraform 1.12 or a compatible patch release. From the repository root:

```bash
terraform version
terraform -chdir=terraform fmt -check -recursive
```

For initialization and validation without configuring a backend:

```bash
terraform -chdir=terraform init -backend=false
terraform -chdir=terraform validate
```

Initialization downloads providers and modules but does not create or change Azure resources.

## Deployment decisions still required

Before a real plan can be produced, choose:

- The parent management group ID.
- Whether subscriptions already exist for `management`, `connectivity`, `identity`, and `security`.
- The Azure regions to use.
- Hub-and-spoke or Virtual WAN networking.
- Private IP ranges, DNS design, firewall rules, and network security services.
- Security contact and notification settings.
- A state backend with encryption and locking.
- The deployment identity and its Azure permissions.

## Microsoft references

- [Azure landing zone accelerator overview](https://azure.github.io/Azure-Landing-Zones/accelerator/)
- [Terraform starter module](https://azure.github.io/Azure-Landing-Zones/accelerator/starter-terraform/)
- [Accelerator planning](https://azure.github.io/Azure-Landing-Zones/accelerator/0_planning/)
