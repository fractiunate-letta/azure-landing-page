# Governance and Azure Policy

Governance is assembled from the local architecture library and applied through the management group module.

## How policy is built

The starter encodes policy default values and assignment modifications in `locals.tf`, then passes them into `main.management.groups.tf`. That includes:

- Policy assignment parameters
- Enforcement mode
- Managed identity settings
- Non-compliance messages
- Assignment overrides
- Resource selectors
- Assignment creation toggles

The source of these values is the generated configuration from `module.config`, which comes from the example `tfvars` file and the architecture library in `terraform/lib`.

## Why this is high impact

Azure Policy assignments at the management group level affect all matching subscriptions beneath that scope. Changing an enforcement mode, adding a deny rule, or altering parameters can block deployments or change resource behavior across the environment.

The starter also creates dependencies so management group governance is applied after the management resources and connectivity resources are ready. This helps avoid ordering failures, but it does not make the policy changes low risk.

## Review checklist

Before applying:

- Review every enabled policy assignment in the chosen example.
- Confirm which assignments are audit-only and which enforce denies.
- Confirm policy parameters match our logging, security, and networking requirements.
- Confirm managed identities used by policy assignments are acceptable.
- Confirm enforcement will not break existing workloads when subscriptions are moved under the hierarchy.

## Related code

- `terraform/locals.tf`
- `terraform/main.management.groups.tf`
- `terraform/lib/`
- `docs/terraform/management-groups.md`
