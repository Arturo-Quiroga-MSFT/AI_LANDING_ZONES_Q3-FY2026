# Workshop 2: From RAG to Agents — Deploying Your First Gen AI Workload

**Duration**: 3-4 hours (hands-on)  
**Level**: 300 (Advanced/Hands-On)  
**Lead**: Arturo Quiroga (PSA)  
**Reviewer**: Anahita Afshari (PSA)

---

## 🎯 Workshop Overview

This hands-on workshop takes partners from infrastructure to workload. Participants deploy a complete AI Landing Zone, stand up a RAG chat application, and explore when and how to graduate from classic RAG to AI agents using Microsoft Foundry. The narrative arc follows the real partner delivery journey: **deploy the foundation → build the workload → understand what's next**.

### 📌 Key Concept

> **The Landing Zone is the foundation. The workload is what delivers value.**
>
> Workshop 1 covered *what* an AI Landing Zone is and *why* it matters. This workshop covers *how* to deploy one and *what to build on it*.
>
> The key distinction partners must internalize:
> - **Classic RAG**: Deterministic retrieval — predictable, cheaper, well-understood. Start here.
> - **AI Agents**: Adaptive reasoning — multi-step orchestration, tool use, nondeterministic. Graduate here when the use case demands it.
>
> 📚 Pre-read: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) | [Technology Plan for AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)

---

## 👥 Target Audience

- Partner solution architects with Azure experience
- Technical consultants doing hands-on deployments
- DevOps/platform engineers building AI infrastructure
- Pre-sales engineers who need demo capability

---

## 📚 Prerequisites

### Required Knowledge
- **Completed Workshop 1** or equivalent understanding of AI Landing Zones
- Azure fundamentals (networking, RBAC, resource groups, subscriptions)
- Basic IaC concepts (Bicep or Terraform — at least conceptual understanding)
- Familiarity with Azure AI Foundry (basic awareness)

### Required Access
- Azure subscription with **Owner** or **Contributor + User Access Administrator** role
- Azure CLI 2.61.0+ installed
- Azure Developer CLI (azd) 1.15.0+ installed
- Git installed
- GitHub access
- **Sufficient Azure OpenAI quota** in target region (check before workshop!)

### Recommended Preparation (Pre-Work)
- **🎓 Complete MS Learn Module** (28 min): [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) ⭐ *Required if skipping Workshop 1*
- **Optional** (37 min): [Guide AI Workload Operations](https://learn.microsoft.com/training/modules/guide-ai-operations-center-excellence/)
- Review the [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)
- Skim the [Deploy-Your-AI-App Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md)
- Review [Required Roles & Scopes](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md)

### Environment Setup (Do Before Workshop!)
```bash
# Verify Azure CLI
az --version  # Need 2.61.0+

# Verify Azure Developer CLI
azd version  # Need 1.15.0+

# Login
az login
azd auth login

# Verify quota (replace with your target region)
az cognitiveservices usage list --location eastus2 -o table
```

---

## 🗂️ Workshop Materials

| Material | Description | Location |
|----------|-------------|----------|
| Workshop Guide | Step-by-step facilitation guide | [WORKSHOP-GUIDE.md](./WORKSHOP-GUIDE.md) |
| Slide Deck Outline | Presentation structure | [SLIDE-OUTLINE.md](./SLIDE-OUTLINE.md) |
| Lab Exercises | Hands-on deployment steps | [EXERCISES.md](./EXERCISES.md) *(TODO)* |
| Design Checklist | Official Microsoft resource | [GitHub](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Deploy-Your-AI-App | Primary lab repository | [GitHub](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) |

---

## 📋 Learning Objectives

By the end of this workshop, participants will be able to:

1. **Deploy** a complete AI Landing Zone using `azd up`
2. **Configure** AI Foundry Service with standard (private networking) setup
3. **Deploy** a sample RAG chat application end-to-end
4. **Distinguish** between classic RAG and AI agent workloads in practice
5. **Explore** Microsoft Foundry agent capabilities (declarative & hosted agents)
6. **Implement** basic monitoring and observability for AI workloads
7. **Assess** when a customer should graduate from RAG to agents

---

## ⏱️ Agenda

| Time | Duration | Module | Description |
|------|----------|--------|-------------|
| 0:00 | 15 min | **Welcome & Setup Validation** | Verify prerequisites, intro, agenda |
| 0:15 | 20 min | **Module 1: Quick Recap & Deployment Strategy** | Workshop 1 recap, deployment path selection, lab overview |
| 0:35 | 60 min | **Module 2: Deploy the Landing Zone** | Hands-on: `azd up`, resource walkthrough, validation |
| 1:35 | 15 min | **Break** | |
| 1:50 | 40 min | **Module 3: Configure & Deploy RAG Application** | AI Foundry setup, data ingestion, chat app deployment |
| 2:30 | 30 min | **Module 4: From RAG to Agents** | RAG vs. Agents in practice, Foundry agent exploration, decision framework |
| 3:00 | 20 min | **Module 5: Monitoring & Observability** | Azure Monitor, AI Foundry tracing, operational baseline |
| 3:20 | 15 min | **Module 6: Wrap-up & Next Steps** | Clean-up, Q&A, Workshop 3 preview |
| 3:35 | 10 min | **Buffer / Extended Q&A** | Overflow time |

---

## 📦 Module Summaries

### Module 1: Quick Recap & Deployment Strategy (20 min)

**Key Topics**:
- 5-minute recap of Workshop 1 essentials (LZ concept, 2 architectures, Design Checklist)
- Why we're using `azd up` for this lab (speed, completeness, production-ready)
- What gets deployed: 30+ Azure resources overview
- Lab architecture preview: "without platform LZ" for simplicity
- RAG → Agents narrative: what we'll build and where we're heading

**Key Resources**:
- [Partner Quick Reference](../../docs/PARTNER-QUICK-REFERENCE.md)
- [Deploy-Your-AI-App Architecture Overview](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

---

### Module 2: Deploy the Landing Zone (60 min) — HANDS-ON LAB

**Key Topics**:
- Clone repository with submodules
- Review and customize parameters (environment name, region, SKUs)
- Execute `azd up` and understand what's being deployed
- Walk through deployed resources in Azure Portal
- Validate deployment: networking, private endpoints, managed identities
- Verify against Design Checklist items (spot-check N-R3, I-R1, S-R1)

**Lab Steps** (high-level):
```bash
# 1. Clone
git clone --recurse-submodules https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git
cd Deploy-Your-AI-Application-In-Production

# 2. Initialize
azd init

# 3. Configure (review parameters)
# See ParameterGuide.md for options

# 4. Deploy
azd up

# 5. Validate
# Check Portal: resource group, networking, private endpoints, RBAC
```

**Key Resources**:
- [Deployment Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/DeploymentGuide.md)
- [Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md)
- [Required Roles & Scopes](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md)

---

### Module 3: Configure & Deploy RAG Application (40 min) — HANDS-ON LAB

**Key Topics**:
- AI Foundry project configuration
- Upload sample data for RAG ingestion
- Configure AI Search index
- Deploy chat application to Container Apps
- Test the RAG application end-to-end
- Understand the data flow: user query → AI Search → model → response

**Key Resources**:
- [AI Foundry Documentation](https://learn.microsoft.com/azure/ai-foundry/)
- [Azure AI Search Documentation](https://learn.microsoft.com/azure/search/)

---

### Module 4: From RAG to Agents (30 min) — CONCEPTUAL + DEMO

> **📌 This is the bridge module** — connecting infrastructure (Modules 2-3) to the broader AI agent adoption story.

**Key Topics**:
- What we just built is a **classic RAG application** — deterministic retrieval
- When would this customer need to **graduate to agents**?
  - Task requires multi-step reasoning
  - Need to call external tools/APIs based on context
  - Inputs are ambiguous and require adaptive behavior
- Microsoft Foundry agent capabilities overview:
  - **Declarative agents**: Prompt-based, behavior-driven (simpler to update)
  - **Hosted agents**: Code-first, custom libraries (full control)
  - **Workflows**: Multi-agent orchestration (sequential, conditional, parallel)
- **Foundry setup alignment**: Standard setup with private networking = the Landing Zone you just deployed
- Single vs. multi-agent decision: when and why
- Live exploration: Foundry agent playground (if time/access permits)

**Key Resources**:
- [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)
- [Technology Plan for AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)
- [Single Agent vs. Multiple Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents)
- [Process to Build AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/build-secure-process)
- [Foundry Agent Quickstart](https://learn.microsoft.com/azure/ai-foundry/agents/quickstart)
- [Agent Design Patterns](https://learn.microsoft.com/azure/architecture/ai-ml/guide/ai-agent-design-patterns)

---

### Module 5: Monitoring & Observability (20 min)

**Key Topics**:
- Azure Monitor baseline for AI workloads
- AI Foundry tracing and evaluation (M-R3)
- Diagnostic settings → Log Analytics (M-R4)
- Key metrics to watch: latency, token usage, error rates
- Model drift detection awareness (M-R5)
- Connecting to GenAIOps (Workshop 3 preview)

**Key Resources**:
- [Design Checklist — Monitoring (M-R1 to M-R6)](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Azure Monitor Baseline Alerts](https://azure.github.io/azure-monitor-baseline-alerts/)

---

### Module 6: Wrap-up & Next Steps (15 min)

**Key Topics**:
- Clean-up: `azd down` to remove lab resources (or keep for experimentation)
- Recap: What we deployed, what we learned, where agents fit
- Next steps for partners:
  1. Repeat the deployment in your own subscription
  2. Experiment with Foundry agent capabilities
  3. Review the full CAF AI Agent Adoption guidance
  4. Attend Workshop 3 for production readiness & GenAIOps
- Workshop 3 preview: CI/CD, lifecycle management, monitoring at scale, cost optimization

---

## 🎓 Instructor Notes

### Preparation Checklist
- [ ] **Test the full deployment** in a clean subscription at least 48 hours before
- [ ] Verify Azure OpenAI quota in target region
- [ ] Prepare a pre-deployed environment as backup (in case `azd up` fails during lab)
- [ ] Bookmark all key Portal pages for quick navigation during demo
- [ ] Prepare Foundry agent playground access for Module 4 demo
- [ ] Print/share the [Required Roles & Scopes](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md) doc
- [ ] Test all links are accessible
- [ ] Prepare troubleshooting guide for common deployment errors

### Delivery Tips
- **Module 2 is the critical path** — if deployment fails, the rest of the lab is impacted. Have a backup plan.
- Allow extra time for Module 2 (~45 min deploy + ~15 min validation)
- Show the Portal walkthrough even if participants deploy independently
- Module 4 is conceptual — adjust depth based on audience technical level
- Encourage participants to keep their deployment running for experimentation after the workshop

### Common Issues to Prepare For
1. **Insufficient quota**: Most common failure. Check beforehand.
2. **Permission errors**: Need Owner or Contributor + UAA
3. **Region availability**: Not all services available in all regions
4. **Deployment timeout**: `azd up` can take 30-45 min; set expectations
5. **Private endpoint DNS resolution**: May need troubleshooting if accessing services after deployment

### Adapting for Time

**If running short (3-hour version)**:
- Shorten Module 4 to 15 min (overview only, skip demo)
- Shorten Module 5 to 10 min (key metrics only)
- Skip Module 1 recap if all participants attended Workshop 1

**If running long (4+ hours)**:
- Extend Module 4 with live Foundry agent creation
- Add hands-on monitoring configuration in Module 5
- Include deeper Design Checklist validation against deployed resources
- Add a "deploy with Bicep" comparison exercise

---

## 📝 Feedback Collection

After the workshop, collect feedback using:

1. **Quick Poll**: Overall satisfaction (1-5)
2. **Lab Effectiveness**: "Were you able to complete the deployment?" (Yes/Partial/No)
3. **Open Questions**:
   - What was most valuable?
   - Where did you get stuck?
   - Was the RAG → Agents narrative useful for customer conversations?
   - What should we add to Workshop 3?

---

## 🔗 Related Resources

### Other Workshops
- [Workshop 1: AI Landing Zone Fundamentals](../01-landing-zone-fundamentals/) — *prerequisite*
- [Workshop 3: Landing Zones to Production](../03-production-readiness/) — *next workshop*

### Documentation
- [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
- [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)
- [Deliverables Roadmap](../../docs/DELIVERABLES-ROADMAP.md)

### External Resources
- [Azure AI Landing Zones GitHub](https://github.com/Azure/AI-Landing-Zones)
- [Deploy Your AI App In Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
- [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)
- [Microsoft Foundry Documentation](https://learn.microsoft.com/azure/ai-foundry/)
- [WAF AI Workloads](https://learn.microsoft.com/azure/well-architected/ai/)

---

**Workshop Owners**: Arturo Quiroga (PSA) & Anahita Afshari (PSA)  
**Created**: February 25, 2026  
**Status**: 🚧 Draft — In Development
