## CI/CD > Kubernetes > Namespaces

[<- To Kubernetes](./index.md)

---

Kubernetes namespaces provide a way to organize and segregate cluster resources. They offer a scope for names and a mechanism to isolate resources within the cluster. This segmentation is beneficial for various reasons, including managing access control, resource allocation, and multi-tenancy support.

### Why Use Namespaces?

1. **Resource Isolation**: Namespaces allow teams or users to work within their dedicated space without interfering with other teams' or users' resources. This isolation helps in preventing conflicts and resource contention.

2. **Access Control**: Kubernetes provides Role-Based Access Control (RBAC), which can be configured at the namespace level. This enables fine-grained access control, allowing administrators to restrict or grant permissions based on namespaces.

3. **Resource Quotas**: Namespace-level resource quotas enable administrators to limit the amount of CPU, memory, storage, and other resources consumed by objects within the namespace. This helps in preventing resource hogging and ensures fair resource distribution.

4. **Multi-Tenancy**: Namespaces facilitate multi-tenancy by allowing multiple teams or projects to share the same cluster while keeping their resources isolated. Each tenant can have its namespace with its own resources and access controls.

### Default Namespaces

Kubernetes clusters come with three default namespaces:

- **default**: This is the namespace where objects are placed if no other namespace is specified.
- **kube-system**: Kubernetes system objects, such as core components like kube-dns, kube-proxy, and others, reside in this namespace.
- **kube-public**: This namespace is publicly accessible and can contain resources that should be visible and readable by all users. However, it's not typically used for user-created resources.

### Creating and Using Custom Namespaces

Custom namespaces can be created using the `kubectl create namespace <namespace-name>` command. Once created, you can use the `kubectl apply -f <resource-definition.yaml>` command to create resources within that namespace.

Example:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

To deploy resources within a specific namespace, you can specify the namespace in the resource manifests:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  namespace: my-namespace
```

### Switching Contexts and Namespace

You can switch between namespaces using the `kubectl config set-context --current --namespace=<namespace-name>` command. This sets the default namespace for subsequent `kubectl` commands.

Example:

```bash
kubectl config set-context --current --namespace=my-namespace
```
