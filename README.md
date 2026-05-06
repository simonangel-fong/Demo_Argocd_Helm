# Demo_Argocd_Helm

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Specify Values

- [Default Values](./docs/guestbook-app.md)
- [Specify Value File](./docs/guestbook-app-value-file.md)
- [Define by value object](./docs/guestbook-app-values-object.md)
- [Define by Parameters](./docs/guestbook-app-parameters.md)

## Deploy a public artifect repo

- [Grafana repo](./docs/grafana-app.md)

## Auto Sync

- [auto sync](./docs/guestbook-app-auto-sync.md)
