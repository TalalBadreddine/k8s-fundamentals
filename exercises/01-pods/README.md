# 01 - Pods

## What is a Pod?
- The smallest deployable unit in Kubernetes
- A Pod wraps one or more containers that share networking and storage
- Every container in a Pod shares the same IP address and port space
- Pods are ephemeral — they are not restarted, they are replaced

## Pod YAML Structure

```yaml
apiVersion: v1          # API version
kind: Pod               # Resource type
metadata:
  name: my-pod          # Pod name
  labels:               # Key-value pairs for organization
    app: my-app
spec:
  containers:           # List of containers
  - name: my-container
    image: nginx:1.27
    ports:
    - containerPort: 80
```

## Demo Commands

```bash
# Create a Pod from YAML
kubectl apply -f nginx-pod.yaml

# List Pods
kubectl get pods
kubectl get pods -o wide

# Describe a Pod (events, status, config)
kubectl describe pod nginx-pod

# View logs
kubectl logs nginx-pod

# Exec into a running container
kubectl exec -it nginx-pod -- /bin/bash

# Delete a Pod
kubectl delete pod nginx-pod
```

## Exercise

1. Apply the `nginx-pod.yaml` file
2. Verify the Pod is running with `kubectl get pods`
3. Use `kubectl describe pod nginx-pod` to inspect it
4. Check the logs with `kubectl logs nginx-pod`
5. Exec into the Pod: `kubectl exec -it nginx-pod -- /bin/bash`
6. Inside the Pod, run: `curl localhost` to see the nginx welcome page
7. Exit and delete the Pod: `kubectl delete pod nginx-pod`
