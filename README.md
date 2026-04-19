# n8n on SAP BTP Kyma with Argo CD

This repository is the GitOps baseline for two isolated n8n instances on SAP BTP Kyma:

- `n8n-hr` in namespace `n8n-hr`
- `n8n-fi` in namespace `n8n-fi`
- shared PostgreSQL already provisioned outside GitOps in namespace `n8n-postgres`
- shared Redis already provisioned outside GitOps in namespace `n8n-redis`
- Argo CD in namespace `argocd`

## Design rules baked into this repo

- one Argo CD root app (`bootstrap/root-app.yaml`)
- latest pinned Argo CD install instructions and app version pinning
- official `n8n-io/n8n-hosting` chart pinned to `v1.2.0`
- n8n image pinned to `2.15.0` stable
- all generated n8n URLs forced to public HTTPS URLs
- no real DB/Redis/host values inside the Argo Application objects
- shared parameters split into separate values files under `config/`
- placeholders for secrets kept in manifest files, not in app manifests
- queue mode with Redis + PostgreSQL
- 2 main / 2 worker / 1 webhook-processor per instance
- separate custom task runner image per instance
- APIRule + VirtualService exposure patterns for Kyma
- `server.insecure=true` included for Argo CD exposure on Kyma

## Repository layout

- `bootstrap/` root app
- `apps/` child Argo CD applications
- `argocd/` Argo CD config and exposure manifests
- `platform/` namespaces managed by GitOps for the app layer only
- `config/` shared values and placeholder secrets/config
- `ingress/` APIRules and VirtualServices
- `images/runners/` custom task runner images
- `.github/workflows/` image build workflow

## Before first sync

1. Install Argo CD manually in namespace `argocd` using `argocd/install/README.md`.
2. Update `bootstrap/root-app.yaml` and every `repoURL` reference to your final Git repository URL.
3. Fill the placeholder values in:
   - `config/common/platform-shared.yaml`
   - `config/instances/n8n-hr.yaml`
   - `config/instances/n8n-fi.yaml`
4. Replace the placeholder secret values under `config/manifests/`.
5. Commit and push.
6. Apply `bootstrap/root-app.yaml` once.

## Notes

- This cleaned version does **not** let Argo CD create, update, or delete your live PostgreSQL or Redis resources.
- Argo CD manages only:
  - Argo CD config/exposure
  - app namespaces (`argocd`, `n8n-hr`, `n8n-fi`)
  - n8n secrets/config placeholders
  - n8n applications
  - APIRules and VirtualServices
- PostgreSQL and Redis stay external to GitOps and are only referenced through the config/secrets you populate.
- For production secret management, swap placeholder Secret manifests with External Secrets or another secret manager.
