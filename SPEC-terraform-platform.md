# Terraform platform landing zone — V1

Status: implemented

## Objective

Add Microsoft's full Terraform platform landing zone starter to `terraform/` and explain every major part in Zensical documentation. Prepare code for review and later configuration; do not create or modify Azure resources.

## Scope

- Base the starter on Microsoft's `Azure/alz-terraform-accelerator`, revision `971521667191010072a3e0a3d8f300a72c701c08` (6 November 2026); preserve its license and record provenance.
- Include the upstream full-platform starter and its full multi-region hub-and-spoke and Virtual WAN examples without inventing subscription IDs, tenant IDs, addresses, regions, or credentials.
- Document the configuration, providers, management groups, governance, subscriptions, shared management resources, networking options, outputs, and the separate accelerator bootstrap process. Explain prerequisites, state, permissions, costs, and deployment steps.
- Keep organization-specific design choices, deployment credentials, and state backend configuration explicit rather than claiming the starter is ready to apply.

## Commands and verification

- Format: `terraform -chdir=terraform fmt -check -recursive`.
- Initialize without configuring a backend: `terraform -chdir=terraform init -backend=false`.
- Validate: `terraform -chdir=terraform validate`.
- Documentation: `zensical build --clean`.
- Verify that documentation describes the actual included code and that upstream licensing and attribution are present.

Terraform initialization downloads providers and modules but does not deploy Azure resources. If dependencies or tooling cannot be downloaded, report the exact limitation rather than claiming validation passed.

## Structure and style

- `terraform/`: upstream starter, configuration examples, and provenance.
- `docs/`: concise pages explaining the code and its operation, linked from the existing documentation.
- Preserve upstream HCL style and version constraints; avoid unnecessary local changes.

## Boundaries

- **Always:** review upstream source, protect secrets and Terraform state, and verify without applying.
- **Ask first:** applying changes, creating cloud resources, selecting actual production subscription or network settings, or changing deployment infrastructure.
- **Never:** commit credentials, real state files, or generated provider directories.

## Success criteria

1. The full Microsoft starter and relevant examples are present with their source revision and licensing.
2. Terraform formatting and backend-free initialization/validation succeed, or any external blocker is documented accurately.
3. Documentation builds and explains each major code component, required inputs, and how bootstrap differs from platform deployment.
4. No Azure resources have been created or modified.

## Open decisions for eventual deployment

Management group placement, subscriptions, regions, networking topology and IP ranges, security contacts, state backend, identity, and CI/CD setup remain to be chosen before any real deployment.
