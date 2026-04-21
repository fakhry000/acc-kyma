# Required existing secrets

This package assumes these secrets already exist before Argo CD syncs the n8n applications.

## Namespace: n8n-hr
- `n8n-db-secret`
  - `hostname`
  - `port`
  - `dbname`
  - `username`
  - `password`
  - `schema`
- `n8n-redis-secret`
  - `host`
  - `port`
  - `password`
  - `prefix`
- `n8n-app-secrets`
  - `N8N_ENCRYPTION_KEY`
  - `N8N_HOST`
  - `N8N_PORT`
  - `N8N_PROTOCOL`
- `n8n-task-runner-secret`
  - `N8N_RUNNERS_AUTH_TOKEN`

## Namespace: n8n-fi
- `n8n-db-secret`
  - `hostname`
  - `port`
  - `dbname`
  - `username`
  - `password`
  - `schema`
- `n8n-redis-secret`
  - `host`
  - `port`
  - `password`
  - `prefix`
- `n8n-app-secrets`
  - `N8N_ENCRYPTION_KEY`
  - `N8N_HOST`
  - `N8N_PORT`
  - `N8N_PROTOCOL`
- `n8n-task-runner-secret`
  - `N8N_RUNNERS_AUTH_TOKEN`
