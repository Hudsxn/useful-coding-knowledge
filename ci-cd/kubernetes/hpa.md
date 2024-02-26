```markdown
## CI/CD > Kubernetes > Horizontal Pod Autoscaling (HPA)

[<- To Kubernetes](./index.md)

---

Horizontal Pod Autoscaling (HPA) is a Kubernetes feature that automatically adjusts the number of replica Pods in a Deployment, ReplicaSet, or StatefulSet based on observed CPU utilization or custom metrics.

### How HPA Works

HPA continuously monitors the CPU utilization or custom metrics of Pods in the target resource (Deployment, ReplicaSet, or StatefulSet) and adjusts the number of replica Pods to maintain the specified target CPU utilization or metric value.

1. **Metrics Collection**: HPA collects metrics from Pods using the Metrics Server or custom metric providers.

2. **Evaluation**: HPA evaluates the collected metrics against the specified target value and calculates the desired number of replica Pods required to meet the target.

3. **Scaling**: HPA adjusts the number of replica Pods up or down to match the desired number, ensuring that the target CPU utilization or metric value is maintained.

### Creating Horizontal Pod Autoscalers

Horizontal Pod Autoscalers are defined using YAML or JSON manifests and are associated with the target Deployment, ReplicaSet, or StatefulSet. The manifest specifies the target resource, target CPU utilization or custom metric, and scaling behavior.

Example HPA definition:

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: my-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      targetAverageUtilization: 50
```

### Scaling Behavior

- **MinReplicas**: Specifies the minimum number of replica Pods that should be maintained, even if the target CPU utilization or metric value is low.
- **MaxReplicas**: Specifies the maximum number of replica Pods that can be scaled up to, even if the target CPU utilization or metric value is high.

### Custom Metrics

In addition to CPU utilization, HPA supports scaling based on custom metrics using External Metrics APIs or Custom Metrics APIs. Custom metrics allow users to scale based on application-specific metrics such as request latency, queue length, or custom business metrics.
