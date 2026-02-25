# Workshop 3: Landing Zones to Production (GenAIOps Bridge)

**Duration**: 4 hours  
**Level**: 400 (Expert)  
**Lead**: Arturo Quiroga (PSA)  
**Co-Leads**: Ana Lopez Moreno (PSA), George Bittencourt (PSA), Guilherme Nogueira (PSA)  
**Reviewer**: Anahita Afshari (PSA)

---

## 🎯 Workshop Overview

This workshop bridges the gap between a deployed AI workload (Workshop 2) and running it in production. Partners learn to operationalize AI Landing Zones with CI/CD, monitoring, governance, cost optimization, and — critically — agent-specific operational patterns from the CAF AI Agents framework.

### 📌 Key Concept

> **Deploying is Day 1. Operating is Day 2 through Day N.**
>
> Workshop 2 deployed a Landing Zone and built a RAG/agent workload. This workshop covers what happens next: how to ship changes safely, monitor in production, govern agent behavior, and optimize costs at scale.
>
> 📚 Pre-read: [CAF Govern & Secure AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure) | [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)

---

## 👥 Target Audience

- Partner architects planning production AI deployments
- DevOps/platform engineers building AI pipelines
- Operations teams managing AI workloads
- Security and governance leads for AI projects

---

## 📚 Prerequisites

### Required Knowledge
- **Completed Workshop 2** (or have a deployed AI Landing Zone)
- CI/CD fundamentals (GitHub Actions or Azure DevOps)
- Azure Monitor and Log Analytics basics
- Familiarity with AI Foundry and RAG patterns

### Required Access
- Azure subscription with deployed Workshop 2 environment (or equivalent)
- GitHub account (for CI/CD module)
- Azure DevOps organization (optional alternative)

---

## 🗂️ Workshop Materials

| Material | Description | Location |
|----------|-------------|----------|
| Workshop Guide | Step-by-step facilitation guide | [WORKSHOP-GUIDE.md](./WORKSHOP-GUIDE.md) |
| Slide Deck Outline | Presentation structure | [SLIDE-OUTLINE.md](./SLIDE-OUTLINE.md) |
| Design Checklist | Official Microsoft resource | [GitHub](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |

---

## 📋 Learning Objectives

By the end of this workshop, participants will be able to:

1. **Implement** CI/CD pipelines for AI applications on Landing Zones
2. **Configure** production monitoring, alerting, and dashboards for AI workloads
3. **Apply** agent governance controls (data access, tool permissions, human-in-the-loop)
4. **Design** agent operational runbooks and versioning strategies
5. **Optimize** costs for AI workloads (model selection, scaling, reserved capacity)
6. **Plan** a production cutover from PoC to enterprise-grade operations

---

## ⏱️ Agenda

| Time | Duration | Module | Description |
|------|----------|--------|-------------|
| 0:00 | 15 min | **Welcome & Context Setting** | Workshop 2 recap, production readiness gap analysis |
| 0:15 | 50 min | **Module 1: CI/CD for AI Workloads** | Pipelines, IaC automation, model deployment, testing |
| 1:05 | 10 min | **Break** | |
| 1:15 | 45 min | **Module 2: Production Monitoring & Observability** | Dashboards, alerting, AI Foundry tracing, SLAs |
| 2:00 | 10 min | **Break** | |
| 2:10 | 45 min | **Module 3: Agent Governance & Security** | CAF Govern & Secure, tool permissions, responsible AI |
| 2:55 | 10 min | **Break** | |
| 3:05 | 30 min | **Module 4: Cost Optimization & Scaling** | Model economics, reserved capacity, autoscaling |
| 3:35 | 25 min | **Module 5: Wrap-up & Production Planning** | Runbook template, cutover checklist, Q&A |

---

## 📦 Module Summaries

### Module 1: CI/CD for AI Workloads (50 min)

> **🔧 Ana/George/Guilherme**: This is the core Gen AI OPS module. Please fill in pipeline patterns, preferred tooling, and any accelerator content you have.

**Key Topics**:
- CI/CD pipeline architecture for AI Landing Zones
- Infrastructure pipeline (Bicep/Terraform) vs. application pipeline (container build/deploy)
- Model deployment and versioning strategies
- Testing AI workloads: unit tests, integration tests, model evaluation
- Blue/green and canary deployment patterns for AI apps
- GitHub Actions / Azure DevOps pipeline templates

**Key Resources**:
- *TODO: Add Gen AI OPS accelerator pipeline references*
- [Deploy-Your-AI-App CI/CD](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

---

### Module 2: Production Monitoring & Observability (45 min)

> **🔧 Ana/George/Guilherme**: Build on the monitoring baseline from WS2 Module 5. Add production-grade patterns: dashboards, alerting rules, runbook triggers.

**Key Topics**:
- Production monitoring stack: Application Insights + Log Analytics + AI Foundry Tracing
- Building monitoring dashboards (Azure Workbooks or Grafana)
- Alert rules: latency thresholds, error rates, token budget limits, model drift
- AI-specific observability: retrieval quality, response relevance, hallucination detection
- Agent observability: tool call monitoring, reasoning chain tracing, escalation tracking
- SLA definition for AI workloads (latency P95, availability, response quality)
- Design Checklist items: M-R1 through M-R6

**Key Resources**:
- [Azure Monitor Baseline Alerts](https://azure.github.io/azure-monitor-baseline-alerts/)
- [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)

---

### Module 3: Agent Governance & Security (45 min)

> **📌 This is the newest module** — built from the CAF AI Agents Govern & Secure phase. This bridges traditional AI governance with agent-specific patterns.

**Key Topics**:
- CAF Govern & Secure phase for AI agents
- Data access controls: what data can agents access, under what conditions
- Tool permission boundaries: which APIs/tools each agent can invoke
- Human-in-the-loop policies: when agents must escalate vs. act autonomously
- Responsible AI guardrails for agent outputs (content filtering, grounding enforcement)
- Multi-agent security: credential isolation, cross-boundary trust models
- Agent audit trail: logging all tool calls, decisions, and data access
- Compliance mapping: AI agents in regulated industries

**Key Resources**:
- [CAF Govern & Secure AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)
- [CAF Build Secure Process](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/build-secure-process)
- *TODO: Add specific governance templates or checklists*

---

### Module 4: Cost Optimization & Scaling (30 min)

**Key Topics**:
- AI workload cost model: compute + model inference (tokens) + storage + networking
- Model selection economics: GPT-4o vs. smaller models for different tasks
- Reserved capacity and provisioned throughput for Azure OpenAI
- Autoscaling Container Apps for variable AI workloads
- Cost allocation and showback using tags
- Right-sizing AI Search and Cosmos DB tiers
- Design Checklist items: C-R1 through C-R4

**Key Resources**:
- [Azure OpenAI Pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/)
- [Azure Cost Management](https://learn.microsoft.com/azure/cost-management-billing/)

---

### Module 5: Wrap-up & Production Planning (25 min)

**Key Topics**:
- Production readiness checklist (comprehensive)
- Operational runbook template for AI workloads
- Agent-specific failure modes and recovery procedures
- Cutover planning: PoC → staging → production
- Support model: who owns what in production
- Workshop series recap: WS1 (concepts) → WS2 (build) → WS3 (operate)
- Next steps and ongoing learning resources

---

## 🎓 Instructor Notes

### Preparation Checklist
- [ ] Coordinate content with Gen AI OPS team (Ana, George, Guilherme)
- [ ] Have a deployed Workshop 2 environment available for demo
- [ ] Prepare sample CI/CD pipeline (GitHub Actions or Azure DevOps)
- [ ] Build or obtain sample monitoring dashboard
- [ ] Prepare agent governance scenario for discussion exercise
- [ ] Review all CAF AI Agents governance documentation
- [ ] Test all links are accessible

### Content Ownership

| Module | Primary Owner | Supporting |
|--------|--------------|-----------|
| Module 1: CI/CD | Ana / George / Guilherme | Arturo |
| Module 2: Monitoring | Ana / George / Guilherme | Arturo |
| Module 3: Agent Governance | Arturo | Ana |
| Module 4: Cost Optimization | Arturo | Anahita |
| Module 5: Wrap-up | Arturo | All |

### Delivery Tips
- This audience is advanced — skip basics, go deep on patterns
- Use real pipeline YAML/code, not just concepts
- Agent governance is new territory — expect lots of questions
- Cost optimization resonates strongly with decision-makers

---

## 📝 Feedback Collection

1. **Quick Poll**: Overall satisfaction (1-5)
2. **Depth Check**: "Was the content advanced enough for your needs?"
3. **Open Questions**:
   - What operational patterns are you missing?
   - Which module was most valuable for production planning?
   - What would you add for a V2 of this workshop?

---

## 🔗 Related Resources

### Other Workshops
- [Workshop 1: AI Landing Zone Fundamentals](../01-landing-zone-fundamentals/) — *foundational concepts*
- [Workshop 2: From RAG to Agents](../02-first-genai-workload/) — *prerequisite*

### Documentation
- [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
- [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)
- [Deliverables Roadmap](../../docs/DELIVERABLES-ROADMAP.md)
- [Diagram References](../../architecture/diagrams/DIAGRAM-REFERENCES.md)

### External Resources
- [Azure AI Landing Zones GitHub](https://github.com/Azure/AI-Landing-Zones)
- [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)
- [CAF Govern & Secure AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)
- [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)
- [Azure Monitor Baseline Alerts](https://azure.github.io/azure-monitor-baseline-alerts/)

---

**Workshop Owners**: Arturo Quiroga (PSA), Ana Lopez Moreno (PSA), George Bittencourt (PSA) & Guilherme Nogueira (PSA)  
**Created**: February 25, 2026  
**Status**: 📋 Scaffold — Awaiting Gen AI OPS team input
