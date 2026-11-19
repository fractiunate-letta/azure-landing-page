# Outputs

`outputs.tf` exposes the deployed platform pieces so they can be reviewed or consumed by later automation.

## Connectivity outputs

The starter returns different output sets depending on whether hub-and-spoke or Virtual WAN is enabled:

- Virtual network or virtual hub resource IDs and names
- Firewall resource IDs, names, and IP addresses
- Bastion host resource IDs and DNS names
- Public and private DNS resolver outputs
- Gateway resource IDs and public IP addresses
- Route tables and NAT gateways
- Private DNS zone resource IDs
- Full module output objects

## Configuration output

The `templated_inputs` output returns the assembled configuration, including the templated Virtual WAN hubs. That can help during review because it shows what the starter generated from the `tfvars` example.

## Review value

These outputs are useful for confirming that the selected topology and settings produced the intended resources. They are also the natural integration points for later workload landing zone work that depends on shared networking or DNS.
