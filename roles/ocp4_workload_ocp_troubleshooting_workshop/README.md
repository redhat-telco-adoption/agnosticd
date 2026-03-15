# ocp4_workload_ocp_troubleshooting_workshop

Workload to deploy the OpenShift Troubleshooting Workshop onto OpenShift 4.
Provisions per-attendee namespaces, HTPasswd identity provider, and 19 broken
lab scenarios covering configuration, storage, security, networking, resources,
and lifecycle failure modes.

## Requirements

- OpenShift 4.x cluster accessible via kubeconfig
- AgnosticD V2 framework installed and configured
- Ansible collections: `kubernetes.core`, `agnosticd.core`
- A default StorageClass must exist on the cluster
- A `gold-storage` StorageClass must **not** exist (enforced by `pre_workload` validation)

## Role Variables

### Configurable Defaults (`defaults/main.yml`)

| Variable                                              | Default                                                                     | Description                                                   |
|-------------------------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------|
| `ocp_username`                                        | `system:admin`                                                              | OpenShift admin username, required by the AgnosticD framework |
| `ocp4_workload_ocp_troubleshooting_workshop_idp_name` | `htpasswd` (inherits from `ocp4_workload_authentication_htpasswd_idp_name`) | HTPasswd identity provider name used in summary reporting     |

### Internal Variables (`vars/main.yml`)

These variables are set internally at runtime and are not intended for external configuration. They are prefixed with
`_` per AgnosticD convention.

| Variable                                              | Description                                                                    |
|-------------------------------------------------------|--------------------------------------------------------------------------------|
| `_ocp4_workload_ocp_troubleshooting_workshop_modules` | List of workshop modules with their names and required namespace access levels |

## Workshop Modules

| Module | Topic         | Labs                                                               |
|--------|---------------|--------------------------------------------------------------------|
| 01     | Configuration | Missing ConfigMap, Missing Secret, Invalid Env                     |
| 02     | Storage       | Missing PVC, PVC Pending, Volume Permissions                       |
| 03     | Security      | RBAC, SCC, Image Pull Secret                                       |
| 04     | Networking    | Selector Mismatch, Route Misconfigured, DNS Failure, NetworkPolicy |
| 05     | Resources     | Insufficient Resources, OOMKilled, Quota Exceeded                  |
| 06     | Lifecycle     | CrashLoopBackOff, Probe Failure, Wrong Image Tag                   |

## Actions Supported

- `provision` — Creates the HTPasswd IDP, per-user namespaces (one per module), resource quotas, LimitRanges, and
  deploys the 19 broken lab scenarios
- `destroy` — Removes all provisioned resources

## Usage with AgnosticD V2

Reference the workload in an AgnosticD V2 config vars file:

```yaml
workloads:
  - redhat_telco_adoption.agnosticd.ocp4_workload_ocp_troubleshooting_workshop

ocp_username: "system:admin"
ocp4_workload_ocp_troubleshooting_workshop_idp_name: "htpasswd"
```

Then provision with:

```bash
agd provision
```

## Dependencies

None

## License

Apache-2.0

## Author Information

Red Hat Demo Platform (demo-platform@redhat.com)
