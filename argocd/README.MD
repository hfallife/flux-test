## Installation
```
- kustomize build argocd | kubectl -n argocd apply -f -
- kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

## Get the password
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Update the password
```
argocd login <ARGOCD_SERVER> # e.g. localhost:8080 or argocd.example.com
argocd account update-password
```

## Open console
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Add cluster to argocd
```
argocd cluster add
```