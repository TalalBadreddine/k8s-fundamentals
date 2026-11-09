# 02 - Deployments

## Key Concepts
- A **Deployment** manages a **ReplicaSet**, which manages **Pods**
- **ReplicaSet** ensures a desired number of Pod replicas are running
- **Self-healing**: if a Pod dies, the ReplicaSet creates a new one
- **Rolling updates**: update Pods gradually with zero downtime
- **Rollback**: revert to a previous version if something goes wrong

## Demo: Self-Healing

```bash
# Create the Deployment
kubectl apply -f nginx-deployment.yaml

# Watch Pods
kubectl get pods -w

# Delete a Pod and watch it come back
kubectl delete pod <pod-name>
# The ReplicaSet immediately creates a replacement!
```

## Demo: Scaling, Update & Rollback

```bash
# Scale to 5 replicas
kubectl scale deployment nginx-deployment --replicas=5
kubectl get pods

# Update the image (triggers a rolling update)
kubectl set image deployment/nginx-deployment nginx=nginx:1.26
kubectl rollout status deployment/nginx-deployment

# Check rollout history
kubectl rollout history deployment/nginx-deployment

# Rollback to previous version
kubectl rollout undo deployment/nginx-deployment
kubectl rollout status deployment/nginx-deployment
```

## Exercise

1. Apply `nginx-deployment.yaml` (starts with 3 replicas)
2. Verify 3 Pods are running
3. Delete one Pod and observe it being recreated automatically
4. Scale the Deployment to 5 replicas
5. Update the image to `nginx:1.26`
6. Watch the rolling update with `kubectl rollout status`
7. Roll back with `kubectl rollout undo`
8. Confirm Pods are back on the original image with `kubectl describe`
