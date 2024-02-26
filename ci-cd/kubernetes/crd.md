```markdown
## CI/CD > Kubernetes > Custom Resource Definitions & Operators

[<- To Kubernetes](./index.md)

---

Custom Resource Definitions (CRDs) and Operators are Kubernetes features that enable users to extend the Kubernetes API and automate complex application management tasks.

### Custom Resource Definitions (CRDs)

CRDs allow users to define custom resources with their own schema and semantics, extending the Kubernetes API with application-specific objects. CRDs are used to create custom resources such as databases, message queues, machine learning models, and more.

#### Creating CRDs

CRDs are defined using YAML or JSON manifests and registered with the Kubernetes API server. The manifest specifies the custom resource's group, version, kind, and schema.

Example CRD definition:

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: myresource.mygroup.example.com
spec:
  group: mygroup.example.com
  version: v1
  names:
    kind: MyResource
    singular: myresource
    plural: myresources
  scope: Namespaced
  validation:
    openAPIV3Schema:
      type: object
      properties:
        spec:
          type: object
          properties:
            size:
              type: integer
              minimum: 1
```

### Operators

Operators are Kubernetes controllers that automate application management tasks by watching and reconciling the state of custom resources. Operators use the Kubernetes API to manage the lifecycle of custom resources, handling tasks such as provisioning, configuration, scaling, and monitoring.

#### Creating Operators

Operators are typically developed using Kubernetes client libraries (such as client-go for Go or kubectl for Python) and the controller-runtime framework. Operators watch for changes to custom resources and perform reconciliation to ensure that the desired state matches the observed state.

### Operator Frameworks

There are several operator frameworks available to simplify the development of Kubernetes operators, including:

- **Operator SDK**: Provides tools and libraries to build, test, and package operators.
- **Kubebuilder**: A toolkit for building Kubernetes APIs and controllers using controller-runtime.
- **Operator Framework**: A collection of tools and best practices for building and managing operators.

### Benefits of CRDs and Operators

- **Customization**: CRDs allow users to define custom resources tailored to their application's needs.
- **Automation**: Operators automate complex application management tasks, reducing manual intervention and improving reliability.
- **Extensibility**: CRDs and Operators enable the Kubernetes API to be extended with application-specific functionality, making Kubernetes more versatile and adaptable to diverse workloads.
