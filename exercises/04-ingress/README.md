# 04 - Ingress & Ingress Controller

## Why Services Alone Aren't Enough
- NodePort wastes ports and exposes random high ports
- LoadBalancer creates one LB per Service (expensive)
- **Ingress** gives you HTTP routing (host/path-based) behind a single entry point

## Ingress vs Ingress Controller
- **Ingress** = the routing rules (a Kubernetes resource)
- **Ingress Controller** = the component that reads Ingress rules and configures a reverse proxy (e.g., NGINX Ingress Controller, Traefik)

## Key Features
- **Host-based routing**: `app1.example.com` -> Service A, `app2.example.com` -> Service B
- **Path-based routing**: `/app1` -> Service A, `/app2` -> Service B
- **TLS termination**: attach a certificate for HTTPS

## Demo: Route Two Apps by Path

```bash
# Install NGINX Ingress Controller (if not already installed)
# For minikube: minikube addons enable ingress
# For kind: kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

# Deploy both apps and their services
kubectl apply -f app1.yaml
kubectl apply -f app2.yaml

# Create the Ingress
kubectl apply -f ingress.yaml

# Check Ingress
kubectl get ingress

# Test (adjust based on your setup)
curl http://localhost/app1
curl http://localhost/app2
```

## Exercise

1. Apply `app1.yaml` and `app2.yaml` (two simple nginx deployments with different content)
2. Apply `ingress.yaml` to route `/app1` and `/app2` to the correct Services
3. Verify with `kubectl get ingress`
4. Test the routes using curl or your browser
