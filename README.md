# Introduction to AKS

## Azure Kubernetes Services

A "big" services that involves issues of:

- Infrastructure
- Development
- DevOps
- Operating the cluster
- Monitoring

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
- [SLA](https://azure.microsoft.com/en-us/support/legal/sla/kubernetes-service/v1_1/) & [cloud architecture](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks/secure-baseline-aks)
  - Backed by Scalesets
  - 2 VMs (99.9) or 3 VMs in availability zone (99.95%)
  - [Uptime SLA - higher availability for the management plane](https://docs.microsoft.com/en-us/azure/aks/uptime-sla)
  - Perform a compound analysis
  - Resiliency, High availability, DR
- [Scalabiltiy](https://docs.microsoft.com/en-us/azure/aks/concepts-scale)
  - HPA
  - Cluster auto-scaler
  - ACI (bursting)
- [Networking](https://docs.microsoft.com/en-us/azure/aks/concepts-network)
  - Kubnet
    - Pro: Private IP range to the cluster. Use when you have exhasted your IP space.
    - Con: External services cannot connect directly to PODs.
  - > Azure CNI
    - Pro: PODs get an IP from VNET and can communicate to/from other services on the network
    - CON: Node pre-allocates IPs from the network (30 default but can be configured). A large cluster may require a large network.
  - > Private cluster
    - Cannot execute kubelet cmds outside the network
  - public clustering 
    - Can execute kubelet cmds from the internet
  - Egress
    - By default nodes connect to LB and traffic goes out to the internet freely
    - (*)This can be restricted by putting a UDR and FW to egress traffic
  - Ingress
    - Loadbalancer
    - AGIC or others (NGINX)
  - Network policies

## Container Registry & Key Vault integration

- Integration with ACR and Docker Hub
- Integration with Key Vault
  - **Note:** In Kubernetes secrets are 64 based encoded strings. They are not secrets.

## Development

- DAPR

## Operating the cluster

- [CKAD Training](https://github.com/johandry/CKAD)

## DevOps

- CI/CI pipelines with Git actions or Azure DevOps
- [Helmp charts](https://helm.sh/)
- [(*) Gitops](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/gitops-aks/gitops-blueprint-aks)

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

