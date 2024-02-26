## CI/CD > Kubernetes > Persistent Volumes & Claims

[<- To Kubernetes](./index.md)

---

Kubernetes Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) are used to manage storage in a Kubernetes cluster. They provide a way to abstract underlying storage infrastructure from applications, making it easier to manage storage resources dynamically.

### Persistent Volumes (PVs)

Persistent Volumes represent storage resources in the cluster, such as physical disks, cloud storage volumes, or network storage. PVs are provisioned by administrators and can be dynamically provisioned or statically configured.

#### Provisioning PVs

PVs can be provisioned manually by administrators or dynamically provisioned using storage classes. Storage classes define different types of storage and how they are provisioned.

Example PV definition:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  storageClassName: standard
  hostPath:
    path: /data
```

#### Using PVs

PVs are consumed by Pods through Persistent Volume Claims (PVCs). Pods can request specific storage resources by creating PVCs, which Kubernetes binds to matching PVs.

### Persistent Volume Claims (PVCs)

Persistent Volume Claims are requests for storage resources by Pods. PVCs define storage requirements such as size, access mode, and storage class.

#### Creating PVCs

PVCs can be created by users specifying their storage requirements.

Example PVC definition:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

#### Binding PVCs

When a PVC is created, Kubernetes attempts to bind it to a suitable PV that satisfies the PVC's requirements. If no matching PV is available, Kubernetes dynamically provisions one based on the PVC's storage class.

### Using PVs and PVCs

Once a PVC is bound to a PV, Pods can use the PVC to mount the associated storage.

Example Pod definition using a PVC:

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
    - name: my-pvc
      mountPath: /data
volumes:
- name: my-pvc
  persistentVolumeClaim:
    claimName: my-pvc
```
