# Partner Pitch Deck - Slide Outline

**Purpose**: Structure for the partner-facing pitch deck explaining AI Landing Zones business value  
**Owner**: Anahita Afshari (PSA) + Arturo Quiroga (PSA)  
**Status**: 📋 Outline — Ready for PowerPoint creation  
**Created**: February 25, 2026

> **📌 Note**: This outline incorporates Microsoft's official [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) business planning framework for partner conversations about AI agents and Landing Zones.

---

## Section 1: The Opportunity (3-4 slides)

### Slide 1: Title
- **Title**: AI Landing Zones — Accelerating Production-Ready AI on Azure
- **Subtitle**: Partner Enablement Briefing
- **Footer**: AI Center of Excellence V2 | Q3 FY2026

### Slide 2: The AI Imperative
- Enterprises are rushing to deploy Gen AI workloads
- Most PoCs never reach production (security, governance, scalability gaps)
- Partners who can bridge PoC → Production win strategic engagements
- **Key stat**: [Include relevant adoption stat from Microsoft data]

### Slide 3: What Customers Are Building
- **Two categories of AI workloads** partners should understand:

| Workload Type | Description | Complexity |
|--------------|-------------|------------|
| **Classic RAG** | Deterministic retrieval — chat, Q&A, knowledge bases | Lower — predictable, well-understood |
| **AI Agents** | Adaptive reasoning — multi-step orchestration, tool use | Higher — nondeterministic, requires governance |

- Microsoft's CAF identifies 3 agent types with increasing capability:
  1. **Productivity Agents** — Retrieve & synthesize information
  2. **Action Agents** — Perform specific tasks within workflows
  3. **Automation Agents** — Multi-step processes, minimal human oversight

- **Source**: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)

### Slide 4: The Partner Opportunity
- Deploy production-ready AI infrastructure in hours, not months
- Cover the full spectrum: classic RAG → AI agents
- Differentiate with security, governance, and operational readiness
- Align with Microsoft's official guidance and tooling

---

## Section 2: AI Landing Zones — The Foundation (4-5 slides)

### Slide 5: What Is an AI Landing Zone?
- Secure, resilient, scalable reference architecture for AI workloads
- Production-ready from Day 0 (security, networking, governance built in)
- Official Microsoft guidance — not a community project
- Available as: Bicep, Terraform, azd, Portal (coming soon)

### Slide 6: Two Architecture Options
- **With Platform Landing Zone** — Enterprise customers with existing ALZ
- **Without Platform Landing Zone** — Greenfield, PoCs, standalone
- Both are production-ready; choose based on customer context
- **Diagrams**: Reference official architecture images

### Slide 7: What's Included
- **AI Layer**: AI Foundry, AI Search, model endpoints
- **Compute**: Container Apps, App Service, Functions
- **Data**: Cosmos DB, Storage, Fabric integration
- **Security**: Private endpoints, Key Vault, Managed Identity, Defender
- **Governance**: Azure Policy, Purview, Responsible AI, Content Safety
- **Monitoring**: Azure Monitor, Log Analytics, AI Foundry tracing

### Slide 8: From Landing Zone to AI Agents
- The Landing Zone is the *infrastructure foundation*
- The [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) framework covers *what runs on it*
- **4-phase adoption process**:
  1. **Plan** — Business plan, technology plan, org readiness, data architecture
  2. **Govern & Secure** — Responsible AI, governance, prepare environment
  3. **Build** — Single/multi-agent systems, build process
  4. **Manage** — Integration, operations (GenAIOps)

---

## Section 3: Business Value & ROI (4-5 slides)

> **📌 Framework Source**: [CAF Business Plan for AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan)

### Slide 9: Four Strategic Impact Areas
- Microsoft identifies 4 quadrants where AI agents create business value:

| Impact Area | Description | Example |
|------------|-------------|---------|
| **Reshape Business Processes** | Automate complex, multi-step workflows | Supply chain adjustments, incident triage |
| **Enrich Employee Experiences** | Augment staff by handling cognitive load | Research synthesis, technical content drafting |
| **Reinvent Customer Engagement** | Resolve dynamic queries autonomously | Context-aware customer support, personalized service |
| **Accelerate Innovation** | Analyze trends, simulate scenarios | Shorten product dev cycles, faster experimentation |

- **Source**: [CAF AI Agent Opportunities](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-to-use-ai-agents)

### Slide 10: When to Use Agents (Decision Tree)
- **Not everything needs an agent** — help customers avoid over-engineering
- **Don't use agents when**: Task is predictable/rule-based, or goal is static Q&A
- **Use agents when**: Task requires dynamic decision-making, complex orchestration, or adaptive behavior
- **Reference**: [AI Agent Decision Tree](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents)

### Slide 11: Prioritizing Use Cases (Partner Framework)
- Microsoft's 3-criteria scoring model (1-5 scale each):

| Criterion | What to Evaluate |
|-----------|-----------------|
| **Business Impact** | Executive alignment, quantifiable value, change management timeframe |
| **Technical Feasibility** | Implementation risks, safeguards maturity, technology fit |
| **User Desirability** | Key personas defined, value proposition clear, change resistance low |

- **Partner action**: Use this framework in discovery workshops to rank customer use cases
- **Source**: [Prioritize AI Agent Use Cases](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#how-to-prioritize-ai-agent-use-cases)

### Slide 12: Defining Success Metrics
- Establish measurable KPIs *before* development begins:
  1. **Set baseline business goals** — Measure current process performance
  2. **Use business metrics as decision gates** — Continue, pivot, or stop at checkpoints
  3. **Evaluate post-deployment** — Compare actual results vs. target KPIs
- Partners should include success metrics in every engagement statement of work

### Slide 13: Technology Selection Path
- Guide customers through build-vs-buy:

| Option | Type | Best For |
|--------|------|----------|
| **SaaS Agents** (M365, Dynamics, Security Copilot) | Ready-to-use | Immediate value, standard functions |
| **Microsoft Foundry** | PaaS (pro-code & low/no-code) | Custom agents, deep integration — **deploys on AI Landing Zone** |
| **Copilot Studio** | SaaS (low/no-code) | Fast development, business teams |
| **GPUs + Containers** (AKS, Container Apps) | IaaS/PaaS | Custom model hosting, strict compliance |

- **Key insight**: Foundry's standard setup with private networking **maps directly to the AI Landing Zone architecture**
- **Source**: [Technology Plan for AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)

---

## Section 4: Partner Engagement Model (3-4 slides)

### Slide 14: The Partner Delivery Journey
- **Step 1: Discover** — Qualify use cases using agent decision tree + prioritization framework
- **Step 2: Deploy** — Stand up AI Landing Zone infrastructure (Bicep/Terraform/azd)
- **Step 3: Build** — Deploy workloads (RAG → Agents) using Foundry/Copilot Studio
- **Step 4: Operate** — GenAIOps, monitoring, lifecycle management

### Slide 15: Engagement Scenarios at a Glance

| Scenario | Recommended Path | Key Focus |
|----------|-----------------|-----------|
| Enterprise with ALZ | Bicep/Terraform + Platform LZ | Networking, Identity integration |
| Greenfield/PoC | azd up (standalone) | Speed, validation, cost |
| Regulated Industry | Bicep + security review | Security, Governance, compliance |
| Cost-Sensitive | Minimal deployment | Cost optimization, right-sizing |
| AI Agents | Foundry standard setup on LZ | Agent decision tree, governance, testing |

### Slide 16: Partner Resources & Enablement
| Resource | What It Provides |
|----------|-----------------|
| [AI Landing Zones Repo](https://github.com/Azure/AI-Landing-Zones) | Architecture, IaC templates, Design Checklist |
| [Deploy-Your-AI-App](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) | Full production deployment (azd up) |
| [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) | Business planning, technology selection, governance |
| [AI CoE Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/) | Training for all partners (1.5 hrs) |
| [Partner Quick Reference](../docs/PARTNER-QUICK-REFERENCE.md) | Curated navigation guide (internal) |

### Slide 17: Call to Action
1. Complete the [AI CoE Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/) (1.5 hrs)
2. Deploy a test environment using `azd up`
3. Use the [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) with your next customer
4. Review [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) for agent conversations
5. Attend our [Workshops](../workshops/) for hands-on practice

---

## 📝 Design Notes

### Tone & Audience
- **Audience**: Partner sales, solution architects, technical consultants
- **Tone**: Strategic but practical — "here's why this matters and here's exactly how to do it"
- **Goal**: Equip partners to have confident AI Landing Zone + AI Agent conversations with customers

### Visuals to Include
- Official AI Landing Zone architecture diagrams (with/without platform LZ)
- CAF AI Agent Adoption 4-phase workflow diagram
- Agent spectrum diagram (Productivity → Action → Automation)
- Agent decision tree diagram
- Use case prioritization framework diagram (Business Impact × Feasibility × Desirability)
- Technology build options comparison diagram

### Key Diagrams from CAF AI Agents (reference, don't copy)
| Diagram | Source URL |
|---------|-----------|
| AI Agent Adoption Process | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/ai-agent-adoption.svg` |
| Agent Decision Tree | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/ai-agent-decision-tree.svg` |
| Agent Types Spectrum | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/spectrum-agents.png` |
| Agent Architecture (5 components) | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/agent-overview.png` |
| AI Agent Opportunities (4 quadrants) | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/ai-agent-opportunities.png` |
| Use Case Prioritization | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/prioritize-agent-use-cases.png` |
| Build Options Overview | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/build-overview.png` |
| Technology Options | `https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/images/technology-options.png` |

---

**Total Estimated Slides**: 17-20  
**Target Creation Time**: 3-4 hours  
**Reviewer**: Arturo Quiroga (PSA)  
**Created**: February 25, 2026
