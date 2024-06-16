Setting up MongoDB on Kubernetes using a StatefulSet and a StorageClass involves several steps. This process ensures that MongoDB pods maintain stable network identities and persistent storage across rescheduling. Below is a step-by-step guide:

### Prerequisites

1. **Kubernetes Cluster:** Ensure you have a running Kubernetes cluster.
2. **kubectl:** Command-line tool for interacting with the cluster.
3. **Storage Provisioner:** Ensure your cluster has a dynamic storage provisioner like AWS EBS, GCE PD, or any other CSI driver.

### Steps to Set Up MongoDB with StatefulSet and StorageClass

1. **Create a StorageClass:**

   First, define a `StorageClass` that will dynamically provision PersistentVolumes (PVs) for MongoDB.

   ```yaml
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: mongodb-storage
   provisioner: kubernetes.io/aws-ebs  # Change this based on your cloud provider
   parameters:
     type: gp2  # EBS volume type, change as per your need
   ```

   Apply this configuration:

   ```bash
   kubectl apply -f storageclass.yaml
   ```

2. **Create a Headless Service:**

   A headless service is required to manage the network identity of the StatefulSet.

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: mongodb
     labels:
       app: mongodb
   spec:
     ports:
     - port: 27017
       name: mongo
     clusterIP: None
     selector:
       app: mongodb
   ```

   Apply this configuration:

   ```bash
   kubectl apply -f mongodb-service.yaml
   ```

3. **Create a StatefulSet:**

   Define the StatefulSet to manage MongoDB pods.

   ```yaml
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: mongodb
   spec:
     serviceName: "mongodb"
     replicas: 3
     selector:
       matchLabels:
         app: mongodb
     template:
       metadata:
         labels:
           app: mongodb
       spec:
         containers:
         - name: mongo
           image: mongo:4.4  # Specify the MongoDB image version
           ports:
           - containerPort: 27017
             name: mongo
           volumeMounts:
           - name: mongo-persistent-storage
             mountPath: /data/db
     volumeClaimTemplates:
     - metadata:
         name: mongo-persistent-storage
       spec:
         accessModes: [ "ReadWriteOnce" ]
         storageClassName: "mongodb-storage"
         resources:
           requests:
             storage: 10Gi  # Size of the persistent volume
   ```

   Apply this configuration:

   ```bash
   kubectl apply -f mongodb-statefulset.yaml
   ```

4. **Verify the Setup:**

   Check the status of your StatefulSet and the created PersistentVolumeClaims (PVCs):

   ```bash
   kubectl get statefulsets
   kubectl get pods -l app=mongodb
   kubectl get pvc -l app=mongodb
   ```

### Summary

1. **StorageClass:** Defines how storage is provisioned.
2. **Headless Service:** Manages network identity for StatefulSet.
3. **StatefulSet:** Manages the deployment and scaling of MongoDB pods with persistent storage.

This setup ensures that MongoDB instances maintain stable network identities and persistent storage, crucial for database operations and high availability. You can adjust the configurations based on your specific requirements, such as the number of replicas, storage size, and MongoDB version.