## CI/CD > Kubernetes > Containers

[<- To Kubernetes](./index.md)

---

The main difference between a Deployment and a Service in Kubernetes lies in their respective purposes and functionalities within the Kubernetes ecosystem:

1. **Deployment**:
   - **Purpose**: A Deployment is a Kubernetes resource used to manage the deployment and scaling of application Pods. It ensures that a specified number of replica Pods are running and maintains the desired state of the application.
   - **Functionality**: Deployments manage the lifecycle of Pods, handling tasks such as creating new Pods, updating existing Pods, rolling out changes with zero-downtime, and scaling the number of Pods based on demand.
   - **Use Cases**: Deployments are typically used to manage stateless applications or microservices that can be horizontally scaled by adding or removing Pods.

2. **Service**:
   - **Purpose**: A Service is a Kubernetes resource used to expose and provide network access to a set of Pods running in the cluster. It enables communication between different parts of an application or external clients.
   - **Functionality**: Services provide a stable endpoint (IP address and port) that abstracts away the dynamic nature of Pods. They route incoming traffic to the appropriate Pods based on labels and selectors, ensuring that requests are load-balanced across the Pod replicas.
   - **Use Cases**: Services are commonly used to expose web applications, APIs, databases, or any other network-accessible components within the Kubernetes cluster. They facilitate service discovery, load balancing, and internal communication between application components.

In summary, while Deployments manage the creation and scaling of application Pods, Services provide networking capabilities to route traffic to those Pods. Deployments focus on the application's runtime environment and lifecycle management, while Services focus on enabling communication and access to application components within the Kubernetes cluster. Together, Deployments and Services play complementary roles in orchestrating and operating containerized applications in Kubernetes. Below is an example of a `deployment.yaml` and `service.yaml` 

### Deployment YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example-app
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

Explanation:
- `apiVersion`: Specifies the Kubernetes API version being used (`apps/v1` for Deployment).
- `kind`: Specifies the type of Kubernetes resource (Deployment).
- `metadata`: Provides metadata about the Deployment, including its name.
- `spec`: Defines the desired state of the Deployment.
  - `replicas`: Specifies the desired number of replica Pods (in this case, 3).
  - `selector`: Defines how the Deployment selects which Pods to manage.
    - `matchLabels`: Specifies that Pods with the label `app: example-app` should be managed by this Deployment.
  - `template`: Specifies the Pod template used to create new Pods.
    - `metadata`: Labels applied to Pods created from this template.
    - `spec`: Defines the specification for the Pod.
      - `containers`: Specifies the containers within the Pod.
        - `name`: Name of the container.
        - `image`: Docker image to use for the container (`nginx:latest` in this example).
        - `ports`: Ports to expose on the container (`80` in this case).

### Service YAML:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: example-service
spec:
  selector:
    app: example-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```

Explanation:
- `apiVersion`: Specifies the Kubernetes API version being used (`v1` for Service).
- `kind`: Specifies the type of Kubernetes resource (Service).
- `metadata`: Provides metadata about the Service, including its name.
- `spec`: Defines the desired state of the Service.
  - `selector`: Specifies the Pods that the Service will route traffic to.
    - `app: example-app`: Selects Pods with the label `app: example-app`.
  - `ports`: Specifies the ports exposed by the Service.
    - `protocol`: Specifies the protocol (`TCP` in this case).
    - `port`: Port exposed by the Service.
    - `targetPort`: Port on the Pods to which traffic will be forwarded.
  - `type`: Specifies the type of Service (`ClusterIP` in this case, which exposes the Service internally within the cluster).

These YAML files define a simple Deployment with three replicas running an Nginx web server and a corresponding Service to expose the Deployment internally within the Kubernetes cluster. From there, you simply use the command line to start up your newly crafted service/deployment using `kubectl`, you would typically follow these steps:

1. **Apply Deployment YAML**: Use the `kubectl apply` command to apply the Deployment YAML file to your Kubernetes cluster. This will create the specified number of Pods based on the Deployment configuration.

```bash
kubectl apply -f deployment.yaml
```

Replace `deployment.yaml` with the path to your actual Deployment YAML file.

2. **Apply Service YAML**: Use the `kubectl apply` command to apply the Service YAML file to your Kubernetes cluster. This will create the Service, which will act as a stable endpoint for accessing your application Pods.

```bash
kubectl apply -f service.yaml
```

Replace `service.yaml` with the path to your actual Service YAML file.

After running these commands, Kubernetes will start the Pods based on the Deployment configuration and expose them using the Service configuration. You can verify the status of the Pods and Services by using `kubectl get pods` and `kubectl get services` commands respectively.

Here's a recap of the commands:

```bash
# Apply Deployment YAML
kubectl apply -f deployment.yaml

# Apply Service YAML
kubectl apply -f service.yaml

# Verify Pods
kubectl get pods

# Verify Services
kubectl get services
```

These commands will help you start the Pods and Services defined in your YAML files and confirm their status within the Kubernetes cluster.