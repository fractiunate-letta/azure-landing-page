# Bootstrap, state, and deployment

The Terraform starter in `terraform/` is the platform landing zone code. Microsoft's accelerator also has a separate bootstrap phase that prepares the delivery environment.

## Bootstrap vs platform deployment

These are different steps:

1. **Bootstrap**: Creates or prepares the delivery environment, such as repositories, pipelines, managed identities, and Terraform state storage.
2. **Platform deployment**: Applies the starter code to create the Azure management group hierarchy, governance, management resources, and connectivity.

The files in `terraform/` are for the platform deployment side. They do not replace the accelerator's bootstrap process.

## State backend

`terraform.tf` contains a commented-out backend block. Before real deployment, configure an Azure backend with:

- A dedicated storage account
- State container
- Encryption
- Locking
- Least-privilege access for the deployment identity

Do not commit state files or backend credentials.

## Deployment identity

The deployment identity must have permissions at every relevant scope. For the platform landing zone, that can include permissions to:

- Create management groups
- Assign Azure Policies
- Create role assignments
- Deploy resources into the management and connectivity subscriptions
- Read or write Terraform state in the selected backend

The exact roles depend on the enabled modules and selected topology. Review them before deployment rather than assuming one universal role assignment.

## Suggested safe sequence

1. Review the selected example.
2. Replace placeholder tenant, subscription, region, and network values.
3. Configure a state backend.
4. Authenticate as the deployment identity.
5. Run `terraform plan` and review the full plan.
6. Get approval for the deployment.
7. Apply in a controlled environment before production.

## Costs

The starter can create billable shared resources, including networking, firewall, monitoring, and security services. Review the selected configuration for cost before applying it.

## Microsoft references

- [Accelerator overview](https://azure.github.io/Azure-Landing-Zones/accelerator/)
- [Terraform starter module](https://azure.github.io/Azure-Landing-Zones/accelerator/starter-terraform/)
- [Azure landing zone accelerator repository](https://github.com/Azure/alz-terraform-accelerator)
