# Enterprise 3-Tier Application Architecture on Azure

A reference architecture for designing a **secure, highly available and scalable 3-tier application on Microsoft Azure** using a hub-and-spoke network model.

> **Focus:** Azure networking · Hub-and-spoke · Hybrid connectivity · Security · Identity · Monitoring · Backup

## Architecture

![Azure 3-Tier Application Architecture](https://user-images.githubusercontent.com/99427790/235126768-ed3d720c-8c83-4ed9-853e-883f70e3d9fb.png)

## Design goals

- Network isolation between environments
- Controlled hybrid connectivity to on-premises infrastructure
- Highly available application and identity services
- Centralized security and secrets management
- Centralized monitoring and diagnostics
- Backup and operational recovery
- Clear separation of management, development and production workloads

## Network topology

The design uses a **hub-and-spoke topology**:

- **Management / Hub VNet** hosts shared services and centralized connectivity.
- **Development Spoke** isolates development workloads.
- **Production Spoke** isolates production workloads.
- VNet peering provides controlled communication between the required network boundaries.

This pattern supports separation of concerns and makes centralized security and connectivity services easier to manage.

## Connectivity and security

### Hybrid connectivity

- Azure VPN Gateway provides IPsec connectivity to the on-premises environment.
- A local network gateway represents the on-premises network.
- Azure Bastion provides controlled administrative access to virtual machines without exposing management ports directly to the internet.

### Network controls

- Public and private subnets are separated by workload role.
- Network Security Groups restrict permitted traffic.
- Application Gateway provides Layer 7 HTTP/HTTPS routing.
- Database access is restricted to the application tier.

### Identity and secrets

- Multiple Active Directory domain controllers provide identity-service availability.
- Azure Key Vault stores secrets and certificates rather than application source code.

## Operations

The design includes:

- Log Analytics Workspace for centralized telemetry
- Diagnostic settings for Azure resources
- Metrics and log-based alerts
- Automation for VM update management
- Recovery Services Vault for VM backup and recovery policies
- Storage Accounts for appropriate diagnostics and platform logs

## Engineering considerations

This is an architecture reference rather than a prescriptive production blueprint. The exact topology should be adapted to workload requirements, identity architecture, regulatory requirements, traffic patterns and operational ownership.

Before implementation, validate routing, NSG rules, private connectivity, DNS, application dependencies, backup requirements and Azure service limits.

## Technologies

**Cloud:** Microsoft Azure  
**Networking:** VNet · Hub-and-Spoke · VNet Peering · VPN Gateway · Azure Bastion · Application Gateway  
**Security:** NSG · Azure Key Vault · Identity services  
**Observability:** Azure Monitor · Log Analytics · Diagnostic Settings  
**Operations:** Automation · Recovery Services Vault

## Author

**Vitalis Ibekwe**  
Cloud · Platform · SRE · DevOps Engineer

GitHub: https://github.com/VitalisCode
