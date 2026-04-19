# Install Argo CD on Kyma

Use the HA manifest and pin the version.

## 1) Install Argo CD in `argocd`

```powershell
kubectl create namespace argocd
kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/v3.3.6/manifests/ha/install.yaml
```

## 2) Set `server.insecure=true` before exposing Argo CD

```powershell
kubectl apply -f argocd/config/argocd-cmd-params-cm.yaml
kubectl rollout restart deployment argocd-server -n argocd
```

## 3) Get the initial admin password

```powershell
argocd admin initial-password -n argocd
```

## 4) Expose Argo CD on Kyma

```powershell
kubectl apply -f argocd/config/argocd-apirule.yaml
kubectl apply -f argocd/config/argocd-virtualservice.yaml
```

## 5) Apply the root app

```powershell
kubectl apply -f bootstrap/root-app.yaml
```
