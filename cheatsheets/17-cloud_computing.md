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

  - Pod
  - Deployment
  - Service
  - ConfigMap
  - Secret
  - Ingress
  - Namespace

##### Labels

  - Labels are key-value pairs attached to objects.
  - Labels specify identifying attributes of objects.
  - Labels are used to *identify* and *select* objects.
  - They are meaningful and relevant to users, but do not imply any semantics.

##### Annotations

  - Annotations attach arbitrary non-identifying metadata to objects.
  - Annotations can be small or large, structured or unstructured, and can include characters not permitted by labels.

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
