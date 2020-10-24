This repository contains manifests to easily create a PV/PVC for Persistent Storage in Kubernetes over EFS.

## Prerequisites

This assumes that you have an EFS Volume provisioned and that your cluster is able to connect to it (via role policy)

## How to

Simply change the filesystem id, access point, aws region and the names of the objects to better suit your deployment in `efs-provisioner.yaml` and ensure the names in `class.yaml` match and *kubectl apply -f k8s-efs-provisioner*

This will launch an `efs-provisioner` pod that acts as a broker between your cluster and EFS and allow your other pods in the same namespace to mount your volume.

## Example Usage

In your app deployment, mount the volume like so:

```yaml
    spec:
      containers:
      ...
      ...
      ...
          volumeMounts:
            - name: efs-pvc
              mountPath: /var/www/html
      volumes:
        - name: efs-pvc
          persistentVolumeClaim:
            claimName: efs
```
