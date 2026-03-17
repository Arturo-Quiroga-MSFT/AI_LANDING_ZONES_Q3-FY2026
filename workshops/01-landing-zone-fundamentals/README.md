# Workshop 1: AI Landing Zone Fundamentals

**Duration**: 2-3 hours  
**Level**: 200 (Intermediate)  
**Lead**: Anahita Afshari (PSA)  
**Co-Lead**: Arturo Quiroga (PSA)  
**Reviewer**: Arturo Quiroga (PSA)

---

## 🎯 Workshop Overview

This workshop introduces partners to Azure AI Landing Zones, covering core concepts, architecture patterns, and the official design checklist. By the end, participants will understand how to assess customer needs and select appropriate AI Landing Zone configurations.

### 📌 Key Foundation Concept

> **AI Landing Zones are Application Landing Zones** within the [Cloud Adoption Framework (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/). They are NOT a separate landing zone type—they deploy INTO existing Azure Landing Zone architectures or standalone.
>
> - **With Platform Landing Zone**: Leverages existing hub networking, firewall, DNS, Bastion (enterprise customers)
> - **Without Platform Landing Zone**: Standalone deployment with own networking (PoCs, greenfield)
>
> 📚 Pre-read: [AI in Azure Landing Zones](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/#ai-in-azure-landing-zones)

---

## 👥 Target Audience

- Partner solution architects
- Technical consultants
- Pre-sales engineers
- DevOps engineers new to AI workloads

---

## 📚 Prerequisites

> **📋 Detailed prerequisites and pre-work instructions**: [PREREQUISITES.md](./PREREQUISITES.md)

### Required Knowledge

* Basic Azure fundamentals (compute, storage, networking)
* Understanding of Azure subscription and resource group concepts
* Familiarity with Azure Portal navigation
* Networking basics: virtual networks, subnets, DNS

### Required Microsoft Learn Modules (Pre-Work)

Participants **must complete** these modules before the workshop (~1 hr 30 min total):

| Module | Duration |
|--------|----------|
| [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) | 28 min |
| [Choose the Best Azure Landing Zone](https://learn.microsoft.com/training/modules/cloud-adoption-framework-ready/) | 30 min |
| [Design a Governance Strategy](https://learn.microsoft.com/training/modules/cloud-adoption-framework-govern/) | 30 min |

### Required Access

* GitHub account (to view official repositories)
* Internet access for documentation references
* Azure subscription with Contributor role (for optional hands-on exercises)

### Recommended Preparation

* Review the [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
* Skim the [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
* Browse the [AI Landing Zones GitHub README](https://github.com/Azure/AI-Landing-Zones#readme)

### ⚠️ Cost Warning

> **Azure costs can be significant.** A standard AI Landing Zone deployment costs **~$2,128-3,098/month** per the official [Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md). If you plan to deploy resources during or after the workshop, **delete all resources immediately after** to avoid unexpected charges. See [PREREQUISITES.md — Cost Considerations](./PREREQUISITES.md#cost-considerations) for details and a cleanup checklist.

---

## 🗂️ Workshop Materials

| Material | Description | Location |
|----------|-------------|----------|
| Prerequisites & Pre-Work | Required modules, access, and cost warnings | [PREREQUISITES.md](./PREREQUISITES.md) |
| Workshop Guide | Step-by-step facilitation guide | [WORKSHOP-GUIDE.md](./WORKSHOP-GUIDE.md) |
| Slide Deck Outline | Presentation structure | [SLIDE-OUTLINE.md](./SLIDE-OUTLINE.md) |
| Design Checklist | Official Microsoft WAF-aligned resource | [GitHub](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Cost Guide | Official per-service cost breakdown | [GitHub](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md) |
| Exercises | Hands-on activities | [EXERCISES.md](./EXERCISES.md) |
| Assessment Template | Customer discovery tool | `/templates/assessment-tools/` |

---

## 📋 Learning Objectives

By the end of this workshop, participants will be able to:

1. **Explain** what Azure AI Landing Zones are and why they matter
2. **Identify** the key components of an AI Landing Zone architecture
3. **Compare** deployment options (with/without Platform Landing Zone)
4. **Navigate** the official Design Checklist across 10 design areas
5. **Assess** customer requirements using the Partner Quick Reference
6. **Choose** the appropriate IaC approach for different scenarios
7. **Plan** next steps for a customer engagement

---

## ⏱️ Agenda

| Time | Duration | Module | Description |
|------|----------|--------|-------------|
| 0:00 | 15 min | **Welcome & Objectives** | Introductions, agenda, learning goals |
| 0:15 | 25 min | **Module 1: What is AI Landing Zone?** | Concepts, CAF/WAF alignment, use cases |
| 0:40 | 30 min | **Module 2: Reference Architectures** | With/without platform LZ, component deep-dive |
| 1:10 | 10 min | **Break** | |
| 1:20 | 40 min | **Module 3: Design Checklist Walkthrough** | 10 design areas, key recommendations |
| 2:00 | 25 min | **Module 4: Deployment Options** | IaC comparison, decision framework |
| 2:25 | 20 min | **Module 5: Partner Engagement Scenarios** | Customer discovery, positioning |
| 2:45 | 15 min | **Wrap-up & Next Steps** | Q&A, resources, Workshop 2 preview |

---

## 📦 Module Summaries

### Module 1: What is AI Landing Zone? (25 min)

**Key Topics**:
- Definition and purpose of AI Landing Zones
- Relationship to Azure Landing Zones (ALZ)
- Cloud Adoption Framework (CAF) alignment
- Well-Architected Framework (WAF) alignment
- Target use cases and scenarios

**Key Resources**:
- [Official README](https://github.com/Azure/AI-Landing-Zones#readme)
- [CAF AI Scenario](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/)

---

### Module 2: Reference Architectures (30 min)

**Key Topics**:
- Architecture with Platform Landing Zone (enterprise)
- Architecture without Platform Landing Zone (standalone)
- Key components: AI Foundry, Container Apps, Data Layer, Security
- When to use which architecture

**Key Resources**:
- [Architecture Diagram (with platform)](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)
- [Architecture Diagram (without platform)](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)

---

### Module 3: Design Checklist Walkthrough (40 min)

**Key Topics**:
- 10 design areas overview
- Deep-dive into critical recommendations:
  - Networking (N-R1 to N-R9)
  - Identity (I-R1 to I-R6)
  - Security (S-R1 to S-R5)
  - Monitoring (M-R1 to M-R6)
- How to use checklist with customers

**Key Resources**:
- [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Partner Quick Reference](../../docs/PARTNER-QUICK-REFERENCE.md)

---

### Module 4: Deployment Options (25 min)

**Key Topics**:
- Azure Developer CLI (azd up) - quick deploy
- Bicep templates - Azure-native
- Terraform modules - multi-cloud
- [Portal (Deploy to Azure)](https://github.com/Azure/AI-Landing-Zones#deploy-to-azure) - one-click from repo
- Decision framework for choosing approach

**Key Resources**:
- [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)
- [Deploy-Your-AI-App Repository](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

---

### Module 5: Partner Engagement Scenarios (20 min)

**Key Topics**:
- Enterprise customer with existing Landing Zones
- Greenfield/PoC deployment
- Regulated industry requirements
- Cost-sensitive scenarios
- SI vs SDC positioning differences
- Customer discovery questions

**Key Resources**:
- [Partner Quick Reference - Scenarios](../../docs/PARTNER-QUICK-REFERENCE.md#-partner-engagement-scenarios)

---

## 🎓 Instructor Notes

### Preparation Checklist
- [ ] Review all linked documentation
- [ ] Test all links are accessible
- [ ] Prepare demo subscription (optional)
- [ ] Print/share Design Checklist for participants
- [ ] Prepare Q&A backup slides
- [ ] Test screen sharing and connectivity

### Delivery Tips
- Start with "why" before "how"
- Use real customer scenarios where possible
- Encourage questions during each module
- Reference official docs constantly (build muscle memory)
- Don't recreate content—show where to find it
- Leave time for Q&A in each module

### Common Questions to Prepare For
1. "How does this differ from regular Azure Landing Zones?"
2. "Can we use this for non-GenAI workloads?"
3. "What's the cost of a typical deployment?"
4. "How long does deployment take?"
5. "Is this production-ready?"

---

## 📝 Feedback Collection

After the workshop, collect feedback using:

1. **Quick Poll**: Overall satisfaction (1-5)
2. **Open Questions**:
   - What was most valuable?
   - What was confusing or missing?
   - What should we add to Workshop 2?

---

## 🔗 Related Resources

### Next Workshops
- [Workshop 2: From RAG to Agents — Deploying Your First Gen AI Workload](../02-first-genai-workload/)
- [Workshop 3: Landing Zones to Production](../03-production-readiness/)

### Documentation
- [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
- [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)
- [Deliverables Roadmap](../../docs/DELIVERABLES-ROADMAP.md)

### External Resources
- [Azure AI Landing Zones GitHub](https://github.com/Azure/AI-Landing-Zones)
- [AI Landing Zones Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md)
- [AI Landing Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Deploy Your AI App In Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
- [CAF AI Scenario](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/)
- [WAF AI Workloads](https://learn.microsoft.com/azure/well-architected/ai/)

---

**Workshop Owners**: Anahita Afshari (PSA) & Arturo Quiroga (PSA)  
**Last Updated**: February 25, 2026  
**Status**: 🚧 Draft - In Development
