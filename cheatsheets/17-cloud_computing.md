# Cloud Computing

  - **On-demand self-service**
    - No human intervention needed to get resources.
  - **Broad Network Access**
    - Access from anywhere.
  - **Resource Pooling**
    - Provider share resources to customers.
  - **Rapid elasticity**
    - Get more resources quickly as needed.
  - **Measured service**
    - Pay only for what you consume.

## Best Practices

  - **Design for Failure**
    - Fail over gracefully.
    - Avoid single points of failure.
  - **Implement Elasticity**
    - Automate deployment process.
    - Scale cloud resources up, down, out, and in.
    - Scheduled-based proactive scaling vs. event-based proactive scaling.
  - **Loose Coupling**
    - Minimize dependencies between components.
  - **Keep Things Secure**
    - Secure application and data.
    - Manage user access control (UAC).


## Containerization

  - **Container Runtime Interface (CRI)**
    - [containerd](https://containerd.io)
    - [CRI-O](https://cri-o.io)
  - **Open Container Initiative (OCI)**
    - [runc](https://github.com/opencontainers/runc)
    - [crun](https://github.com/containers/crun)
    - [gVisor](https://gvisor.dev)
    - [kata-runtime](https://github.com/kata-containers/runtime)

### Docker

#### Technologies

  - cgroups
  - namespaces


## Orchestration

### Kubernetes

  - Container Orchestration
  - Overlay Networking
  - Service Discovery & Load Balancing
  - Storage Orchestration
  - Automated Rollouts & Rollbacks
  - Automatic Bin Packing
  - Autoscaling & Self-Healing
  - Config & Secret Management

#### Architecture

  - **Control Plane Components**
    - kube-apiserver
    - etcd
    - kube-scheduler
    - kube-controller-manager
    - cloud-controller-manager
  - **Node Components**
    - kubelet
    - kube-proxy
    - container-runtime
  - **Addons**
    - DNS
    - Web UI

#### Concepts

##### Objects

  - **Workloads**
    - [Pod](https://kubernetes.io/docs/concepts/workloads/pods)
    - [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment)
      - [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset)
    - [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset)
      - Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. 
      - Unlike a Deployment, a StatefulSet maintains a *sticky identity* for each of their Pods.
      - The pods are created from the same spec, but are not interchangeable.
      - Each pod has a persistent identifier that it maintains across any rescheduling.
    - [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset)
    - [Job](https://kubernetes.io/docs/concepts/workloads/controllers/job)
    - [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs)
  - **Networking**
    - [Service](https://kubernetes.io/docs/concepts/services-networking/service)
      - [EndpointSlice](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices)
    - [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress)
    - [NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/network-policies)
  - **Storage**
    - [ProjectedVolume](https://kubernetes.io/docs/concepts/storage/projected-volumes)
    - [PersistentVolume](https://kubernetes.io/docs/concepts/storage/persistent-volumes)
    - [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes)
  - **Configuration**
    - [ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap)
    - [Secret](https://kubernetes.io/docs/concepts/configuration/secret)

##### Labels

  - Labels do not provide uniqueness.
  - Labels are key-value pairs attached to objects.
  - Labels specify identifying attributes of objects.
    - They are meaningful and relevant to users, but do not directly imply semantics to the core system.
  - Labels are used to identify, organize, and select subsets of objects.
  - Labels enable users to map their organizational structures onto objects without requiring clients to store these mappings.
  - Valid label keys have two segments: an optional **prefix** and a required **name**, separated by a slash `/`.
    - If the prefix is omitted, the label Key is presumed to be private to the user.
    - Automated system components which add labels to end-user objects must specify a prefix (`kubernetes.io/`, `k8s.io/`).
  - **Label Selectors**
    - *Equality-based* requirement
    - *Set-based* requirement (`in`, `notin`, exist, and not exist `!`)

##### Annotations

  - Annotations attach arbitrary non-identifying metadata to objects.
  - Annotations can be small or large, structured or unstructured, and can include characters not permitted by labels.
    - Note: The keys and the values in the map must be strings.
  - Valid annotation keys have two segments: an optional **prefix** and a required **name**, separated by a slash `/`.
    - The prefix is optional. If specified, the prefix must be a DNS subdomain.

##### Affinity/Anti-affinity

  - Node affinity
    - Node affinity is conceptually similar to *nodeSelector*.
    - Constrain which nodes your pod is eligible to be scheduled on based on labels on the node.
    - Two types:
      - `requiredDuringSchedulingIgnoredDuringExecution`
      - `preferredDuringSchedulingIgnoredDuringExecution`
  - Inter-Pod affinity/anti-affinity
    - Constrain which nodes your pod is eligible to be scheduled based on labels on pods already running on the node.
    - Rule --> This pod should (or should not) run in an X if X is already running one or more pods that meet rule Y.
      - X is a *topology domain* like node, availability zone, region, etc. You express it using a `topologyKey`.
      - Y is expressed as a *LabelSelector* with an optional associated list of namespaces (labels on pods are implicitly namespaced).
    - Two types:
      - `requiredDuringSchedulingIgnoredDuringExecution`
      - `preferredDuringSchedulingIgnoredDuringExecution`

##### Taints and Tolerations**

  - Node affinity is a property of Pods that attracts them to a set of nodes (hard or soft).
  - *Taints* are the opposite! They allow a node to repel a set of pods.
  - *Tolerations* are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints.

#### Commands

  - **config**
  - **pod**
  - **deployment**
  - **service**


## Google Cloud

  - **IaaS**
    - Compute engine
  - **Hybrid**
    - Kubernetes Engine
  - **PaaS**
    - App Engine
  - **Serverless**
    - Cloud Functions
  - **SaaS**
    - Managed services

### Network

  - **Zone**
    - A zone is a deployment area for Google Cloud Resources.
    - A zone does not always correspond to a single physical building.
    - Zones are grouped into regions.
    - *Think of a zone as a single failure domain within a region.*
    - For building a fault tolerant application, you can spread your resources across multiple zones in a region.
  - **Region**
    - Regions are independent geographic areas.
    - All the zones within a region have fast network connectivity among them.
    - You can run resources in different regions too:
      - To bring their applications closer to users around the world.
      - To protect against the loss of an entire region.
   - A few Google Cloud Platform Services support placing resources in a Multi-Region.
 
 ### IAM
 
 Who can do what on which resource:
   - **Who**
     - Google Account
     - Google Group
     - Service Account
       - User-created (custom)
       - Built-in
         - *Default Compute Engine service account*
       - Google APIs service account
   - **Can do what**
   - **On which resource**

**Roles:** a group of permissions
  - **Primitive** roles apply to a project (and all resources in the project)
    - Owner
    - Editor
    - Viewer
    - Billing Admin
  - **Predefined** roles apply to a particular service in a project
  - **Custom** roles can be used for practicing the principle of least privilege
 
 ## Services

  - **Compute**
    - Compute Engine
    - Kubernetes Engine (GKE)
      - Operation:
        - Standard
        - Autopilot
      - Version:
        - Static Channel
        - Release Channels
          - Rapid
          - Regular
          - Stable
      - Availability:
        - Zonal clusters
          - Single-zone clusters
          - Multi-zonal clusters
        - Regional clusters
      - Networking:
        - VPC-native
        - Routes-based
      - Isolation:
        - Public
        - Private
    - App Engine
    - Cloud Functions
  - **Storage**
    - Bigtable
    - Cloud Storage
    - Cloud SQL
    - Cloud Spanner
    - Cloud Datastore
  - **Big Data**
    - Pub/Sub
    - Big Query
    - Data Flow
    - Data Proc
    - Data Lab
  - **Machine Learning**
    - Machine Learning
    - Translate API
    - Vision API
    - Speech API
    - Natural Language API

### Load Balancers

  - **Internal**
    - Regional
      - Internal TCP/UDP Load Balancer (Premium network, Pass-through)
      - Internal HTTP(S) Load Balancer (Premium network, Proxy)
  - **External**
    - Regional
      - External TCP/UDP Network Load Balancer (Premium or Standard network, Pass-through)
      - Regional External HTTP(S) Load Balancer (Standard network, Proxy)
    - Global
      - TCP Proxy Load Balancer (Premium or Standard network, Proxy)
      - SSL Proxy Load balancer (Premium or Standard network, Proxy)
      - Global External HTTP(S) Load Balancer (Premium or Standard network, Proxy)
