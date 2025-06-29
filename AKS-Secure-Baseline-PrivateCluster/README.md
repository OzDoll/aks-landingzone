# AKS Secure Baseline with Private Cluster

A deployment of AKS-hosted workloads typically requires a separation of duties and lifecycle management in different areas, such as prerequisites, the host network, the cluster infrastructure, the shared services and finally the workload itself. This reference implementation is no different. Also, be aware that our primary purpose is to illustrate the topology and decisions involved in the deployment of an AKS cluster. We feel a "step-by-step" flow will help you learn the pieces of the solution and will give you insight into the relationship between them. Ultimately, lifecycle/SDLC management of your cluster and its dependencies will depend on your situation (organizational structures, standards, processes and tools), and will be implemented as appropriate for your needs.
Deploy this scenario using the button below.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#view/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAKS-Landing-Zone-Accelerator%2Fmain%2FScenarios%2FAKS-Secure-Baseline-PrivateCluster%2FBicep%2FAll-in-One-Bicep%2Fmain.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAKS-Landing-Zone-Accelerator%2Fmain%2FScenarios%2FAKS-Secure-Baseline-PrivateCluster%2FBicep%2FAll-in-One-Bicep%2Fmain.portal.ui.json)

There are various ways to secure your AKS cluster. From a network security perspective, these can be classified into securing the control plane and securing the workload. When it comes to securing the control plane, one of the best ways to do that is by using a private cluster, where the control plane or API server has internal IP addresses that are defined in the [RFC1918 - Address Allocation for Private Internet](https://datatracker.ietf.org/doc/html/rfc1918) document. By using a private cluster, you can ensure network traffic between your API server and your node pools remains on the private network only. For more details about private clusters, check out the [documentation](https://learn.microsoft.com/azure/aks/private-clusters).

When using a private cluster, the control plane can only be accessed from computers in the private network or peered networks. For this reason, in this reference implementation, we will be deploying a virtual machine in the Hub network through which we can connect to the control plane.

By the end of this, you would have deployed a secure AKS cluster, compliant with AKS Landing Zone Accelerator guidance and best practices.

For this scenario, we have various IaC technology that you can choose from depending on your preference. At this time only the Terraform and Bicep versions are available. Below is an architectural diagram of this scenario.

![Architectural diagram for the secure baseline scenario.](./media/AKS-private-cluster-scenario.jpg)

## Core architecture components
* AKS Private Cluster
* Azure Virtual Networks (hub-spoke)
  * Azure Firewall managed egress
* Azure Application Gateway (WAF)
* Application Gateway Ingress Controller
* AKS-managed Internal Load Balancer
* Azure CNI
* Azure Keyvault
* Azure Container registry
* Azure Bastion
* Azure Monitor for containers
* Azure firewall
* MongoDB 
* Helm
* [Secret store CSI driver](https://learn.microsoft.com/azure/aks/csi-secrets-store-driver)
* [Azure RBAC for Kubernetes Authorization](https://learn.microsoft.com/azure/aks/manage-azure-rbac)
* [Microsoft Entra pod-managed identities](https://learn.microsoft.com/azure/aks/use-azure-ad-pod-identity)

## Next
Pick one of the IaC options below and follow the instructions to deploy the AKS reference implementation.

:arrow_forward: [Bicep](./Bicep)
