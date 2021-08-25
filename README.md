# Introduction to AKS

## Azure Kubernetes Services

A "big" services that involves issues of:

Infrastructure | Development | DevOps | Security | Monitoring
------ | ------|--------|---------|-----
Public vs Private cluster<br>CNI vs Kubnet<br>Azure vs Calico<br>Ingress<br>Egress<br>DNS Configuration| Docker<br>VS Code Tools<br>Dapr | ADO<br>GitOps | RBAC<br>AAD Integration<br>Private Endpoints<br>Key Vault | Container Insights<br>Prometheus Grafana

## AKS Overview

- [Kubernetes architecture](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#kubernetes-cluster-architecture)
  - Master Node (Free from Microsoft)
    - API
    - Controller
    - ETCD
    - Etc.
  - Worker Node
    - Kubenet
    - Containerd
    - Etc.
- [SLA](https://azure.microsoft.com/en-us/support/legal/sla/kubernetes-service/v1_1/)
  - Service backed by VMs in scale sets
  - 2 VMs (99.9%) or 3 VMs in availability zones (99.95%)
  - [Uptime SLA - higher availability for the management plane](https://docs.microsoft.com/en-us/azure/aks/uptime-sla)
  - [Perform a compound analysis](https://megamorf.gitlab.io/cheat-sheets/calculate-compound-availability/)
- Cost
  - Leverage reserved instances
  - Leverage second billing with ACI bursting
- [Scalabiltiy](https://docs.microsoft.com/en-us/azure/aks/concepts-scale)
  - HPA (K8s construct)
  - Cluster auto-scaler (Azure construct)
  - ACI (bursting) (Azure construct)
- [Networking](https://docs.microsoft.com/en-us/azure/aks/concepts-network)
  - Kubnet
    - Pro: Private IP range to the cluster. Use when you have exhasted your IP space.
    - Con: External services cannot connect directly to PODs.
  - > Azure CNI
    - Pro: PODs get an IP from VNET and can communicate to/from other services on the network
    - CON: Node pre-allocates IPs from the network (30 default but can be configured). A large cluster may require a large network.
  - > Private cluster
    - No management operations allowed for outside the network where the cluster is deployed.
  - Public Cluster
    - With the proper credentials, management operations are allowed from the internet.
  - Egress
    - By default nodes connect to LB and traffic goes out to the internet freely
    - (*)This can be restricted by putting a UDR and FW to egress traffic
  - Ingress
    - Loadbalancer (private or public)
    - Application Gateway Ingress Controller (AGIC) or others (NGINX, Traefik, etc.)
  - Traffic restrictions
    - Use NSGs outside the cluster
    - Use Network policies (Azure or Calico) inside the cluster

## [Cloud architecture](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks/secure-baseline-aks)
  - [Sample Architecture](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks-multi-region/aks-multi-cluster)  
  - Resiliency
  - Consider active-active or active-passive architecture
  - DR strategies
    - Backup and restore from/to the running images
    - Restore from DevOps pipeline

## Container Registry & Key Vault integration

- [Integration with Azure Container Registry](https://docs.microsoft.com/en-us/azure/aks/cluster-container-registry-integration?tabs=azure-cli)
- Integration with Key Vault
  - **Note:** In Kubernetes secrets are 64 based encoded strings. These are not secrets.

## Development

- [DAPR](https://dapr.io/)

## Operating the cluster

- [CKAD Training](https://github.com/johandry/CKAD)

## DevOps

- CI/CI pipelines with Git actions or Azure DevOps
- [Helmp charts](https://helm.sh/)
- > [Gitops](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/gitops-aks/gitops-blueprint-aks)

## Security

- RBAC
- > AAD integration
- > [Recommendations from our team](https://github.com/msalemor/aks-security-recommendations)

## Monitoring

- [Container Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-overview)
- Prometheus/Grafana
- Others

## More advanced topics

- Service Mesh
  - [Open Service Mesh](https://openservicemesh.io/)

