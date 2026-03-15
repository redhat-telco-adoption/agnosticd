# redhat_telco_adoption.agnosticd

AgnosticD V2 workload roles for the Red Hat Telco Adoption team, deployed on OpenShift via the Red Hat Demo Platform.

## Overview

This Ansible Collection provides AgnosticD V2 workload roles used to provision workshops, demos, and training content on
the [Red Hat Demo Platform](https://demo.redhat.com). Workloads are deployed onto OpenShift 4.x clusters using the
AgnosticD framework.

**Audience:** Demo Platform operators and content creators.

## Prerequisites

- AgnosticD V2 installed and configured
- OpenShift 4.x cluster accessible via kubeconfig
- Ansible 2.9+
- Required Ansible collections: `kubernetes.core`, `agnosticd.core`

## Collection Information

| Field     | Value                   |
|-----------|-------------------------|
| Namespace | `redhat_telco_adoption` |
| Name      | `agnosticd`             |
| Version   | `1.0.0`                 |
| License   | `GPL-2.0-or-later`      |

## Available Workloads

| Workload Role                                                                                              | Description                                                                                                            |
|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| [`ocp4_workload_ocp_troubleshooting_workshop`](roles/ocp4_workload_ocp_troubleshooting_workshop/README.md) | Deploys the OpenShift Troubleshooting Workshop — per-attendee namespaces with 19 broken lab scenarios across 6 modules |

## Usage with AgnosticD V2

Reference a workload in an AgnosticD V2 config vars file:

```yaml
workloads:
  - redhat_telco_adoption.agnosticd.<workload_name>
```

Then provision with:

```bash
agd provision
```
