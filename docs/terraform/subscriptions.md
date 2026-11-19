# Platform subscriptions

The starter expects subscription IDs for the platform roles defined in `subscription_ids`.

## Supported roles

- `management`
- `connectivity`
- `identity`
- `security`

The upstream default requires valid GUIDs for `management` and `connectivity`. `identity` and `security` can be omitted or supplied later, depending on `required_subscription_keys`.

## How subscriptions are used

The code uses these subscriptions to place shared platform resources and assign subscriptions to management groups:

- Management resources go to the `management` subscription.
- Connectivity resources go to the `connectivity` subscription.
- Identity and security subscriptions are referenced by the generated configuration when provided.

The management group module can also place these subscriptions into the hierarchy. That means this starter can reorganize subscriptions as well as deploy shared services.

## Existing subscriptions

The starter can be adapted to existing subscriptions, but that is not a neutral operation. Before moving an existing subscription under a management group, review:

- Inherited Azure Policies
- Existing Azure role assignments
- Networking assumptions
- Diagnostic and monitoring settings
- Budgets and cost reporting
- Any workload-specific exceptions

## Recommendation

For a full platform landing zone, use dedicated platform subscriptions for `management`, `connectivity`, `identity`, and `security` rather than mixing platform resources into workload subscriptions. That keeps platform responsibilities separate and easier to govern.
