## CI/CD > Kubernetes > ConfigMaps & Secrets

[<- To Kubernetes](./index.md)

---

Kubernetes ConfigMaps and Secrets are Kubernetes resources used to manage configuration settings and sensitive information such as passwords, API keys, and certificates. They provide a way to decouple configuration data from containerized applications, making it easier to manage and update configurations without modifying application code or container images.

### ConfigMaps

ConfigMaps store configuration data in key-value pairs and can be used to inject configuration settings into Pods as environment variables or mounted as files in a volume.

#### Creating ConfigMaps

ConfigMaps can be created using the `kubectl create configmap` command or by providing a YAML/JSON manifest.

Example using `kubectl create configmap`:

```bash
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

Example YAML manifest:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: value1
  key2: value2
```

#### Using ConfigMaps

ConfigMaps can be consumed by Pods in several ways:

1. **Environment Variables**: ConfigMap data can be exposed to Pods as environment variables.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: myimage
    envFrom:
    - configMapRef:
        name: my-config
```

2. **Volume Mounts**: ConfigMap data can be mounted as files in a volume.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: myimage
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
volumes:
- name: config-volume
  configMap:
    name: my-config
```

### Secrets

Secrets are similar to ConfigMaps but are intended for storing sensitive information. Kubernetes stores secrets in a base64-encoded format, but it's important to note that they are not encrypted.

#### Creating Secrets

Secrets can be created using the `kubectl create secret` command or by providing a YAML/JSON manifest.

Example using `kubectl create secret`:

```bash
kubectl create secret generic my-secret --from-literal=username=myuser --from-literal=password=mypassword
```

Example YAML manifest:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: bXl1c2Vy
  password: bXlwYXNzd29yZA==
```

#### Using Secrets

Secrets can be consumed by Pods in a manner similar to ConfigMaps, either as environment variables or mounted volumes.