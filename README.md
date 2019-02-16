# Matomo helm chart

Example helm chart for Matomo using bitnami docker image

## Kubernetes secrets

These secrets need to be **manually** created in the right namespace.
To create a secret, you need to be able to connect to the k8s cluster via `kubectl`.

This [guide](https://kubernetes.io/docs/concepts/configuration/secret/#creating-your-own-secrets) is a good reference.

### Commands to create secrets

Modify the values in the yaml files using `base64` encoding.

```bash
#bash
echo -n 'SuperSecretPassword' | base64
U3VwZXJTZWNyZXRQYXNzd29yZA==
```

```yaml
#yaml
apiVersion: v1
kind: Secret
metadata:
  name: matomo-db
type: Opaque
data:
  mariadb-root-password: U3VwZXJTZWNyZXRQYXNzd29yZA==
  mariadb-password: U3VwZXJTZWNyZXRQYXNzd29yZA==
```

```bash
#bash
kubectl create -f secrets/matomo-db.yaml -n YOUR-NAMESPACE
```
