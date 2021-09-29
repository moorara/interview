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

### Docker

#### Technologies

  - cgroups
  - namespaces


## Orchestration

### Kubernetes

#### Architecture

#### Resources

  - Pod
  - Deployment
  - Service
  - ConfigMap
  - Secret
  - Ingress


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
 
 ## Services

  - **Compute**
    - Compute Engine
    - Kubernetes Engine
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

