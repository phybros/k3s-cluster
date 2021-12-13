# Backups

Handy benji alias:

```
alias benji="k exec -i -n backup-system $(k get po -n backup-system --selector=app.kubernetes.io/component=benji,app.kubernetes.io/instance=benji,app.kubernetes.io/name=benji-k8s -o jsonpath='{.items[0].metadata.name}') -c benji -- benji"
```
