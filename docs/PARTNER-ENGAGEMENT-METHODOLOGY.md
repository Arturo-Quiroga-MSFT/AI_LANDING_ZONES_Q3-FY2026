# AI Landing Zone - Partner Engagement Methodology

**Purpose**: A structured delivery framework for partners executing AI Landing Zone engagements with customers.  
**Audience**: SI and SDC partners, solution architects, technical consultants  
**Last Updated**: February 4, 2026

---

## 🎯 Overview

This methodology provides a step-by-step framework for helping customers move from AI proof-of-concept to production-ready deployments using Azure AI Landing Zones. It ensures consistency, clarity, and impact across customer engagements.

---

## 📋 The 3-Phase Engagement Framework

| Phase | Focus | Duration | Outcome |
|-------|-------|----------|---------|
| **Phase 1: Scoping & Discovery** | Understand use case, assess readiness, align stakeholders | 1-2 weeks | Clear understanding of customer goals and gaps |
| **Phase 2: Assessment & Enablement** | Architecture deep-dive, hands-on deployment, identify gaps | 2-3 weeks | Production-ready architecture design |
| **Phase 3: Implementation & Closeout** | Deliver implementation plan, confirm next steps | 1 week | Actionable roadmap with ownership |

---

## 🏛️ The 6 Pillars of Production Readiness

Successful AI production deployments require proficiency across six foundational pillars:

| Pillar | Description | Key Questions to Ask Customer |
|--------|-------------|-------------------------------|
| **1. AI Center of Excellence** | Governance, operating models, cross-functional alignment | Who owns AI strategy? How are AI initiatives prioritized? |
| **2. AI Landing Zones** | Platform readiness, architecture patterns, deployment pipelines | Do you have existing Azure Landing Zones? What networking constraints exist? |
| **3. Solution Optimization** | Cost management, performance tuning, scalability | What are your latency requirements? Expected token consumption? |
| **4. GenAIOps** | Monitoring, CI/CD, rollback, observability | How will you deploy updates? What's your monitoring strategy? |
| **5. Responsible AI** | Fairness, transparency, safety, compliance | What content safety requirements exist? How do you handle prompt injection? |
| **6. Developer Productivity** | AI-assisted coding, secure adoption | Are developers using GitHub Copilot? What guardrails exist? |

---

## 📍 Phase 1: Scoping & Discovery

### 1.1 Use Case Scoping Session

**Objective**: Align with the customer on their GenAI/Agentic AI use case, production goals, and technical readiness.

**Key Discovery Questions**:

| Category | Questions |
|----------|-----------|
| **Business Objective** | What problem are you solving? What does success look like? |
| **Current State** | Where are you today (PoC, pilot, production)? What's deployed? |
| **Technical Maturity** | Do you have AI Landing Zone infrastructure? What IaC do you use? |
| **Team Skills** | Who will deploy and operate? What's their Azure/AI experience? |
| **Timeline** | When do you need production? What's driving the deadline? |
| **Constraints** | Compliance requirements? Data residency? Network restrictions? |
| **Stakeholders** | Who needs to be involved? (IT, Security, Business, Data) |

**Partner Checklist - Scoping Session**:
- [ ] Schedule scoping call with all relevant customer stakeholders
- [ ] Document business goals, success criteria, and timeline
- [ ] Assess existing Azure Landing Zone status
- [ ] Capture network, identity, and compliance constraints
- [ ] Identify participants for workshops and assessments
- [ ] Determine which workshops are needed (1, 2, and/or 3)

---

### 1.2 Readiness Enablement

**Objective**: Upskill customer stakeholders on foundational concepts before the hands-on assessment.

**Recommended Enablement Path**:

| If Customer Needs... | Deliver... | Duration |
|---------------------|------------|----------|
| AI Landing Zone fundamentals | Workshop 1 | 2-3 hours |
| Hands-on deployment experience | Workshop 2 | 3-4 hours |
| Production operations guidance | Workshop 3 | 4 hours |

**MS Learn Pre-Work** (Assign to customer before workshops):
- [AI Center of Excellence Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/) (1.5 hours)
- [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) (28 min) - **Required**

**Partner Checklist - Enablement**:
- [ ] Assign MS Learn pre-work to customer participants
- [ ] Confirm which workshops are needed based on scoping
- [ ] Schedule workshop sessions (allow 2-3 days between if multiple)
- [ ] Deliver workshops using official materials
- [ ] Capture questions, blockers, and insights for assessment planning

---

### 1.3 Gap Analysis

**Objective**: Assess production readiness and surface blockers using the Design Checklist.

**Assessment Approach**:

Walk through the [AI Landing Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) with the customer:

| Design Area | Key Questions | Checklist Reference |
|-------------|---------------|---------------------|
| **Networking** | Private endpoints configured? Hub connectivity? DNS resolution? | N-R1 to N-R9 |
| **Identity** | Managed identities? RBAC configured? Key-based access disabled? | I-R1 to I-R6 |
| **Security** | Defender enabled? Content safety configured? Purview integrated? | S-R1 to S-R5 |
| **Monitoring** | Diagnostics enabled? Alerts configured? Model drift tracked? | M-R1 to M-R6 |
| **Cost** | PTU vs PAYGO strategy? Auto-shutdown for non-prod? | CO-R1 to CO-R4 |
| **Governance** | Azure Policy applied? Model catalog restrictions? | G-R1 to G-R5 |

**Partner Checklist - Gap Analysis**:
- [ ] Schedule 2-3 hour assessment session with customer SMEs
- [ ] Walk through Design Checklist systematically
- [ ] Document current state vs recommended state for each area
- [ ] Identify critical gaps that block production
- [ ] Prioritize gaps by impact and effort
- [ ] Generate summary for architecture deep-dive

---

## 📍 Phase 2: Assessment & Enablement Engagement

### 2.1 Architecture Deep-Dive

**Objective**: Conduct thorough assessment of customer's current architecture to identify improvement opportunities.

**Architecture Review Framework**:

```
┌─────────────────────────────────────────────────────────────┐
│                    CUSTOMER ARCHITECTURE                     │
├─────────────────────────────────────────────────────────────┤
│  1. PLATFORM FOUNDATION                                      │
│     └─ Existing Landing Zone? Hub connectivity? Governance?  │
├─────────────────────────────────────────────────────────────┤
│  2. AI WORKLOAD COMPONENTS                                   │
│     └─ AI Foundry? Model deployments? Data stores?           │
├─────────────────────────────────────────────────────────────┤
│  3. SECURITY & IDENTITY                                      │
│     └─ Private endpoints? Managed identity? RBAC?            │
├─────────────────────────────────────────────────────────────┤
│  4. OPERATIONS & MONITORING                                  │
│     └─ Observability? CI/CD? Alerting?                       │
├─────────────────────────────────────────────────────────────┤
│  5. DATA & INTEGRATION                                       │
│     └─ RAG sources? Embedding pipeline? Governance?          │
└─────────────────────────────────────────────────────────────┘
```

**Session Agenda** (Full Day):

| Time | Activity | Outcome |
|------|----------|---------|
| 9:00-9:30 | Welcome & Objectives | Align on goals |
| 9:30-10:00 | Recap Enablement | Ensure common baseline |
| 10:00-12:00 | Architecture Deep-Dive | Identify gaps |
| 12:00-1:00 | Lunch | |
| 1:00-3:00 | Breakout Sessions | Detailed technical input |
| 3:00-4:00 | Wrap-up & Next Steps | Summarize decisions |

**Partner Checklist - Architecture Review**:
- [ ] Finalize agenda 2 days before session
- [ ] Confirm all stakeholders (IT, Security, Data, Business)
- [ ] Prepare whiteboard/Miro board for architecture capture
- [ ] Walk through each layer of the architecture
- [ ] Document all decisions, gaps, and open questions
- [ ] Assign owners for follow-up items

---

## 📍 Phase 3: Implementation & Closeout

### 3.1 Implementation Plan Delivery

**Objective**: Compile assessment outputs into an actionable implementation roadmap.

**Implementation Plan Structure**:

```markdown
## Implementation Plan Template

### 1. Executive Summary
- Use case overview
- Key findings
- Recommended approach

### 2. Current State Assessment
- Architecture diagram (as-is)
- Gap analysis summary by pillar
- Risk assessment

### 3. Target State Architecture
- Architecture diagram (to-be)
- Component changes required
- Deployment approach (azd/Bicep/Terraform)

### 4. Implementation Roadmap
| Phase | Activities | Duration | Owner |
|-------|------------|----------|-------|
| Phase 1 | Platform foundation | 2 weeks | Customer Infra |
| Phase 2 | AI workload deployment | 2 weeks | Customer AI Team |
| Phase 3 | Security hardening | 1 week | Customer Security |
| Phase 4 | Operationalization | 2 weeks | Customer Ops |

### 5. Risks & Mitigations
| Risk | Impact | Mitigation | Owner |
|------|--------|------------|-------|

### 6. Next Steps
- Immediate actions (next 2 weeks)
- Follow-up sessions needed
- Support and escalation paths
```

**Partner Checklist - Closeout**:
- [ ] Consolidate all assessment notes and architecture artifacts
- [ ] Draft implementation plan using template above
- [ ] Review internally before sharing with customer
- [ ] Deliver final plan within 5 business days of assessment
- [ ] Schedule follow-up session to align on execution
- [ ] Confirm handoff to implementation team (if different)

---

## 🎯 Workshop-to-Phase Mapping

| Our Workshop | Engagement Phase | Pillar Coverage |
|--------------|------------------|-----------------|
| **Workshop 1: Fundamentals** | Phase 1 (Scoping) | AI CoE, AI Landing Zones, Responsible AI |
| **Workshop 2: Deployment** | Phase 2 (Assessment) | AI Landing Zones, Solution Optimization |
| **Workshop 3: Production** | Phase 3 (Closeout) | GenAIOps, Solution Optimization |

---

## 📚 Reference Materials

### Official Resources
- [AI Landing Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Deploy Your AI App in Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
- [Enterprise-Scale (ALZ) Wiki](https://github.com/Azure/Enterprise-Scale/wiki)
- [AI CoE Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/)

### Partner Enablement Materials
- [Partner Quick Reference Guide](./PARTNER-QUICK-REFERENCE.md)
- [IaC Decision Framework](./IAC-DECISION-FRAMEWORK.md)
- [Workshop Materials](../workshops/)

---

## ✅ Overall Engagement Outcomes

A successful AI Landing Zone engagement should deliver:

| Outcome | Description |
|---------|-------------|
| ✅ **Enhanced Use Case Understanding** | Deep understanding of customer's AI use case, production goals, and technical readiness |
| ✅ **Stakeholder Alignment** | All stakeholders aligned on key terminology, concepts, and governance |
| ✅ **Gap Identification** | Architectural gaps, operational risks, and platform limitations identified |
| ✅ **Clear Implementation Roadmap** | Actionable plan with assigned ownership and milestones |
| ✅ **Continued Momentum** | Customer has tangible artifact to align internal teams and secure sponsorship |

---

*This methodology is maintained by the AI CoE Partner Enablement team.*  
*Questions? Contact Arturo Quiroga or Anahita Afshari*
