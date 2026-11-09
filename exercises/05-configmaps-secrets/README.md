# 05 - ConfigMaps & Secrets

## Separating Config from Code
- **ConfigMaps** store non-sensitive configuration (feature flags, URLs, config files)
- **Secrets** store sensitive data (passwords, API keys, tokens) — base64-encoded
- Both can be injected as **environment variables** or **mounted as files**

## Env Vars vs Mounted Files
| Method     | Use Case                          |
|------------|-----------------------------------|
| Env vars   | Simple key-value pairs            |
| File mount | Config files, certificates, etc.  |

## Demo: Inject a ConfigMap

```bash
# Create ConfigMap and Pod
kubectl apply -f configmap.yaml
kubectl apply -f pod-with-config.yaml

# Verify env vars
kubectl exec configmap-pod -- env | grep APP_

# Verify mounted file
kubectl exec configmap-pod -- cat /etc/config/app.properties
```

## Exercise

1. Apply `configmap.yaml` and `pod-with-config.yaml`
2. Exec into the Pod and verify the environment variables are set
3. Check the mounted config file at `/etc/config/app.properties`
4. Now apply `secret.yaml` and `pod-with-secret.yaml`
5. Exec into the Pod and read the secret: `echo $DB_PASSWORD`
6. Also check the mounted secret file: `cat /etc/secret/password`
