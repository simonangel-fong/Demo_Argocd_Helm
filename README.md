# Demo_Argocd_Helm


```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443


kubectl apply -f guestbook-app.yaml
# application.argoproj.io/guestbook created

argocd app list
# NAME              CLUSTER                         NAMESPACE  PROJECT  STATUS     HEALTH   SYNCPOLICY  CONDITIONS  REPO                                                        PATH            TARGET
# argocd/guestbook  https://kubernetes.default.svc  default    default  OutOfSync  Missing  Manual      <none>      https://github.com/simonangel-fong/argocd-example-apps.git  helm-guestbook  HEAD

argocd app sync argocd/guestbook
# TIMESTAMP                  GROUP        KIND   NAMESPACE                  NAME        STATUS    HEALTH        HOOK  MESSAGE
# 2026-05-05T13:03:09-04:00            Service     default  guestbook-helm-guestbook  OutOfSync  Missing
# 2026-05-05T13:03:09-04:00   apps  Deployment     default  guestbook-helm-guestbook  OutOfSync  Missing
# 2026-05-05T13:03:10-04:00            Service     default  guestbook-helm-guestbook  OutOfSync  Missing              service/guestbook-helm-guestbook created
# 2026-05-05T13:03:10-04:00   apps  Deployment     default  guestbook-helm-guestbook  OutOfSync  Missing              deployment.apps/guestbook-helm-guestbook created

# Name:               argocd/guestbook
# Project:            default
# Server:             https://kubernetes.default.svc
# Namespace:          default
# URL:                https://argocd.example.com/applications/argocd/guestbook
# Source:
# - Repo:             https://github.com/simonangel-fong/argocd-example-apps.git
#   Target:           HEAD
#   Path:             helm-guestbook
# SyncWindow:         Sync Allowed
# Sync Policy:        Manual
# Sync Status:        Synced to HEAD (723b86e)
# Health Status:      Progressing

# Operation:          Sync
# Sync Revision:      723b86e01bea11dcf72316cb172868fcbf05d69e
# Phase:              Succeeded
# Start:              2026-05-05 13:03:09 -0400 EDT
# Finished:           2026-05-05 13:03:09 -0400 EDT
# Duration:           0s
# Message:            successfully synced (all tasks run)

# GROUP  KIND        NAMESPACE  NAME                      STATUS  HEALTH       HOOK  MESSAGE
#        Service     default    guestbook-helm-guestbook  Synced  Healthy            service/guestbook-helm-guestbook created
# apps   Deployment  default    guestbook-helm-guestbook  Synced  Progressing        deployment.apps/guestbook-helm-guestbook created

argocd app get argocd/guestbook
# Name:               argocd/guestbook
# Project:            default
# Server:             https://kubernetes.default.svc
# Namespace:          default
# URL:                https://argocd.example.com/applications/guestbook
# Source:
# - Repo:             https://github.com/simonangel-fong/argocd-example-apps.git
#   Target:           HEAD
#   Path:             helm-guestbook
# SyncWindow:         Sync Allowed
# Sync Policy:        Manual
# Sync Status:        Synced to HEAD (723b86e)
# Health Status:      Healthy

# GROUP  KIND        NAMESPACE  NAME                      STATUS  HEALTH   HOOK  MESSAGE
#        Service     default    guestbook-helm-guestbook  Synced  Healthy        service/guestbook-helm-guestbook created
# apps   Deployment  default    guestbook-helm-guestbook  Synced  Healthy        deployment.apps/guestbook-helm-guestbook created
```

```sh
kubectl apply -f guestbook-app-valuefile.yaml
# application.argoproj.io/guestbook-valuefile created

argocd app list
# NAME                        CLUSTER                         NAMESPACE  PROJECT  STATUS     HEALTH   SYNCPOLICY  CONDITIONS  REPO                                                        PATH            TARGET
# argocd/guestbook            https://kubernetes.default.svc  default    default  Synced     Healthy  Manual      <none>      https://github.com/simonangel-fong/argocd-example-apps.git  helm-guestbook  HEAD
# argocd/guestbook-valuefile  https://kubernetes.default.svc  default    default  OutOfSync  Missing  Manual      <none>      https://github.com/simonangel-fong/argocd-example-apps.git  helm-guestbook  HEAD

argocd app sync argocd/guestbook-valuefile

```

```sh
kubectl apply -f guestbook-app-parameters.yaml
# application.argoproj.io/guestbook-app-parameters created

argocd app list
# NAME                             CLUSTER                         NAMESPACE  PROJECT  STATUS     HEALTH   SYNCPOLICY  CONDITIONS  REPO                                                        PATH            TARGET
# argocd/guestbook-app-parameters  https://kubernetes.default.svc  default    default  OutOfSync  Missing  Manual      <none>      https://github.com/simonangel-fong/argocd-example-apps.git  helm-guestbook  HEAD

argocd app sync argocd/guestbook-app-parameters --replace

kubectl get po
# NAME                                                      READY   STATUS    RESTARTS   AGE
# guestbook-app-parameters-helm-guestbook-78d98bb7b-79msz   1/1     Running   0          32s
# guestbook-app-parameters-helm-guestbook-78d98bb7b-k8pvm   1/1     Running   0          32s
# guestbook-app-parameters-helm-guestbook-78d98bb7b-z5b8j   1/1     Running   0          32s
```