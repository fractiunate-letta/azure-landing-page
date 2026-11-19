# Azure landing zones

An **Azure landing zone** is a blueprint for organizing, securing, and operating Azure resources across subscriptions. It is an architecture, not a single Azure resource or a separate subscription.

- The **platform landing zone** provides shared foundations: management groups, governance, and, where needed, shared networking and monitoring.
- A **workload landing zone** is where a particular application or workload runs. It includes its development, test, and production environments, each using one or more subscriptions.

Most organizations use one platform landing zone per Microsoft Entra tenant. [1]

## Documentation

- [Azure landing zones overview](index.md)
- [Terraform platform landing zone](terraform/index.md)

## How subscriptions fit together

Management groups organize subscriptions and apply shared rules. A subscription inherits policies and access assignments from its parent management groups. [1][3]

```text
Microsoft Entra tenant
└── Management groups
    ├── Platform
    │   ├── Management subscription
    │   └── Connectivity subscription
    └── Workloads
        ├── Application A — development subscription
        ├── Application A — production subscription
        └── Application B — production subscription
```

This is a simplified example, not a required hierarchy. Existing subscriptions can be organized into the hierarchy; creating a landing zone does not require replacing them. Review the policies and access they will inherit **before moving them**. Separate dev and production subscriptions when isolation is needed. [1][3]

## Set it up

1. **Plan:** Identify the tenant, existing subscriptions, owners, environments, regions, networking needs, costs, and required guardrails.
2. **Choose an implementation:** Use a Microsoft platform landing zone accelerator or build your own infrastructure as code (IaC). Accelerators are the faster starting point for most organizations. [1]
3. **Prepare access:** Assign the deployment identity the permissions required by the chosen deployment method at the correct scopes; see below.
4. **Configure the platform:** Define the management-group hierarchy, policy assignments, role assignments, and any shared services you actually need.
5. **Review and deploy:** Review the generated IaC and planned changes, including costs and effects on existing subscriptions. Deploy through the selected accelerator's instructions.
6. **Onboard workloads:** Place subscriptions in the appropriate management groups, configure workload access and budgets, then verify inherited policies and deploy a test workload.

Microsoft's [Azure Migrate platform landing zone workflow][2] generates Terraform and a design document, which you can review and deploy using its generated instructions. It requires an Azure Migrate project and Visual Studio Code with GitHub Copilot Chat. Other accelerators and custom builds have different prerequisites.

## Roles and permissions

Permissions depend on **what is deployed and at which scope**. Microsoft documents these for the Azure Migrate platform landing zone workflow specifically: [2]

| Task | Documented access |
| --- | --- |
| Standard platform deployment | **Contributor** and **User Access Administrator** at the target management group, plus **Contributor** at the target subscription. |
| Initial tenant or subscription bootstrap | **Owner** at the tenant root management group or target management group might temporarily be needed. |
| Creating subscriptions | Billing permissions depend on the agreement; programmatic creation has additional eligibility requirements. [4] |

Do not treat this table as universal: check the selected accelerator's prerequisites and every target scope. Microsoft Entra directory roles and Azure RBAC roles are different; **Global Administrator does not automatically have Azure resource access**. Grant only the access needed, use temporary elevation where possible, and remove bootstrap access afterward. [2][5]

## Configuration and best practices

- **Keep the hierarchy simple:** Group subscriptions by common governance and security needs, not by every team or organizational layer. [3]
- **Set guardrails centrally:** Assign shared Azure Policies at appropriate management-group scopes; check inherited effects before moving existing subscriptions. [1][3]
- **Delegate narrowly:** Assign workload access to groups at subscription or resource-group scope, using least privilege. Keep dev and production access separate. Use Privileged Identity Management for eligible privileged access where appropriate. [5]
- **Use IaC:** Keep hierarchy, policies, roles, and subscription configuration in version control; review planned changes before applying them. [2][4]
- **Standardize onboarding:** Record owners, budgets, networking, and security requirements; automate subscription setup when the number of workloads justifies it. [4]
- **Centralize deliberately:** Add shared networking, monitoring, or other services when they provide a clear operational, governance, or cost benefit—not simply because a reference architecture shows them. [1]

## Sources

Microsoft documentation accessed 18 November 2026. Dates below are the pages' **last-updated metadata**, not necessarily their original publication dates.

1. [What is an Azure landing zone?][1] — updated 16 October 2026.
2. [Generate and deploy a platform landing zone with Azure Migrate][2] — updated 24 September 2026.
3. [Management group design considerations and recommendations][3] — updated 1 October 2026.
4. [Subscription vending][4] — updated 1 October 2026.
5. [Landing zone identity and access management][5] — updated 1 October 2026.

[1]: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/
[2]: https://learn.microsoft.com/en-us/azure/migrate/platform-landing-zone
[3]: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org-management-groups
[4]: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/subscription-vending
[5]: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/identity-access-landing-zones
