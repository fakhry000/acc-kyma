# Final check notes

## Fixed in this checked package
- `bootstrap/root-app.yaml` uses `project: default` so first bootstrap does not fail before `n8n-platform` exists.
- Argo CD public exposure is included.
- HR and FI APIRule + VirtualService are included.
- HR and FI Argo CD applications are included.
- Task runner configuration is included for both instances.
- DB secret mapping includes `schema`.
- Redis secret mapping uses `host`, `port`, `password`, `prefix`.

## Important limitation from the official chart
The official n8n chart documents secret references for:
- core n8n secret (`secretRefs.existingSecret`)
- database password secret
- redis password secret

The chart models the remaining DB/Redis connection settings as values. Because of that, this package still keeps non-password connection fields in values so the chart remains deployable.

Passwords are still sourced from existing Kubernetes secrets.

## Before first sync
Make sure these secrets already exist in both namespaces:
- `n8n-db-secret`
- `n8n-redis-secret`
- `n8n-app-secrets`
- `n8n-task-runner-secret`
