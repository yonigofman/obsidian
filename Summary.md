## Kubernetes (K8s) Summary

Kubernetes (often abbreviated as K8s) is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

### Key Features
- **Automated Rollouts and Rollbacks:** K8s can automatically roll out changes to your application or its configuration and roll back changes if something goes wrong.
- **Service Discovery and Load Balancing:** K8s can expose a container using the DNS name or their own IP address and can load-balance across them.
- **Storage Orchestration:** K8s can automatically mount a storage system of your choice, such as local storage, public cloud providers, and more.
- **Self-Healing:** K8s restarts containers that fail, replaces containers, kills containers that don’t respond to your user-defined health check, and doesn’t advertise them to clients until they are ready to serve.
- **Secret and Configuration Management:** K8s lets you store and manage sensitive information, such as passwords, OAuth tokens, and ssh keys.

### Basic Concepts

| **Concept**          | **Description**                                                                                                                                                                    |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Cluster**          | A set of worker machines, called nodes, that run containerized applications managed by Kubernetes.                                                                                 |
| **Node**             | A single machine in a Kubernetes cluster. Each node runs the Kubernetes runtime, kubelet, and kube-proxy.                                                                          |
| **Pod**              | The smallest and simplest Kubernetes object. A pod represents a single instance of a running process in your cluster and can contain one or more containers.                       |
| **Service**          | An abstraction which defines a logical set of Pods and a policy by which to access them. Services enable loose coupling between dependent Pods.                                     |
| **Deployment**       | Provides declarative updates for Pods and ReplicaSets. You describe the desired state in a Deployment object, and the Deployment Controller changes the actual state to the desired state. |
| **ReplicaSet**       | Ensures that a specified number of pod replicas are running at any given time.                                                                                                      |
| **Namespace**        | Provides a mechanism for isolating groups of resources within a single cluster.                                                                                                    |
| **ConfigMap**        | Provides a way to inject configuration data into Pods.                                                                                                                             |
| **Secret**           | Similar to ConfigMap, but designed to hold sensitive information.                                                                                                                  |
| **Ingress**          | Manages external access to the services in a cluster, typically HTTP.                                                                                                              |
| **Volume**           | Abstracts storage to be used by containers in a pod.                                                                                                                               |

### Kubernetes Architecture

1. **Master Node Components:**
   - **kube-apiserver:** Exposes the Kubernetes API.
   - **etcd:** Key-value store for all cluster data.
   - **kube-scheduler:** Schedules pods to run on nodes.
   - **kube-controller-manager:** Runs controller processes.
   - **cloud-controller-manager:** Interacts with underlying cloud providers.

2. **Worker Node Components:**
   - **kubelet:** Ensures that containers are running in a pod.
   - **kube-proxy:** Maintains network rules and enables communication to pods.
   - **Container Runtime:** Software responsible for running containers (e.g., Docker, containerd).

### Common kubectl Commands Cheat Sheet

| **Command**                             | **Description**                                                |
|-----------------------------------------|----------------------------------------------------------------|
| `kubectl get nodes`                     | List all nodes in the cluster.                                 |
| `kubectl get pods`                      | List all pods in the default namespace.                        |
| `kubectl get pods --all-namespaces`     | List all pods across all namespaces.                           |
| `kubectl get services`                  | List all services in the default namespace.                    |
| `kubectl describe pod [pod_name]`       | Show detailed information about a pod.                         |
| `kubectl logs [pod_name]`               | Print the logs from a container in a pod.                      |
| `kubectl exec -it [pod_name] -- /bin/bash` | Execute a command in a container in a pod (interactive shell). |
| `kubectl apply -f [file.yaml]`          | Apply a configuration to a resource by filename or stdin.      |
| `kubectl delete pod [pod_name]`         | Delete a pod.                                                  |
| `kubectl scale --replicas=[num] deployment/[deployment_name]` | Scale a deployment to a specified number of replicas. |
| `kubectl rollout restart deployment/[deployment_name]` | Restart a deployment.                                    |
| `kubectl create -f [file.yaml]`         | Create resources defined in a file.                            |
| `kubectl get namespaces`                | List all namespaces.                                           |
| `kubectl config view`                   | Show the kubeconfig settings.                                  |

### Useful YAML Snippets

**Pod Definition**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
    ports:
    - containerPort: 80
```

**Service Definition**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

**Deployment Definition**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: MyApp
  template:
    metadata:
      labels:
        app: MyApp
    spec:
      containers:
      - name: my-container
        image: nginx
        ports:
        - containerPort: 80
```


# Service Types

Certainly! Here's a detailed table about the different types of services in Kubernetes:

| **Service Type**    | **Description**                                                                                                                                                                                                                                                                                             | **Use Cases**                                                                                          |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **ClusterIP**       | Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster. It is the default Service type.                                                                                                                                                | Internal communication between services within the same cluster.                                        |
| **NodePort**        | Exposes the Service on each Node's IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created. You’ll be able to contact the NodePort Service from outside the cluster using `<NodeIP>:<NodePort>`.                                            | Exposing a service to external traffic without a load balancer.                                          |
| **LoadBalancer**    | Exposes the Service externally using a cloud provider's load balancer. The cloud provider assigns a fixed, external IP to the service. The LoadBalancer service creates a NodePort and ClusterIP service, and configures the external load balancer to route traffic to the NodePort.                   | Exposing a service to external traffic with automatic load balancing provided by cloud providers.        |
| **ExternalName**    | Maps the Service to the contents of the `externalName` field (e.g., `example.com`). You can use this to return a CNAME record with the external name. Unlike other service types, ExternalName does not define a new IP address. Instead, it returns the CNAME record for the external name.           | Connecting to an external service by a DNS name, useful for integrating external services into a cluster. |
| **Headless Service**| A special type of service that does not have a cluster IP. When creating headless services, you set the cluster IP field to `None`. Kubernetes does not assign a ClusterIP, and DNS queries for the service return the individual IPs of the associated Pods.                                               | Direct pod-to-pod communication, StatefulSets, or for services where you need direct access to the pods. |

### Detailed Explanation

1. **ClusterIP**
    - **Internal Access:** The Service is accessible only within the cluster.
    - **Default Type:** If you do not specify a type, Kubernetes will default to ClusterIP.
    - **Example Use Case:** Microservices within the same application that need to communicate with each other.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-clusterip-service
    spec:
      selector:
        app: MyApp
      ports:
        - protocol: TCP
          port: 80
          targetPort: 9376
    ```

2. **NodePort**
    - **External Access:** The Service is accessible externally on each Node’s IP address at a specified port.
    - **Port Range:** NodePort values must be in the range 30000-32767.
    - **Example Use Case:** Simple, external access to a service without using a cloud provider’s load balancer.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-nodeport-service
    spec:
      type: NodePort
      selector:
        app: MyApp
      ports:
        - protocol: TCP
          port: 80
          targetPort: 9376
          nodePort: 30007
    ```

3. **LoadBalancer**
    - **Cloud Provider Integration:** Relies on the cloud provider to provision an external load balancer.
    - **Automatic Scaling:** Scales traffic to available pods automatically.
    - **Example Use Case:** Web applications that need to be exposed to the internet with high availability.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-loadbalancer-service
    spec:
      type: LoadBalancer
      selector:
        app: MyApp
      ports:
        - protocol: TCP
          port: 80
          targetPort: 9376
    ```

4. **ExternalName**
    - **DNS CNAME Records:** Maps the service to a DNS name by returning a CNAME record.
    - **No Cluster IP:** Does not allocate a cluster IP.
    - **Example Use Case:** Accessing external databases or third-party services by DNS names.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-externalname-service
    spec:
      type: ExternalName
      externalName: example.com
    ```

5. **Headless Service**
    - **Direct Pod Access:** No ClusterIP is assigned, allowing direct access to pods.
    - **StatefulSets:** Often used with StatefulSets for stable network identities.
    - **Example Use Case:** Applications requiring direct access to individual pods for stateful connections.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-headless-service
    spec:
      clusterIP: None
      selector:
        app: MyApp
      ports:
        - protocol: TCP
          port: 80
          targetPort: 9376
    ```
