# Helm Charts Repository

Kubernetes Helm charts for K3s cluster at `tim@10.1.1.50`.

## Charts

```
caddy/            Caddy ingress controller with Cloudflare DNS-01
```

## Caddy Setup

1. Create Cloudflare API token at https://dash.cloudflare.com/profile/api-tokens
   - Template: "Edit zone DNS"
   - Permissions: Zone > DNS > Edit, Zone > Zone > Read

2. Create secret on cluster:
```bash
ssh tim@10.1.1.50
sudo kubectl create namespace caddy-system
sudo kubectl create secret generic cloudflare-api-token \
  --from-literal=token='YOUR_CLOUDFLARE_TOKEN' \
  -n caddy-system
```

3. Update email in `caddy/values.yaml`

4. Deploy via Rancher UI or Helm:
```bash
ssh tim@10.1.1.50
cd /path/to/charts
sudo helm install caddy ./caddy -n caddy-system
```
