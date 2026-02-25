# AI Landing Zones - Partner Quick Reference Guide

**Purpose**: Curated navigation through official Microsoft AI Landing Zone resources for partners.  
**Audience**: SI and SDC partners, solution architects, and technical consultants  
**Last Updated**: February 25, 2026

---

## 🎯 Start Here

### Understanding How AI Landing Zones Fit in CAF

> **📌 Critical Context for Partners**: Azure AI Landing Zones are **application landing zones** within the broader [Cloud Adoption Framework (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/) architecture. They are NOT a separate type of landing zone—they deploy INTO your customer's existing Azure Landing Zone hierarchy.

| Concept | What It Is | Partner Implication |
|---------|------------|---------------------|
| **Platform Landing Zone** | Shared services (Identity, Connectivity, Management) managed by central IT | Your AI workload will use these services (hub network, firewall, DNS, Bastion) |
| **Application Landing Zone** | Subscription(s) where workloads run | **AI Landing Zone deploys here** |
| **AI Landing Zone** | Application landing zone accelerator for AI workloads | Choose "with platform" or "without platform" architecture |

**Key Decision for Partners:**
- **Customer has existing Azure Landing Zones?** → Use "AI Landing Zone with Platform Landing Zone" architecture
- **Greenfield/PoC/No existing LZ?** → Use "AI Landing Zone without Platform Landing Zone" (standalone)

📚 **CAF References** (skim before customer engagements):
- [What is an Azure Landing Zone?](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/) - Core concepts (5 min read)
- [Platform vs Application Landing Zones](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/#platform-landing-zone-vs-application-landing-zones) - Key distinction
- [AI in Azure Landing Zones](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/#ai-in-azure-landing-zones) - Official positioning
- [Baseline Foundry in Landing Zone](https://learn.microsoft.com/azure/architecture/ai-ml/architecture/baseline-microsoft-foundry-landing-zone) - Detailed reference architecture
- [**CAF AI Agent Adoption**](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) - Plan, govern, build, and manage AI agents (**NEW**)

---

### Quick Navigation

Before diving into details, understand the big picture:

| If You Need To... | Go Here |
|-------------------|---------|
| Understand what AI Landing Zones are | [Official README](https://github.com/Azure/AI-Landing-Zones#readme) |
| See the reference architecture | [Architecture Diagrams](#-reference-architectures) |
| Check design recommendations | [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Deploy quickly | [Deploy Your AI App In Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) |
| Learn what's new | [What's New](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Whats-New.md) || **Plan AI Agent workloads on your LZ** | [**CAF AI Agent Adoption**](#-ai-agent-adoption-guidance-caf) |
---

## 📚 Official Resource Map

### Primary Repositories

| Repository | Purpose | When to Use |
|------------|---------|-------------|
| [Azure/AI-Landing-Zones](https://github.com/Azure/AI-Landing-Zones) | Reference architecture, IaC templates (Bicep/Terraform), design guidance | Foundation for any AI Landing Zone deployment |
| [Deploy-Your-AI-Application-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) | Complete production deployment with Fabric, Purview, AI Foundry | When customer needs end-to-end solution with data governance |
| [Azure/Enterprise-Scale](https://github.com/Azure/Enterprise-Scale) | Platform Landing Zone reference implementation, network topology, governance policies | **For "with platform LZ" deployments** - network, identity, and connectivity design |

### Platform Landing Zone Resources (Network Topology)

> **📌 Don't recreate network topology guidance!** The Enterprise-Scale team maintains comprehensive documentation.

| Resource | What It Covers |
|----------|----------------|
| [Enterprise-Scale Wiki](https://github.com/Azure/Enterprise-Scale/wiki) | All CAF design areas with implementation guidance |
| [Define Azure Network Topology](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/define-an-azure-network-topology) | Hub-spoke vs Virtual WAN decision tree |
| [Network Topology & Connectivity](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/design-area/network-topology-and-connectivity) | Comprehensive connectivity design area |
| [Private Link and DNS at Scale](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/private-link-and-dns-integration-at-scale) | Private endpoint DNS integration patterns |

### Key Documents Quick Links

| Document | What It Covers | Direct Link |
|----------|----------------|-------------|
| Design Checklist | 40+ recommendations across 10 design areas | [View](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| FAQ | Common questions about AI Landing Zones | [View](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-FAQ.md) |
| What's New | Latest updates and changes | [View](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Whats-New.md) |
| Roadmap | Upcoming features and plans | [View](https://aka.ms/ailz/roadmap) |
| Cost Guide | Pricing and cost optimization | Referenced in Design Checklist (CO-R1 to CO-R4) |

---

## 🏗️ Reference Architectures

### Option 1: With Platform Landing Zone (Recommended for Enterprise)

**Best for**: Customers with existing Azure Landing Zones, enterprise-scale deployments

![With Platform Landing Zone](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)

**Key Characteristics**:
- Leverages existing hub-spoke networking
- Uses central Firewall, Bastion, DNS zones from platform
- Integrates with existing identity and governance controls
- Recommended by Microsoft for production workloads

**Official Diagram**: [AI-Landing-Zone-with-platform.png](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)

---

### Option 2: Without Platform Landing Zone (Standalone)

**Best for**: Greenfield deployments, PoCs, smaller organizations without existing landing zones

![Without Platform Landing Zone](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)

**Key Characteristics**:
- Self-contained application landing zone
- Includes own networking, security, and governance
- Faster to deploy for isolated scenarios
- Can be migrated to platform model later

**Official Diagram**: [AI-Landing-Zone-without-platform.png](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)

---

## 📋 Design Areas at a Glance

The Design Checklist covers 10 critical areas. Here's what each includes:

| Design Area | # Recommendations | Key Topics |
|-------------|-------------------|------------|
| **Networking** | N-R1 to N-R9 | DDoS, Bastion, Private Endpoints, NSGs, WAF, APIM, Firewall, DNS, Outbound |
| **Identity** | I-R1 to I-R6 | Managed Identity, MFA/PIM, Entra ID, Conditional Access, RBAC |
| **Security** | S-R1 to S-R5 | Defender for Cloud, Security Baseline, Purview, MITRE/OWASP, Prompt Shields |
| **Monitoring** | M-R1 to M-R6 | Azure Monitor, Alerts, Tracing, Diagnostics, Model Drift |
| **Cost** | CO-R1 to CO-R4 | PTU vs PAYGO, Deployment Types, Auto-shutdown |
| **Data** | D-R1 to D-R3 | Thread Storage, File Storage, Fabric Integration |
| **Governance** | G-R1 to G-R5 | Azure Policy, Regulatory Compliance, Responsible AI, Content Safety, Model Catalog |
| **Reliability** | R-R1 | Multi-region Disaster Recovery |
| **Resource Org** | R-R1 to R-R4 | Region Selection, Quota, Subscription Limits, Multi-project |
| **Compute** | C-R1 | Compute Options (Container Apps, App Service, AKS) |

**Full Checklist**: [AI-Landing-Zones-Design-Checklist.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)

---

## 🚀 Deployment Paths

### Path A: Quick Production Deployment (~45 min)

**Use**: [Deploy-Your-AI-Application-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git

# Deploy everything
azd up
```

**What You Get**:
- 30+ Azure resources pre-configured
- AI Foundry + Fabric + Purview + AI Search
- Private networking by default
- Managed identities and RBAC
- Ready for RAG chat scenarios

**Prerequisites**:
- Azure subscription (Owner or Contributor + UAA)
- Azure CLI 2.61.0+
- Azure Developer CLI 1.15.0+
- Sufficient Azure OpenAI quota

**Documentation**: [Deployment Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/DeploymentGuide.md)

---

### Path B: Custom Bicep Deployment

**Use**: [Azure/AI-Landing-Zones/bicep](https://github.com/Azure/AI-Landing-Zones/tree/main/bicep)

**Best for**: Organizations preferring Azure-native IaC, already using Bicep

**Features**:
- Modular, AVM-based templates
- Full control over parameters
- Easy to customize and extend

---

### Path C: Custom Terraform Deployment

**Use**: [Azure/AI-Landing-Zones/terraform](https://github.com/Azure/AI-Landing-Zones/tree/main/terraform)

**Best for**: Multi-cloud organizations, teams with Terraform expertise

**Features**:
- AVM-based modules
- State management flexibility
- Cross-cloud tooling compatibility

**Documentation**: [Terraform README](https://github.com/Azure/AI-Landing-Zones/blob/main/terraform/README.md)

---

### Path D: Portal Deployment

**Status**: Coming Soon (per official repo)

**Best for**: Quick PoCs, non-IaC deployments, visual learners

---

## 🎯 Partner Engagement Scenarios

### Scenario 1: Enterprise Customer with Existing Azure Landing Zones

**Recommended Path**: Bicep/Terraform + Platform Landing Zone architecture

**Key Considerations**:
- Integrate with existing hub networking
- Use central Firewall and Bastion
- Align with existing governance policies
- Review quota in target regions

**Checklist Focus Areas**: Networking (N-R1 to N-R9), Identity (I-R1 to I-R6)

---

### Scenario 2: Greenfield/PoC Deployment

**Recommended Path**: Deploy-Your-AI-App-In-Production (azd up)

**Key Considerations**:
- Fastest time to value
- Complete solution out of box
- Can evolve to enterprise pattern later
- Validate quota before deployment

**Checklist Focus Areas**: Resource Organization (R-R1 to R-R4), Cost (CO-R1 to CO-R4)

---

### Scenario 3: Regulated Industry (Healthcare, Finance)

**Recommended Path**: Custom Bicep + extensive security review

**Key Considerations**:
- Review all Security recommendations (S-R1 to S-R5)
- Implement Responsible AI controls (G-R3, G-R4)
- Configure Purview for data governance
- Enable all Defender for Cloud features
- No public endpoints

**Checklist Focus Areas**: Security, Governance, Data, Identity

---

### Scenario 4: Cost-Sensitive Deployment

**Recommended Path**: Bicep/Terraform with minimal services

**Key Considerations**:
- Use PAYGO initially, switch to PTU when predictable
- Implement auto-shutdown for non-prod (CO-R4)
- Consider global deployment types for lower cost (CO-R3)
- Right-size compute resources

**Checklist Focus Areas**: Cost (CO-R1 to CO-R4), Compute (C-R1)

---

## 🤖 AI Agent Adoption Guidance (CAF)

> **📌 Key Insight for Partners**: AI Landing Zones provide the *infrastructure*. The [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) guidance covers *what to build on that infrastructure* and how to adopt it. Together they complete the partner conversation: **build the Landing Zone → deploy and govern AI agents on it.**

Microsoft's official AI agent adoption framework follows **4 phases**:

| Phase | What It Covers | Key Partner Value |
|-------|----------------|-------------------|
| **1. Plan for Agents** | Business plan, technology plan, org readiness, data architecture | Helps partners qualify customer use cases *before* deploying infrastructure |
| **2. Govern & Secure Agents** | Responsible AI, governance & security, prepare environment | Extends Landing Zone security (S-R1-5, G-R1-5) with agent-specific controls |
| **3. Build Agents** | Single vs. multi-agent systems, build process | Architecture decisions for what runs on the Landing Zone |
| **4. Manage Agents** | Integration, operations | Connects to GenAIOps (Workshop 3 territory) |

### Agent Decision Tree

Microsoft provides an [AI agent decision tree](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents) that helps partners determine:
1. **Should the customer use agents at all?** (vs. deterministic code or classic RAG)
2. **SaaS or custom build?** (M365 Copilot agents, Dynamics 365 agents vs. Foundry/Copilot Studio)
3. **Single or multi-agent?** (based on security boundaries, team structure, future growth)

> **💡 Partner Tip**: Use this decision tree in discovery conversations. If a customer just needs document Q&A, a classic RAG app (no agent) is simpler, cheaper, and more predictable. Reserve agents for scenarios that require multi-step reasoning, tool orchestration, or adaptive behavior.

### Three Agent Types (Increasing Complexity)

| Agent Type | What It Does | Example Use Case | Landing Zone Implications |
|------------|-------------|-----------------|---------------------------|
| **Productivity Agents** | Retrieve and synthesize information | Internal knowledge management, customer service support | Standard RAG infrastructure (AI Search, Foundry, Cosmos DB) |
| **Action Agents** | Perform specific tasks within workflows | Service ticket creation, system monitoring, data updates | +Action tools, API integrations, Logic Apps / Functions |
| **Automation Agents** | Multi-step processes with minimal oversight | Supply chain optimization, complex approval workflows | +Triggers, orchestration, rigorous governance & testing |

### Technology Build Options

| Platform | Type | Best For |
|----------|------|----------|
| **SaaS Agents** (M365 Copilot, Dynamics, Security Copilot) | Ready-to-use | Immediate value, standard business functions |
| **Microsoft Foundry** | PaaS (pro-code & low/no-code) | Custom agents on AI Landing Zone, deep integration |
| **Microsoft Copilot Studio** | SaaS (low/no-code) | Fast development, business teams, moderate customization |
| **GPUs & Containers** (AKS, Container Apps) | IaaS/PaaS | Custom model hosting, compliance-sensitive workloads |

> **📌 Foundry Setup Note**: Microsoft Foundry offers a *basic setup* (rapid prototyping, no network isolation) and a *standard setup* (enterprise data controls, private networking). The **standard setup with private networking** maps directly to the AI Landing Zone architecture. See [Foundry environment setup](https://learn.microsoft.com/azure/ai-foundry/agents/environment-setup).

### Key CAF AI Agent Resources

| Resource | Link |
|----------|------|
| AI Agent Adoption (overview) | [View](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) |
| Business Plan for AI Agents | [View](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan) |
| Technology Plan for AI Agents | [View](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy) |
| Single Agent vs. Multiple Agents | [View](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents) |
| Process to Build AI Agents | [View](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/build-secure-process) |
| Agent Design Patterns (Azure Architecture Center) | [View](https://learn.microsoft.com/azure/architecture/ai-ml/guide/ai-agent-design-patterns) |

---

## 🔗 Framework Alignment

### Cloud Adoption Framework (CAF)

The AI Landing Zone aligns with:
- [CAF AI Scenario](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/)
- [AI Checklist](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/#ai-checklists)
- [AI Strategy Guidance](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/strategy)
- [AI on Azure Platforms (PaaS)](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/platform/architectures)
- [**CAF AI Agent Adoption**](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) - Plan, govern, build, and manage AI agents

### Well-Architected Framework (WAF)

The AI Landing Zone follows:
- [AI Workloads on Azure](https://learn.microsoft.com/azure/well-architected/ai/)
- Design methodology, principles, and areas for AI workloads

---

## ❓ Common Questions

| Question | Answer |
|----------|--------|
| Can I deploy without Platform Landing Zone? | Yes, use the standalone architecture |
| Is Terraform or Bicep better? | See our [IaC Decision Framework](./IAC-DECISION-FRAMEWORK.md) |
| What Azure regions are supported? | Check quota and service availability per [R-R1](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Can I use this for non-GenAI workloads? | Yes, the architecture supports both generative and non-generative AI |
| Is this production-ready? | Yes, designed for production per Well-Architected Framework |
| What about sovereign clouds? | Designed for Azure Public, but can be adapted |

**More FAQs**: [Official FAQ](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-FAQ.md)

---

## 📞 Getting Help

| Resource | Link |
|----------|------|
| GitHub Issues (AI-Landing-Zones) | [Report Issues](https://github.com/Azure/AI-Landing-Zones/issues) |
| GitHub Issues (Deploy-Your-AI-App) | [Report Issues](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/issues) |
| Discussions | [AI-Landing-Zones Discussions](https://github.com/Azure/AI-Landing-Zones/discussions) |
| Internal (MSFT Partners) | Contact your PSA or AI CoE team |

---

## 📚 Additional Learning

### 🎓 MS Learn Training (Recommended First!)

| Resource | Duration | Description |
|----------|----------|-------------|
| [**AI Center of Excellence Learning Path**](https://learn.microsoft.com/training/paths/ai-center-excellence/) | 1 hr 34 min | Complete learning path covering all 3 modules below |
| [Introduction to AI Center of Excellence](https://learn.microsoft.com/training/modules/intro-ai-center-excellence/) | 29 min | AI adoption planning, governance, roles & responsibilities |
| [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) | 28 min | Landing zone concepts, platform vs workload teams, deployment |
| [Guide AI workload operations](https://learn.microsoft.com/training/modules/guide-ai-operations-center-excellence/) | 37 min | GenAIOps, security, compliance, cost management, monitoring |

> **💡 Partner Tip**: Have your team complete the "Introduction to AI Landing Zones" module before workshops!

### Azure Service Documentation

| Resource | Description |
|----------|-------------|
| [Azure AI Foundry Documentation](https://learn.microsoft.com/azure/ai-foundry/) | Core AI development platform |
| [Microsoft Fabric Documentation](https://learn.microsoft.com/fabric/) | Data foundation |
| [Azure AI Search Documentation](https://learn.microsoft.com/azure/search/) | RAG search backend |
| [Microsoft Purview Documentation](https://learn.microsoft.com/purview/) | Data governance |

---

**Next Steps**:
1. Review the [Partner Engagement Methodology](./PARTNER-ENGAGEMENT-METHODOLOGY.md) for the 3-phase delivery framework
2. Review the [IaC Decision Framework](./IAC-DECISION-FRAMEWORK.md) to choose your deployment approach
3. Complete [Workshop 1: Landing Zone Fundamentals](../workshops/01-landing-zone-fundamentals/) for hands-on learning
4. Use the Design Checklist with your customer

---

*This guide is maintained by the AI CoE Partner Enablement team.*  
*Feedback? Contact Arturo Quiroga or Anahita Afshari*
