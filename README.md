Purpose of the Repository: Clearly state that this repository contains Terraform code to provision an AKS cluster with a 3-tier microservice Blue/Green deployment strategy on Azure, utilizing a single node pool for cost optimization within the free tier.
Prerequisites: List any necessary tools (Terraform CLI, Azure CLI, kubectl) and Azure account setup.
Architecture: Include the diagram above (or a more visually appealing version if you create one using other tools). Explain the components and how they interact.
Deployment Steps: Detail the steps to deploy the infrastructure using Terraform.
Blue/Green Implementation: Explain how the Blue/Green deployment is achieved (e.g., deploying to separate namespaces, using service selectors, and how traffic switching is handled by the Load Balancer/Application Gateway).
Considerations for Single Node Pool: Highlight the implications of using a single node pool (resource sharing, isolation levels).
Cost Optimization: Emphasize that this approach is tailored for the Azure Free Account and might require adjustments for production environments.
Future Enhancements (Optional): You could mention potential future improvements, such as using separate node pools for better isolation in a production setting.


+--------------------------+      +---------------------------+
| Azure DevOps (ADO)       |----->| Terraform Infrastructure  |
| (Pipelines)              |      | (AKS Cluster, Load Balancer,|
+--------------------------+      | Network, etc.)            |
                                 +---------------------------+
                                            ^
                                            | Deploys
                                            |
+-----------------------------------------------------------------+
|                     Azure Kubernetes Service (AKS)              |
| (Single Node Pool)                                              |
+-----------------------------------------------------------------+
|                                                                 |
|   +-----------------+     +-----------------+                   |
|   | Namespace: dev  |     | Namespace: dev  |                   |
|   |                 |     |                 |                   |
|   |   +---------+   |     |   +---------+   |                   |
|   |   | Pod 1   |   |     |   | Pod A   |   |                   |
|   |   +---------+   |     |   +---------+   |                   |
|   |   | Pod 2   |   |     |   | Pod B   |   |                   |
|   |   +---------+   |     |   +---------+   |                   |
|   |   | Service:  |--+---->|   | Service:  |                   |
|   |   | blue-svc|   |     |   | green-svc |                   |
|   |   +---------+   |     |   +---------+   |                   |
|   +-----------------+     +-----------------+                   |
|                                                                 |
+-----------------------------------------------------------------+
=
