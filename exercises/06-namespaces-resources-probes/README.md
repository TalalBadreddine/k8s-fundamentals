# 06 - Namespaces, Resources & Probes

## Namespaces
- Logical isolation within a cluster
- Default namespaces: `default`, `kube-system`, `kube-public`
- Use for separating environments (dev/staging) or teams

```bash
# Create a namespace
kubectl create namespace intern-lab

# Run resources in a namespace
kubectl apply -f pod.yaml -n intern-lab

# List Pods in a namespace
kubectl get pods -n intern-lab
```

## Resource Requests & Limits
- **Requests**: minimum guaranteed resources (used for scheduling)
- **Limits**: maximum a container can use (enforced at runtime)
- Without limits, one Pod can starve others

## Probes
| Probe     | Purpose                                           |
|-----------|---------------------------------------------------|
| Liveness  | Is the container alive? If not, restart it         |
| Readiness | Is the container ready to serve traffic?           |

## Demo: Failing Probe Causes Restarts

```bash
kubectl apply -f failing-probe-pod.yaml

# Watch the Pod restart
kubectl get pods -w

# Check events
kubectl describe pod failing-probe-pod
```

## Exercise

1. Create the namespace: `kubectl create namespace intern-lab`
2. Apply `resource-pod.yaml` into `intern-lab` namespace
3. Describe the Pod to see the resource requests/limits
4. Apply `probed-pod.yaml` — it has proper liveness and readiness probes
5. Apply `failing-probe-pod.yaml` — watch it restart due to the failing liveness probe
6. Use `kubectl describe pod failing-probe-pod` to see the probe failure events
