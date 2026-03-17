# Infrastructure as Code (IaC) Decision Framework

**Purpose**: Help partners choose the right IaC approach for AI Landing Zone deployments  
**Audience**: Solution architects, DevOps engineers, technical consultants  
**Last Updated**: February 25, 2026

---

## 🎯 Quick Decision Guide

```
┌─────────────────────────────────────────────────────────────────────┐
│                    IaC APPROACH DECISION TREE                       │
└─────────────────────────────────────────────────────────────────────┘
                                │
                    Need fastest deployment?
                         (< 1 hour)
                                │
              ┌─────────────────┴────────────────┐
              │                                  │
             YES                                NO
              │                                  │
              ▼                                  │
    ┌─────────────────┐                          │
    │  azd up         │                          │
    │  (Deploy-Your-  │              Does customer have
    │   AI-App repo)  │              multi-cloud strategy?
    └─────────────────┘                          │
                                   ┌─────────────┴────────────┐
                                   │                          │
                                  YES                        NO
                                   │                          │
                                   ▼                          │
                          ┌─────────────────┐                 │
                          │   Terraform     │      Is team Azure-native
                          │                 │      with Bicep experience?
                          └─────────────────┘                 │
                                                ┌─────────────┴─────────────┐
                                                │                           │
                                               YES                         NO
                                                │                           │
                                                ▼                           ▼
                                       ┌─────────────────┐        ┌─────────────────┐
                                       │     Bicep       │        │   Terraform or  │
                                       │                 │        │   Bicep (either)│
                                       └─────────────────┘        └─────────────────┘
```

---

## 📊 Comparison Matrix

| Factor | azd up (Quick Deploy) | Bicep | Terraform | Portal |
|--------|----------------------|-------|-----------|--------|
| **Deployment Time** | ~45 min | ~30-60 min | ~30-60 min | ~30-45 min |
| **Customization** | Limited | Full | Full | Limited |
| **Learning Curve** | Low | Medium | Medium-High | Low |
| **Multi-cloud** | No | No | Yes | No |
| **State Management** | Automatic | ARM backend | Flexible | N/A |
| **CI/CD Integration** | Built-in | Azure DevOps native | GitHub/GitLab/Any | Manual |
| **Modularity** | Fixed | AVM modules | AVM modules | N/A |
| **Drift Detection** | Limited | ARM-based | Built-in | None |
| **Enterprise Support** | MSFT | MSFT | HashiCorp + MSFT | MSFT |
| **Official Repo** | [Deploy-Your-AI-App](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) | [AI-Landing-Zones/bicep](https://github.com/Azure/AI-Landing-Zones/tree/main/bicep) | [AI-Landing-Zones/terraform](https://github.com/Azure/AI-Landing-Zones/tree/main/terraform) | [Deploy to Azure](https://github.com/Azure/AI-Landing-Zones#deploy-to-azure) |

---

## 🔍 Detailed Analysis

### Option 1: Azure Developer CLI (azd up)

**Repository**: [Deploy-Your-AI-Application-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

#### ✅ Choose When:
- Customer needs fastest time-to-value
- Running PoCs or pilots
- Customer wants complete solution (AI Foundry + Fabric + Purview + Search)
- Limited IaC expertise on customer team
- Need for demos and rapid iteration

#### ⚠️ Avoid When:
- Customer requires heavy customization
- Integrating with existing landing zones
- Customer has strict change management processes
- Need granular control over each resource

#### Pros:
- Single command deployment (`azd up`)
- Pre-wired security and networking
- Built-in CI/CD with GitHub Actions
- Comprehensive documentation
- 30+ resources automatically configured

#### Cons:
- Less flexible than raw IaC
- Opinionated architecture
- May deploy resources customer doesn't need
- Requires azd CLI knowledge

#### Prerequisites:
```bash
# Required tools
az --version      # 2.61.0+
azd version       # 1.15.0+

# Clone and deploy
git clone --recurse-submodules https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git
cd Deploy-Your-AI-Application-In-Production
azd up
```

---

### Option 2: Bicep

**Repository**: [Azure/AI-Landing-Zones/bicep](https://github.com/Azure/AI-Landing-Zones/tree/main/bicep)

#### ✅ Choose When:
- Customer is Azure-only (no multi-cloud)
- Team has Azure/ARM experience
- Native Azure DevOps integration needed
- Customer prefers Microsoft-supported tooling
- Need for maximum Azure feature coverage

#### ⚠️ Avoid When:
- Customer has multi-cloud strategy
- Team is invested in Terraform ecosystem
- Customer uses non-Azure CI/CD tools extensively

#### Pros:
- First-class Azure integration
- No state file management (uses ARM)
- Native Azure DevOps support
- Transpiles to ARM (easy debugging)
- AVM (Azure Verified Modules) based
- Type safety and intellisense in VS Code

#### Cons:
- Azure-only (not multi-cloud)
- Steeper learning curve vs azd
- Manual module composition required

#### Sample Deployment:
```bash
# Deploy main template
az deployment sub create \
  --location eastus \
  --template-file main.bicep \
  --parameters main.bicepparam
```

#### Key Files:
```
bicep/
├── main.bicep              # Main orchestration
├── main.bicepparam         # Parameters
├── modules/                # Modular components
│   ├── networking/
│   ├── compute/
│   ├── ai-services/
│   └── security/
└── README.md
```

---

### Option 3: Terraform

**Repository**: [Azure/AI-Landing-Zones/terraform](https://github.com/Azure/AI-Landing-Zones/tree/main/terraform)

#### ✅ Choose When:
- Customer has multi-cloud strategy (Azure + AWS/GCP)
- Team has existing Terraform expertise
- Customer uses Terraform Cloud/Enterprise
- Need for portable IaC skills
- Customer prefers declarative state management

#### ⚠️ Avoid When:
- Customer is Azure-only with no Terraform experience
- Tight Azure DevOps integration is required
- Customer doesn't want to manage state files

#### Pros:
- Multi-cloud capable (reuse skills)
- Strong community and ecosystem
- Built-in drift detection
- Flexible state backends
- AVM (Azure Verified Modules) based
- Mature testing frameworks (Terratest)

#### Cons:
- State file management required
- Azure features may lag behind Bicep
- Additional tooling (Terraform CLI)
- HashiCorp licensing considerations

#### Sample Deployment:
```bash
# Initialize and deploy
terraform init
terraform plan -out=tfplan
terraform apply tfplan
```

#### Key Files:
```
terraform/
├── main.tf                 # Main configuration
├── variables.tf            # Input variables
├── outputs.tf              # Outputs
├── providers.tf            # Provider config
├── modules/                # Reusable modules
└── README.md
```

---

### Option 4: Portal (Deploy to Azure)

**Access**: [Deploy to Azure](https://github.com/Azure/AI-Landing-Zones#deploy-to-azure) button on official repo README

#### ✅ Choose When:
- Customer wants no-code deployment
- Quick demos without CLI setup
- Learning/exploration purposes
- One-time deployments

#### ⚠️ Avoid When:
- Customer needs repeatable deployments
- CI/CD integration required
- Version control and auditing needed

---

## 🎯 Partner Scenario Recommendations

### Scenario: Large SI Customer with Azure Enterprise Agreement

**Recommendation**: **Bicep**

**Why**:
- Azure-native, best Azure feature support
- Integrates with existing Azure DevOps
- No additional licensing (Terraform Enterprise)
- Skills aligned with Microsoft ecosystem

**Alternative**: Terraform if customer already uses it

---

### Scenario: Multi-Cloud Enterprise (Azure + AWS)

**Recommendation**: **Terraform**

**Why**:
- Consistent IaC approach across clouds
- Team skills transfer between clouds
- Unified state management
- Single tool for all infrastructure

---

### Scenario: SMB Customer, First AI Project

**Recommendation**: **azd up (Deploy-Your-AI-App)**

**Why**:
- Fastest to deploy
- Pre-configured best practices
- Minimal IaC expertise needed
- Complete solution out of box
- Can evolve to Bicep/Terraform later

---

### Scenario: Regulated Industry PoC

**Recommendation**: **Bicep** (with security focus)

**Why**:
- Full customization of security controls
- Clear audit trail in ARM
- Easy compliance documentation
- Native Microsoft support

---

### Scenario: ISV Building AI-Powered Product

**Recommendation**: **Terraform**

**Why**:
- Likely deploying to multiple customer environments
- Potentially multi-cloud customers
- Mature testing and validation
- Flexible state management

---

## 🔄 Migration Paths

### From azd → Bicep/Terraform

1. Export deployed resources from Azure
2. Use azd to understand resource relationships
3. Recreate in modular Bicep/Terraform
4. Import existing resources to new IaC

### From Bicep → Terraform (if needed)

1. Document all resources and dependencies
2. Map Bicep resources to Terraform equivalents
3. Use `terraform import` for existing resources
4. Validate parity with original deployment

### From Portal → IaC

1. Export ARM template from Azure Portal
2. Convert ARM to Bicep using `az bicep decompile`
3. Optimize and modularize the Bicep
4. Or convert ARM to Terraform using third-party tools

---

## 🤖 Foundry Agent Environment Setup Options

When deploying AI agent workloads on the Landing Zone, partners must choose the right **Microsoft Foundry setup type**. This decision directly maps to the infrastructure deployed via the IaC options above.

> **Source**: [Foundry Agent Environment Setup](https://learn.microsoft.com/azure/ai-foundry/agents/environment-setup) | [CAF Technology Plan](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)

### Setup Comparison

| Factor | Basic Setup | Standard Setup |
|--------|-------------|----------------|
| **Network Isolation** | None (public endpoints) | Private networking (VNet + Private Endpoints) |
| **Use Case** | Rapid prototyping, PoCs, learning | Production, enterprise, regulated |
| **Data Residency** | Standard Azure region | Full network control, no public egress |
| **Maps to IaC** | azd up (default params) | Bicep/Terraform with full networking modules |
| **Maps to Landing Zone** | Without Platform LZ (minimal) | **With or Without Platform LZ (full security)** |
| **Managed Identity** | Optional | Required |
| **Key Vault Integration** | Optional | Required |
| **Defender for Cloud** | Recommended | Required |

### Decision Guidance

```
┌─────────────────────────────────────────────────────┐
│          FOUNDRY SETUP DECISION                     │
└─────────────────────────────────────────────────────┘
                      │
           Is this production or
           handling sensitive data?
                      │
          ┌───────────┴───────────┐
          │                       │
         YES                     NO
          │                       │
          ▼                       ▼
  ┌───────────────┐      ┌───────────────┐
  │   Standard    │      │    Basic      │
  │   Setup       │      │    Setup      │
  │               │      │               │
  │ = AI Landing  │      │ Quick start,  │
  │   Zone arch   │      │ upgrade later │
  └───────────────┘      └───────────────┘
```

### What Standard Setup Requires (Your Landing Zone Provides)

| Foundry Standard Requirement | Landing Zone Component | IaC Module |
|-----------------------------|----------------------|------------|
| Private networking | VNet + Subnets + NSGs | `modules/networking/` |
| Private Endpoints | PE for all PaaS services | `modules/networking/` |
| Managed Identity | System/User-assigned MI | `modules/security/` |
| AI Search connection | AI Search with private EP | `modules/ai-services/` |
| Cosmos DB for memory | Cosmos DB with private EP | `modules/compute/` |
| Key Vault for secrets | Key Vault with private EP | `modules/security/` |
| Diagnostic settings | Log Analytics + App Insights | `modules/monitoring/` |

**Key partner talking point**: *"When you deploy the AI Landing Zone, you're deploying Foundry's standard enterprise setup. There's no separate infrastructure step for agents — the Landing Zone IS the agent-ready environment."*

### Mapping to IaC Options

- **azd up**: Deploys Standard-equivalent infrastructure by default (private endpoints, managed identity). Best for demos and PoCs.
- **Bicep**: Full control over Foundry standard setup. Use `modules/ai-services/` to customize AI Foundry hub/project configuration. Best for Azure-native production.
- **Terraform**: Same Standard setup with Terraform state management. Use AVM modules for AI Foundry resources. Best for multi-cloud shops.

---

## 📋 Pre-Deployment Checklist

Regardless of IaC choice, verify:

- [ ] **Quota**: Sufficient Azure OpenAI quota in target region
- [ ] **Permissions**: Owner or Contributor + User Access Administrator
- [ ] **Region**: Services available in target region (check [R-R1](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md))
- [ ] **Networking**: Plan for private endpoints and DNS
- [ ] **Identity**: Managed Identity strategy defined
- [ ] **Naming**: Naming convention established
- [ ] **Tags**: Tagging strategy for cost allocation
- [ ] **State** (Terraform only): Backend configured
- [ ] **Pipeline**: CI/CD approach determined

---

## 🛠️ Tooling Requirements

| Tool | azd | Bicep | Terraform |
|------|-----|-------|-----------|
| Azure CLI | 2.61.0+ | 2.61.0+ | 2.61.0+ |
| Azure Developer CLI | 1.15.0+ | - | - |
| Bicep CLI | - | Latest | - |
| Terraform CLI | - | - | 1.5.0+ |
| VS Code Extensions | azd | Bicep | HashiCorp Terraform |

---

## 📚 Learning Resources

### azd
- [Azure Developer CLI Documentation](https://learn.microsoft.com/azure/developer/azure-developer-cli/)
- [Deploy-Your-AI-App Deployment Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/DeploymentGuide.md)

### Bicep
- [Bicep Documentation](https://learn.microsoft.com/azure/azure-resource-manager/bicep/)
- [Azure Verified Modules](https://aka.ms/AVM)
- [Bicep Playground](https://aka.ms/bicepdemo)

### Terraform
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [Azure Verified Modules for Terraform](https://aka.ms/AVM)
- [Terraform Best Practices](https://developer.hashicorp.com/terraform/cloud-docs/recommended-practices)

---

## ❓ FAQ

**Q: Can I mix IaC approaches?**  
A: Not recommended. Pick one approach per environment to avoid state conflicts.

**Q: Which has better Azure feature coverage?**  
A: Bicep typically gets new Azure features first, followed by Terraform.

**Q: Is azd production-ready?**  
A: Yes, but you may want to migrate to Bicep/Terraform for enterprise governance.

**Q: What about Pulumi or other IaC tools?**  
A: The official repos support Bicep and Terraform. Pulumi could work but requires manual translation.

**Q: Can I use ARM templates directly?**  
A: Yes, but Bicep is preferred (ARM replacement). Bicep compiles to ARM.

---

## 📞 Getting Help

| IaC Tool | Support Channel |
|----------|-----------------|
| azd | [Azure Developer CLI Issues](https://github.com/Azure/azure-dev/issues) |
| Bicep | [Bicep Issues](https://github.com/Azure/bicep/issues) |
| Terraform | [AzureRM Provider Issues](https://github.com/hashicorp/terraform-provider-azurerm/issues) |
| AI Landing Zones | [AI-Landing-Zones Issues](https://github.com/Azure/AI-Landing-Zones/issues) |

---

**Next Steps**:
1. Choose your IaC approach based on this framework
2. Review the [Partner Quick Reference Guide](./PARTNER-QUICK-REFERENCE.md) for architecture options
3. Deploy using [Workshop 1](../workshops/01-landing-zone-fundamentals/) for hands-on practice

---

*This framework is maintained by the AI CoE Partner Enablement team.*  
*Feedback? Contact Arturo Quiroga or Anahita Afshari*
