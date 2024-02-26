## CI/CD > Kubernetes > Stateful Sets

[<- To Kubernetes](./index.md)

---

# Kubernetes StatefulSets

StatefulSets are a Kubernetes resource used to manage stateful applications. Unlike Deployments, which are primarily used for stateless applications, StatefulSets are designed for applications that require stable, unique network identifiers, persistent storage, and ordered deployment and scaling.

### Key Features of StatefulSets

1. **Stable Network Identifiers**: StatefulSets provide stable, unique network identifiers (such as DNS names) for each Pod in the set, allowing applications to discover and communicate with each other consistently.

2. **Ordered Deployment and Scaling**: StatefulSets maintain a stable, predictable ordering when deploying or scaling Pods, ensuring that each Pod is started or stopped in sequence, which is crucial for applications with dependencies or shared state.

3. **Persistent Storage**: StatefulSets support the use of Persistent Volume Claims (PVCs) to provide persistent storage for Pods. This allows stateful applications to store data persistently across Pod restarts or rescheduling.

4. **Headless Services**: StatefulSets can be associated with a headless service, which disables load balancing and allows direct communication with individual Pods. This is useful for applications that require direct Pod-to-Pod communication or for stateful applications that need to maintain consistent identity.

### Creating StatefulSets

StatefulSets are defined using YAML or JSON manifests similar to other Kubernetes resources. The manifest includes specifications for the Pod template, replica count, storage, and other configuration settings.

Example StatefulSet definition:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-statefulset
spec:
  serviceName: my-service
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx
        ports:
        - containerPort: 80
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: standard
      resources:
        requests:
          storage: 1Gi
```

### Scaling StatefulSets

StatefulSets can be scaled up or down using the `kubectl scale` command or by updating the replica count in the StatefulSet manifest. Scaling operations respect the ordering of Pods and ensure that new Pods are started or stopped in sequence.

Example scaling command:

```bash
kubectl scale statefulset my-statefulset --replicas=5
```

### Updating StatefulSets

Updating a StatefulSet involves modifying the StatefulSet manifest to apply changes to Pods. StatefulSets support rolling updates, which update Pods in a controlled, orderly fashion, one at a time.
