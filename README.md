# Helm Charts Repository

Kubernetes Helm charts for K3s cluster at `tim@10.1.1.50`.

## Charts

```
cert-manager/     Certificate management with Cloudflare DNS-01
caddy/            Caddy ingress controller
```

## Setup Order

### 1. Deploy cert-manager

```bash
ssh tim@10.1.1.50
cd /tmp
git clone https://github.com/schenanigans/schenanigans-helm.git
cd schenanigans-helm

# Add Jetstack repo
helm repo add jetstack https://charts.jetstack.io
helm repo update

# Install cert-manager
sudo helm install cert-manager ./cert-manager -n cert-manager --create-namespace
```

Wait for cert-manager to be ready:
```bash
sudo kubectl get pods -n cert-manager -w
```

### 2. Deploy Caddy

```bash
# Add Caddy repo
helm repo add caddy https://caddyserver.github.io/ingress/
helm repo update

# Install Caddy
sudo helm install caddy ./caddy -n caddy-system --create-namespace
```

### 3. Create Certificate

Example wildcard certificate:
```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: wildcard-cert
  namespace: caddy-system
spec:
  secretName: wildcard-tls
  issuerRef:
    name: letsencrypt-prod
    kind: ClusterIssuer
  dnsNames:
    - "*.example.com"
    - "example.com"
```

Apply:
```bash
sudo kubectl apply -f certificate.yaml
```

### 4. Create Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example
  namespace: default
spec:
  ingressClassName: caddy
  tls:
  - hosts:
    - app.example.com
    secretName: wildcard-tls
  rules:
  - host: app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

## Configuration

Update before deploying:
- `cert-manager/templates/clusterissuer-letsencrypt.yaml` - Change email
- `caddy/values.yaml` - Change email
