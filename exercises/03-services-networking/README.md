# 03 - Services & Networking

## Why Pods Need Services
- Pod IPs are ephemeral — they change when Pods are recreated
- A **Service** provides a stable IP and DNS name to reach a set of Pods
- Services use **labels and selectors** to find their target Pods

## Service Types
| Type         | Description                                      |
|--------------|--------------------------------------------------|
| ClusterIP    | Internal only (default). Reachable inside the cluster |
| NodePort     | Exposes on each node's IP at a static port (30000-32767) |
| LoadBalancer | Provisions an external load balancer (cloud only) |

## Demo

```bash
# Create the Deployment and Service
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml

# Check the Service
kubectl get svc

# Port-forward to access locally
kubectl port-forward svc/nginx-service 8080:80

# In another terminal
curl http://localhost:8080
```

## Exercise

1. Apply `nginx-deployment.yaml` to create a Deployment with 3 replicas
2. Apply `nginx-service.yaml` to expose it as a ClusterIP Service
3. Run `kubectl get svc` and note the ClusterIP
4. Use `kubectl port-forward svc/nginx-service 8080:80` to access it
5. Open another terminal and run `curl http://localhost:8080`
6. Try the NodePort variant: apply `nginx-nodeport.yaml`
7. Access it via `http://localhost:<nodePort>`
