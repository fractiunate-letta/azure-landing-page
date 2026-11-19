# Terraform platform landing zone

The `terraform/` directory contains Microsoft's Terraform starter for the full Azure platform landing zone. It is a reviewable baseline from which we can configure and deploy the shared platform.

!!! warning "Review before deployment"
    This directory is starter code from Microsoft. It does not know our tenant, subscriptions, regions, networks, or deployment identity. Review it and complete the examples before applying it. Do not apply it to Azure without separate deployment approval.

## What the code creates

- A management group hierarchy under `root_parent_management_group_id`.
- Azure Policy governance, including deny and audit rules from the starter configuration.
- Management subscriptions for the `management`, `connectivity`, `identity`, and `security` platform roles.
- Shared management resources, such as monitoring and automation resources.
- Connectivity in either hub-and-spoke or Azure Virtual WAN topology across one or more regions.
- Deployment-time outputs for the created resources and hierarchy.

## Repository layout

| Path | Purpose |
| --- | --- |
| `terraform/` | Microsoft Terraform starter root |
| `terraform/examples/full-multi-region/hub-and-spoke-vnet.tfvars` | Full multi-region hub-and-spoke example |
| `terraform/examples/full-multi-region/virtual-wan.tfvars` | Full multi-region Azure Virtual WAN example |
| `terraform/LICENSE-upstream` | Upstream license for the starter |
| `docs/terraform/*.md` | Explanation of each major component |

## Provenance

Source: `Azure/alz-terraform-accelerator`

Revision: `971521667191010072a3e0a3d8f300a72c701c08`

Date: 2026-11-06

Keep this provenance if the starter code is updated. Do not remove `terraform/LICENSE-upstream`.

## Prerequisites before real deployment

1. Decide whether this is a new environment or an existing environment to migrate.
2. Choose the parent management group.
3. Decide which platform subscriptions will be used, or create dedicated subscriptions.
4. Choose regions and whether the platform is hub-and-spoke or Virtual WAN.
5. Choose private IP ranges and any network security requirements.
6. Decide where Terraform state will be stored, with locking and encryption.
7. Choose the deployment identity and its Azure roles at every scope.
8. Plan Azure Policy effects, budgets, monitoring, and Defender for Cloud costs.

This starter can deploy more than management groups. It can also deploy networking, security, monitoring, and identity-related resources, depending on the configuration and enabled features.

## Validation commands

Run these from the repository root after installing Terraform and authenticating with Azure CLI. They initialize modules and providers without configuring a remote backend; they do not create Azure resources.

```bash
terraform -chdir=terraform fmt -check -recursive
terraform -chdir=terraform init -backend=false
terraform -chdir=terraform validate
```

Then review a plan:

```bash
terraform -chdir=terraform plan \
  -var-file=examples/full-multi-region/hub-and-spoke-vnet.tfvars \
  -out=tfplan
```

Use `virtual-wan.tfvars` instead if that is the selected topology. The examples contain placeholders such as `<region-1>` and `<tenant-id>`, so they need real values before a meaningful plan can be produced.

## Next reading

- [Setup and provenance](setup.md)
- [Variables and configuration](variables.md)
- [Terraform providers](providers.md)
- [Management groups](management-groups.md)
- [Governance and Azure Policy](governance.md)
- [Subscriptions](subscriptions.md)
- [Management resources](management-resources.md)
- [Hub-and-spoke networking](networking-hub-and-spoke.md)
- [Virtual WAN networking](networking-virtual-wan.md)
- [Outputs](outputs.md)
- [Bootstrap, state, and deployment](bootstrap.md)
