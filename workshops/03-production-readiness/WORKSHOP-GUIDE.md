# Workshop 3: Facilitation Guide

**Purpose**: Step-by-step facilitation scaffold for Workshop 3 delivery  
**Format**: Instructor-led with live demos and guided discussion  
**Total Duration**: 4 hours (with breaks)

> **🔧 For Ana, George, Guilherme**: Sections marked with *(GEN AI OPS — FILL IN)* are placeholders for your team's content. The scaffold provides structure and talking-point starters; add your operational expertise, pipeline YAML, dashboard templates, and customer examples.

---

## Pre-Workshop Checklist

### Audience Preparation
- [ ] Attendees have completed (or reviewed materials from) WS1 and WS2
- [ ] Attendees have access to a deployed Landing Zone with at least one AI workload
- [ ] Pre-read distributed: CAF AI Agent Adoption overview + Module 3 governance primer

### Environment Preparation
- [ ] Demo environment: Landing Zone with deployed RAG app (from WS2)
- [ ] CI/CD pipeline configured in GitHub Actions or Azure DevOps (demo-ready)
- [ ] Application Insights / Log Analytics workspace with sample telemetry data
- [ ] Azure Workbook or Grafana dashboard pre-built for demo
- [ ] Cost Management view configured with tags and budgets
- [ ] *(GEN AI OPS — FILL IN)* Any additional demo environments or accelerator repos

### Instructor Preparation
- [ ] Review all 5 modules and slide deck
- [ ] Prepare 2-3 real pipeline YAML examples
- [ ] Prepare 2-3 real monitoring dashboard screenshots
- [ ] Identify 1-2 customer stories for governance/cost sections
- [ ] Dry run the demo flow end to end (30 min)

---

## Delivery Timeline

| Time | Duration | Activity |
|------|----------|----------|
| 0:00 | 10 min | Welcome, Agenda, Context |
| 0:10 | 50 min | **Module 1**: CI/CD for AI Workloads |
| 1:00 | 10 min | ☕ Break |
| 1:10 | 45 min | **Module 2**: Production Monitoring & Observability |
| 1:55 | 10 min | ☕ Break |
| 2:05 | 45 min | **Module 3**: Agent Governance & Security |
| 2:50 | 10 min | ☕ Break |
| 3:00 | 30 min | **Module 4**: Cost Optimization & Scaling |
| 3:30 | 25 min | **Module 5**: Wrap-up & Production Planning |
| 3:55 | 5 min | Close & Survey |

---

## Module-by-Module Facilitation

---

### Welcome & Context (10 min)

**Objective**: Ground participants in the workshop journey and set expectations.

**Talking Points**:
- "In WS1 you understood the architecture. In WS2 you built the workload. Today: how do you run it?"
- This is the operations bridge — the content that makes the difference between a demo and a production system.
- No hands-on labs today — instead: deep demos, patterns, and a production readiness checklist you take away.

**Transition**: "Let's start with the foundation: how do you get code to production safely?"

---

### Module 1: CI/CD for AI Workloads (50 min)

**Owner**: *(GEN AI OPS — George/Guilherme for pipeline content, Arturo for context)*

**Objective**: Show participants how to set up infrastructure and application pipelines for AI workloads.

#### Talking Points — Two Pipelines (10 min)
- Infrastructure pipeline deploys the Landing Zone (Bicep/Terraform)
- Application pipeline deploys the AI workload (container + model config)
- "These are separate concerns — different repos, triggers, and approval gates"

#### Demo — Infrastructure Pipeline (15 min) *(GEN AI OPS — FILL IN)*
- Show: pipeline YAML → trigger on PR merge → lint → validate → what-if → deploy
- Highlight: approval gates between `what-if` and `deploy`
- Point out: Landing Zone modules being composed (networking, identity, compute)
- *TODO: Provide demo pipeline YAML and repo setup instructions*

#### Demo — Application Pipeline (15 min) *(GEN AI OPS — FILL IN)*
- Show: build container → run tests → push to ACR → deploy to Container Apps
- Highlight: model evaluation step (groundedness, relevance scoring)
- Point out: environment promotion (dev → staging → prod)
- *TODO: Provide demo pipeline YAML and sample test suite*

#### Discussion — Testing AI Workloads (10 min)
- "What's different about testing AI vs. traditional apps?"
- Facilitate: unit tests (deterministic) vs. evaluation tests (probabilistic)
- Key insight: you can't assert exact outputs, but you can score quality ranges
- Prompt versioning: "Treat your system prompt like a config file — version it"

**Transition**: "You can deploy reliably. Now: how do you know it's working?"

---

### Module 2: Production Monitoring & Observability (45 min)

**Owner**: *(GEN AI OPS — George/Guilherme for monitoring patterns, Arturo for agent observability)*

**Objective**: Teach participants the AI monitoring pyramid and how to build dashboards + alerts.

#### Talking Points — Monitoring Pyramid (10 min)
- Layer 1 (base): Infrastructure health — compute, memory, disk, network
- Layer 2: Model quality — latency, token consumption, error rate
- Layer 3: User experience — response relevance, task completion, escalation rate
- Layer 4 (top): Business KPIs — adoption, time saved, cost per resolution
- "Most teams only monitor Layer 1. Production readiness requires all four."

#### Demo — Monitoring Dashboard (15 min) *(GEN AI OPS — FILL IN)*
- Show: Application Insights overview → requests, failures, latency
- Show: Log Analytics queries → KQL for token usage, error categorization
- Show: Azure Workbook or dashboard → key metrics at a glance
- *TODO: Provide sample KQL queries and Workbook template*

#### Talking Points — Agent Observability (10 min)
- Agent monitoring adds: tool call tracking, reasoning chain tracing, escalation monitoring
- "If you deploy agents, you MUST trace the full decision path"
- Show: AI Foundry tracing (if available) or Application Insights custom events
- Reference: [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)

#### Exercise — Define Your Alerts (10 min)
- Table exercise: participants define 5 alert rules for their workload
- Provide template: Metric | Threshold | Severity | Action
- Share: common pitfalls (alert fatigue, missing quality alerts)
- Debrief: "Did anyone include a response quality alert? A cost alert?"

**Transition**: "You can deploy and monitor. Now: who controls what the agent can do?"

---

### Module 3: Agent Governance & Security (45 min)

**Owner**: *(Arturo for CAF governance framework, GEN AI OPS for operational enforcement)*

**Objective**: Establish agent governance as a first-class operational concern.

#### Talking Points — CAF Govern & Secure Phase (10 min)
- 4-phase lifecycle: Plan → **Govern & Secure** → Build → Manage
- "Governance happens BEFORE you deploy to production"
- Key questions: What data can the agent access? What tools can it invoke? When must it escalate?
- Reference: [CAF Govern & Secure](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)

#### Interactive Discussion — Data & Tool Boundaries (15 min)
- Present scenario: "Your agent can search a knowledge base AND submit expense reports"
- Ask: "What boundaries would you set?"
- Facilitate: least privilege, tool allowlists, rate limits, sensitive action policies
- Draw on whiteboard/slide: data access matrix per agent type
  - Productivity agent: read-only, curated knowledge bases
  - Action agent: read + specific write APIs, with rate limits
  - Automation agent: broader access, requires human approval gates

#### Talking Points — Responsible AI & Audit (10 min)
- Content filtering: Azure AI Content Safety integration
- Grounding enforcement: agents must cite sources or decline
- Audit trail: every tool call, every data access, every escalation → logged
- "In regulated industries, this is not optional — and in 2026, it's expected everywhere"

#### Facilitated Exercise — Governance Matrix (10 min) *(GEN AI OPS — FILL IN)*
- Participants build a governance matrix for their agent scenario:
  | Agent Type | Data Access | Tools Allowed | Escalation Policy | Audit Level |
  |------------|-------------|---------------|--------------------|-------------|
  | ... | ... | ... | ... | ... |
- Debrief 2-3 examples with the group
- *TODO: Provide blank template and 1 filled example*

**Transition**: "Governance protects you. Now: cost optimization ensures sustainability."

---

### Module 4: Cost Optimization & Scaling (30 min)

**Owner**: *(Arturo for cost model, GEN AI OPS for scaling patterns)*

**Objective**: Help participants understand AI cost drivers and optimization levers.

#### Talking Points — Cost Model (10 min)
- Walk through the 5 cost components: model inference, AI Search, compute, storage, networking
- "Model inference is usually 50-70% of your AI workload cost"
- Quick math: show cost of 10K req/day at different model tiers

#### Talking Points — Optimization Levers (10 min)
- Model selection: route simple queries to smaller/cheaper models
- Prompt engineering: shorter prompts = fewer tokens = lower cost
- Caching: identical queries → cached responses (save 100% of model cost)
- Right-sizing: don't overprovision search replicas or compute
- Provisioned throughput vs. pay-as-you-go: when each makes sense

#### Talking Points — Tagging & Showback (10 min) *(GEN AI OPS — FILL IN)*
- Tagging strategy: environment, team, project, workload
- Azure Cost Management: budgets, alerts, cost analysis
- Per-request cost tracking: how to calculate and log cost per API call
- "If you can't measure it, you can't optimize it"
- *TODO: Add sample tagging policy and Cost Management budget setup*

**Transition**: "Let's pull it all together into a production readiness plan."

---

### Module 5: Wrap-up & Production Planning (25 min)

**Owner**: *(Arturo — lead, all team contribute)*

**Objective**: Give participants a concrete production readiness checklist and next steps.

#### Production Readiness Checklist (10 min)
- Walk through the full checklist (Slide 31)
- "This is what you take away today. This is the bar for production."
- Highlight the items most often missed: responsible AI review, load testing, incident response plan

#### Operational Runbook Template (5 min)
- Show the runbook template structure
- Emphasize: agent-specific failure modes are NEW — they don't exist in your current runbooks
- "Tool failures, hallucination spikes, and model degradation are incidents now"

#### Workshop Series Recap & Next Steps (5 min)
- The 3-workshop journey: Understand → Build → Operate
- "You now have the full toolkit to take partners from concept to production"
- Mention: additional resources, office hours, community channels

#### Q&A & Close (5 min)
- Open floor for questions
- Distribute feedback survey
- Thank participants

---

## Troubleshooting Guide

| Issue | Mitigation |
|-------|------------|
| Attendees haven't done WS2 | Share WS2 recap handout at start; focus on concepts over hands-on |
| Demo pipeline fails live | Have pre-recorded run screenshots/video as backup |
| Monitoring workspace has no data | Pre-seed with synthetic telemetry 24h before workshop |
| Agent governance feels abstract | Use the 3 agent scenarios from WS1 Slide 43 as concrete examples |
| Cost discussion gets vendor-specific | Redirect to Azure-native tools; acknowledge multi-cloud exists |
| Time running short | Cut Module 4 exercises; deliver as talking points instead |

---

## Time Adaptation

### Compressed: 3 hours
- Module 1: 40 min (cut one demo, merge into single pipeline walkthrough)
- Module 2: 35 min (cut exercise, demo only)
- Module 3: 35 min (cut facilitated exercise, present governance matrix as example)
- Module 4: 20 min (talking points only, no exercise)
- Module 5: 15 min (checklist + close)
- Breaks: 2 × 7 min

### Extended: 5+ hours
- Add hands-on lab: participants set up a pipeline for a sample repo
- Add hands-on lab: participants build an Azure Workbook from KQL queries
- Add group exercise: build full governance matrix and present to room
- Add deep dive: multi-agent orchestration patterns and security

---

## Post-Workshop Deliverables
- [ ] Distribute slide deck PDF
- [ ] Share production readiness checklist (standalone format)
- [ ] Share link to AI Landing Zones repo
- [ ] Share governance matrix template
- [ ] Collect and review feedback survey results
- [ ] *(GEN AI OPS — FILL IN)* Share pipeline YAML templates, KQL queries, Workbook templates

---

**Authors**: Arturo Quiroga (PSA), Ana Lopez Moreno (PSA), George Bittencourt (PSA) & Guilherme Nogueira (PSA)  
**Created**: February 25, 2026  
**Status**: 📋 Scaffold — Awaiting Gen AI OPS team input
