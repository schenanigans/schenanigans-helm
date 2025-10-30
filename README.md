# Helm Charts Repository

Kubernetes Helm charts for Rancher Fleet GitOps on K3s cluster at `tim@10.1.1.50`.

## Structure

```
traefik/          Traefik ingress controller
fleet.yaml        Root Fleet configuration
```

## Workflow

```bash
# Make changes locally
vim traefik/values.yaml

# Commit and push
git add .
git commit -m "Update config"
git push

# Fleet auto-deploys within ~15 seconds
```

## Status

```bash
ssh tim@10.1.1.50
sudo kubectl get gitrepo -n fleet-default
sudo kubectl get bundles -n fleet-default
sudo kubectl get pods -n kube-system
```
