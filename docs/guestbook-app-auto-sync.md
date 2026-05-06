```sh
kubectl apply -f auto-sync/guestbook-app-auto-sync.yaml
# application.argoproj.io/guestbook-app-auto-sync created

argocd app list

argocd app sync argocd/guestbook-app 

kubectl get application -n argocd

```
