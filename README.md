# Nextcloud Helm Chart

Baseline Helm chart for [Nextcloud](https://nextcloud.com) on Kubernetes. Wraps the [official Nextcloud Helm chart](https://github.com/nextcloud/helm) with **External Secrets**, **HPA**, **PDB**, and a post-install Job for default apps.

## Subcharts

| Subchart | Source | Values prefix | Description |
|----------|--------|---------------|-------------|
| **nextcloud** | [nextcloud/helm](https://github.com/nextcloud/helm) | `nextcloud.*` | App deployment, ingress, external DB/Redis, persistence. |

## Templates

| Template | Purpose |
|----------|---------|
| `externalSecrets.yaml` | Admin, DB, Redis, and SMTP secrets from your ClusterSecretStore |
| `pdb.yaml` | PodDisruptionBudget (minAvailable 1) |
| `hpa.yaml` | HorizontalPodAutoscaler (replicaCount → maxReplicas) |
| `jobs.yaml` | Post-install/upgrade Job to install `defaultApps` |

## Configuration

Override ingress hosts, external PostgreSQL/Redis endpoints, persistence (`existingClaim`), and `externalSecrets.*.itemTitle` for your secret store.

## Install

```bash
helm dependency update .
helm template release . -f values.yaml
```

## Support this project

I build tools to get the best homelab experience I can from what's available and to grow as a programmer along the way. If you'd like to contribute, donations go toward homelab operating costs and subscriptions that keep this tooling maintained. Optional and appreciated.

[![Donate with PayPal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/donate/?business=9RHVW92WMWQNL&no_recurring=0&item_name=Optional+donations+help+support+Expected+Behaviors%E2%80%99+open+source+work.+Thank+you.&currency_code=USD)
