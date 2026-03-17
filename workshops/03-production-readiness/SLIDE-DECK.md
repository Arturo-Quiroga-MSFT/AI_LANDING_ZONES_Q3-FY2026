---
marp: true
theme: default
paginate: true
backgroundColor: #fff
color: #333
style: |
  section {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  h1 {
    color: #0078D4;
  }
  h2 {
    color: #0078D4;
    border-bottom: 2px solid #0078D4;
    padding-bottom: 8px;
  }
  h3 {
    color: #005A9E;
  }
  table {
    font-size: 0.8em;
    width: 100%;
  }
  th {
    background-color: #0078D4;
    color: white;
  }
  blockquote {
    border-left: 4px solid #D83B01;
    background: #FFF4CE;
    padding: 12px 20px;
    font-size: 0.9em;
  }
  a {
    color: #0078D4;
  }
  .columns {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  footer {
    font-size: 0.6em;
    color: #666;
  }
  section.title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  section.title h1 {
    font-size: 2.5em;
    margin-bottom: 0;
  }
  section.title h3 {
    color: #666;
    font-weight: normal;
  }
  .warning {
    background: #FFF4CE;
    border-left: 4px solid #D83B01;
    padding: 12px 20px;
    margin: 10px 0;
  }
  .key-point {
    background: #E8F4FD;
    border-left: 4px solid #0078D4;
    padding: 12px 20px;
    margin: 10px 0;
  }
  code {
    background: #f0f0f0;
    padding: 2px 6px;
    border-radius: 3px;
    font-size: 0.85em;
  }
  pre code {
    background: #1e1e1e;
    color: #d4d4d4;
    padding: 16px;
    border-radius: 6px;
    font-size: 0.75em;
  }
---

<!-- _class: title -->
<!-- _paginate: false -->

# Landing Zones to Production
### The GenAIOps Bridge
#### Partner Enablement Workshop (Advanced)

AI Center of Excellence V2 | Q3 FY2026

---

## Agenda

| Time | Module | Description |
|------|--------|-------------|
| 0:00 | Welcome & Context | Workshop 2 recap, production readiness gap |
| 0:15 | **Module 1** | **CI/CD for AI Workloads** |
| 1:05 | ☕ Break | 10 minutes |
| 1:15 | **Module 2** | **Production Monitoring & Observability** |
| 2:00 | ☕ Break | 10 minutes |
| 2:10 | **Module 3** | **Agent Governance & Security** |
| 2:55 | ☕ Break | 10 minutes |
| 3:05 | Module 4 | Cost Optimization & Scaling |
| 3:35 | Module 5 | Wrap-up & Production Planning |

---

## Where We Are in the Journey

```
  WS1: UNDERSTAND           WS2: BUILD              WS3: OPERATE ← you are here
  ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────────┐
  │  Concepts         │  →  │  Deploy LZ        │  →  │  CI/CD               │
  │  Architectures    │     │  RAG App          │     │  Monitoring          │
  │  Decision         │     │  Explore Agents   │     │  Governance          │
  │  Frameworks       │     │                   │     │  Cost & Scale        │
  └──────────────────┘     └──────────────────┘     └──────────────────────┘
```

**You have a deployed workload. Now: how do you run it in production?**

> Deploying is Day 1. Operating is Day 2 through Day N.

---

<!-- _class: title -->

# Module 1
### CI/CD for AI Workloads

---

## The Two Pipelines

AI workloads require **two separate CI/CD pipelines**:

<div class="columns">
<div>

### Infrastructure Pipeline
- Deploys/updates Landing Zone
- Bicep or Terraform
- Trigger: PR merge to `infra/`
- Changes: networking, identity, PaaS config
- Slower cadence, higher risk

</div>
<div>

### Application Pipeline
- Builds/deploys AI app
- Container build + model config
- Trigger: PR merge to `src/`
- Changes: app code, prompts, model versions
- Faster cadence, more frequent

</div>
</div>

These are **separate pipelines** with different triggers and approval gates.

---

## Infrastructure Pipeline Pattern

```yaml
# Trigger: PR merge to infra/
steps:
  - Lint (bicep lint / terraform validate)
  - Validate (bicep build / terraform plan)
  - What-if / Plan (preview changes)
  - Approve (manual gate)
  - Deploy (bicep deploy / terraform apply)
```

**Key practices:**
- Preview all changes before applying (`what-if` / `plan`)
- Manual approval gate before production
- Immutable deployments — no manual portal changes
- IaC drift detection on schedule

---

## Application Pipeline Pattern

```yaml
# Trigger: PR merge to src/
steps:
  - Build container image
  - Run unit tests
  - Run model evaluation (groundedness, relevance)
  - Push to Azure Container Registry
  - Deploy to Container Apps (staging)
  - Integration tests
  - Approve (manual gate)
  - Deploy to Container Apps (production)
```

**Key addition**: Model evaluation step **before** production deploy.

---

## Model Deployment & Versioning

| What to Version | Strategy |
|-----------------|----------|
| **Model** | Track model name + version (e.g., gpt-4o-2024-08-06) |
| **System prompts** | Store in repo as code, version with git |
| **RAG configuration** | Index schema, chunking strategy, embedding model |
| **Parameters** | Temperature, top-p, max tokens as config files |

**Deployment patterns:**
- Blue/green for model swaps — test before cutover
- Canary: route 5% traffic to new model, monitor, then promote
- Rollback: always keep previous version deployable

---

## Testing AI Workloads

| Test Level | What It Tests | Tools |
|------------|--------------|-------|
| **Unit tests** | Deterministic logic, API contracts | pytest, Jest |
| **Integration tests** | End-to-end flow: query → search → model → response | Custom test harness |
| **Model evaluation** | Response quality, groundedness, relevance | AI Foundry evaluation |
| **Load testing** | Token throughput, latency under concurrency | Azure Load Testing, k6 |

<div class="key-point">

**Critical**: Model evaluation is not optional. A code change that passes unit tests can still degrade response quality if prompts or context change.

</div>

---

## Environments & Promotion

```
  Dev                    Staging                  Production
  ┌──────────────┐      ┌──────────────┐        ┌──────────────┐
  │  Experiment   │  →   │  Validate     │   →    │  Serve        │
  │  Iterate      │      │  Load test    │        │  Monitor      │
  │  Lower SKUs   │      │  Model eval   │        │  Full SKUs    │
  └──────────────┘      └──────────────┘        └──────────────┘
        auto                  auto + gate              gate
```

- Environment-specific parameters: model SKU, search tier, network config
- Approval gates between staging → production
- Feature flags for gradual rollout of new agent capabilities
- **Same IaC templates** across all environments, different parameter files

---

## Key Takeaways — Module 1

- ✅ Separate infrastructure and application pipelines
- ✅ Treat prompts and model config as versioned code
- ✅ Test AI workloads at multiple levels (unit → integration → model eval → load)
- ✅ Automate deployments but gate production promotions
- ✅ Blue/green or canary for model swaps — never yolo to production

---

<!-- _class: title -->

# ☕ Break
### 10 minutes

---

<!-- _class: title -->

# Module 2
### Production Monitoring & Observability

---

## Monitoring Stack Overview

| Tool | What It Covers |
|------|---------------|
| **Application Insights** | Request tracing, errors, latency, dependencies |
| **Log Analytics** | Centralized logs, KQL queries, diagnostic settings |
| **AI Foundry Tracing** | Model-level call traces, token usage, response quality |
| **Azure Workbooks / Grafana** | Custom dashboards |
| **Azure Monitor Alerts** | Proactive notification |

All of these are **already deployed** from your `azd up` in Workshop 2 — now we configure them for production.

---

## The AI Monitoring Pyramid

```
                    ┌───────────────┐
                    │  Business KPIs │
                    └───────┬───────┘
                ┌───────────┴───────────┐
                │    Model Quality      │
                │   User Experience     │
                └───────────┬───────────┘
          ┌─────────────────┴─────────────────┐
          │  Infrastructure Health             │
          │  Cost Metrics                      │
          └───────────────────────────────────┘
```

**Monitor bottom-up**: Infrastructure health → Model quality → Business value

If infrastructure is degraded, model metrics are meaningless. If model quality drops, business KPIs will follow.

---

## Key Metrics Dashboard

| Category | Metric | Target |
|----------|--------|--------|
| **Latency** | Response P50 / P95 / P99 | < 2s / < 5s / < 10s |
| **Tokens** | Prompt + completion per request | Monitor trend |
| **Cost** | Cost per 1K requests | < budget threshold |
| **Errors** | Error rate by category | < 1% |
| **Retrieval** | % relevant search results | > 80% |
| **Availability** | Uptime % | > 99.5% |

<div class="key-point">

Build a single dashboard that shows all of these. If you can't see it at a glance, you won't catch degradation early.

</div>

---

## Agent-Specific Observability

When running AI agents (vs. classic RAG), monitor additional dimensions:

- **Tool call monitoring** — which tools called, success/failure rate, latency per tool
- **Reasoning chain tracing** — full decision path per request (why did the agent choose this tool?)
- **Escalation tracking** — when agent hands off to human, frequency, reasons
- **Drift detection** — are agent behaviors changing over time? New tool patterns emerging?

📚 [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)

---

## Alerting Rules

| Alert | Threshold | Severity |
|-------|-----------|----------|
| Response latency P95 | > 5000 ms | ⚠️ Warning |
| Error rate | > 2% sustained 5 min | 🔴 Critical |
| Token budget | > 80% of daily limit | ⚠️ Warning |
| Model drift score | > threshold | ⚠️ Warning |
| Availability | < 99.5% in 1 hour | 🔴 Critical |
| Hallucination rate | > 5% of responses | 🔴 Critical |

> **Tune thresholds to your workload**. These are starting points. Review and adjust after the first 2 weeks of production data.

---

## SLA Definition for AI Workloads

Traditional SLAs (uptime %) are **insufficient** for AI. Add quality dimensions:

| SLA Type | Metric | Example Target |
|----------|--------|---------------|
| **Availability** | Uptime % | 99.5% |
| **Latency** | P95 response time | < 5 seconds |
| **Quality** | % grounded responses | > 95% |
| **Cost** | Max cost per 1K requests | < $X |
| **Agent** | % tasks completed without escalation | > 85% |

<div class="key-point">

**Partner talking point**: "Your AI SLA should include response quality, not just uptime. A system that's 100% available but gives wrong answers has a worse SLA than one with 99.5% uptime and great quality."

</div>

---

## Key Takeaways — Module 2

- ✅ AI monitoring = traditional monitoring + model-specific metrics
- ✅ Build dashboards around the monitoring pyramid (infra → model → business)
- ✅ Define SLAs that include quality, not just availability
- ✅ Agent workloads need tool call and reasoning observability
- ✅ Alerting thresholds are starting points — tune with production data

---

<!-- _class: title -->

# ☕ Break
### 10 minutes

---

<!-- _class: title -->

# Module 3
### Agent Governance & Security

---

## CAF Govern & Secure Phase

The 4-phase CAF AI Agent lifecycle:

```
  Plan  →  Govern & Secure  →  Build  →  Manage
                  ↑
            YOU ARE HERE
```

**This phase happens BEFORE you build agents in production.**

Governance is not an afterthought — it's a prerequisite.

📚 [CAF Govern & Secure](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)

---

## Data Access Controls

**What data can each agent access?**

- Apply **principle of least privilege** to agent data access
- Classify data sources: which are agent-accessible, which are not
- Implement row-level and document-level security in AI Search
- Separate agent data stores from human-facing data where needed

| Control | Implementation |
|---------|---------------|
| Document-level | AI Search security filters |
| Row-level | Cosmos DB resource tokens |
| Service-level | RBAC per managed identity |
| Network-level | Private endpoints, NSGs |

---

## Tool Permission Boundaries

**Which APIs/tools can each agent invoke?**

| Agent Type | Allowed Tools | Restrictions |
|------------|--------------|-------------|
| **Productivity** | AI Search, knowledge base | Read-only, no external calls |
| **Action** | Specific APIs, ticketing, CRM | Allowlisted endpoints, rate-limited |
| **Automation** | Full orchestration suite | Budget caps, approval for sensitive ops |

**Key practices:**
- Tool allowlists per agent type — default deny
- Rate limiting and budget caps per tool
- Approval workflows for sensitive tool operations (financial, PII, deletion)

---

## Human-in-the-Loop Policies

**When must agents escalate to humans?**

- **Confidence threshold** — agent is uncertain about intent or correct action
- **Sensitive actions** — financial transactions, PII processing, data deletion
- **Compliance triggers** — regulated actions require human approval
- **Accumulated risk** — multiple borderline decisions in one session

<div class="warning">

**Design decision, not afterthought**: Human-in-the-loop policies must be defined BEFORE agents are deployed to production. Retrofitting is expensive and risky.

</div>

> Audit and log every escalation decision — both escalated and not-escalated.

---

## Responsible AI Guardrails

| Guardrail | Purpose | Tool |
|-----------|---------|------|
| **Content filtering** | Block unsafe outputs | Azure AI Content Safety |
| **Grounding enforcement** | Agents must cite sources | System prompt + evaluation |
| **Hallucination detection** | Flag ungrounded responses | AI Foundry evaluation |
| **Bias monitoring** | Detect unfair decision patterns | Custom metrics + dashboards |

**Design Checklist alignment:**
- S-R4: MITRE ATLAS + OWASP for AI risks
- S-R5: AI Content Safety for outputs
- G-R3: Responsible AI dashboard

📚 [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/)

---

## Multi-Agent Security

**Additional security considerations when running multiple agents:**

<div class="columns">
<div>

### Must Have
- Credential isolation between agents
- Per-agent managed identities
- Separate RBAC scopes
- Network segmentation

</div>
<div>

### Must Design
- Cross-boundary trust models
- State synchronization security
- Inter-agent communication auth
- Shared resource access patterns

</div>
</div>

> **When NOT to use multi-agent**: If the added complexity doesn't justify the value. Most workloads start fine with a single agent.

---

## Agent Audit Trail

**Log everything the agent does:**

- Every tool call (input, output, latency)
- Every data access (what was queried, what was returned)
- Every decision (why this tool, why this response)
- Every escalation (to whom, why, outcome)
- Every output (what was sent to the user)

**Retention**: Follow your organization's compliance requirements (min 90 days recommended)

**Forensics**: You must be able to reconstruct any agent decision chain after the fact.

---

## Key Takeaways — Module 3

- ✅ Governance before deployment, not after
- ✅ Least privilege for data access and tool permissions
- ✅ Human-in-the-loop is a design decision, not an afterthought
- ✅ Responsible AI guardrails are mandatory, not optional
- ✅ Audit everything — tool calls, decisions, escalations, outputs

**Exercise**: Walk through Design Checklist governance (G-R1 to G-R5) and security (S-R1 to S-R5) sections against your deployed environment.

---

<!-- _class: title -->

# ☕ Break
### 10 minutes

---

<!-- _class: title -->

# Module 4
### Cost Optimization & Scaling

---

## AI Workload Cost Model

| Cost Component | Driver | Optimization Lever |
|---------------|--------|-------------------|
| **Model inference** | Tokens (prompt + completion) | Smaller models, shorter prompts, caching |
| **AI Search** | Tier + query volume | Right-size tier, optimize index |
| **Compute** | Container App instances | Autoscaling, right-size SKU |
| **Storage** | Document + chat history | Lifecycle policies, archive old data |
| **Networking** | Private endpoints, egress | Minimize cross-region traffic |

📚 [AI Landing Zones Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md) | [Pricing Calculator Estimate](https://azure.com/e/e92e102172054654a13cdc1cada6cecc)

---

## Model Selection Economics

| Model | Relative Cost | Best For |
|-------|-------------|---------|
| GPT-4o | $$$ | Complex reasoning, multi-step tasks |
| GPT-4o-mini | $$ | Most production workloads, good cost/quality |
| GPT-3.5-turbo | $ | Simple queries, high volume, low latency |

**Optimization strategies:**
- **Route** simple queries to smaller models, complex to larger
- **Cache** responses for common/repeated queries
- **Optimize prompts** — reduce token count without losing quality
- **Right-size context** — don't stuff the full document when a summary suffices

> Model selection is the single biggest cost lever for AI workloads.

---

## Scaling Patterns

| Component | Scaling Mechanism | Key Config |
|-----------|------------------|------------|
| **Container Apps** | HTTP-based, KEDA, custom | Min/max replicas, scale rules |
| **Azure OpenAI** | PTU (reserved) vs. PAYGO | PTU for predictable load, PAYGO for bursts |
| **AI Search** | Replica scaling | Read replicas for query throughput |
| **Cosmos DB** | Autoscale RUs | Min/max RUs, partition key design |

<div class="key-point">

**PTU vs. PAYGO**: Use Provisioned Throughput Units for predictable baseline traffic. Use pay-as-you-go for spikes. Combine both for optimal cost.

</div>

---

## Cost Allocation & Showback

**From Day 1, tag everything:**

| Tag | Purpose | Example |
|-----|---------|---------|
| `team` | Cost allocation | `team:ai-platform` |
| `project` | Project tracking | `project:customer-support-agent` |
| `environment` | Env separation | `environment:production` |
| `workload` | Workload type | `workload:rag-chat` |

- Set up **Azure Cost Management budgets and alerts** per tag group
- Track **per-request cost**: tokens × price per token
- Build chargeback models for shared AI infrastructure
- Review costs weekly during first month, monthly after

---

## Key Takeaways — Module 4

- ✅ Understand the cost model before deploying to production
- ✅ Model selection is the biggest cost lever
- ✅ Autoscale everything, right-size everything
- ✅ Combine PTU + PAYGO for optimal model inference cost
- ✅ Tag resources for showback from day one

---

<!-- _class: title -->

# Module 5
### Wrap-up & Production Planning

---

## Production Readiness Checklist

| Area | Item | Status |
|------|------|--------|
| CI/CD | Infrastructure pipeline (Bicep/Terraform) | ☐ |
| CI/CD | Application pipeline (build, test, deploy) | ☐ |
| CI/CD | Model evaluation in pipeline | ☐ |
| Monitoring | Dashboards configured (metrics pyramid) | ☐ |
| Monitoring | Alerting rules active | ☐ |
| Governance | Agent data access policies defined | ☐ |
| Governance | Tool permission boundaries enforced | ☐ |
| Governance | Human-in-the-loop policies configured | ☐ |
| Governance | Responsible AI review completed | ☐ |
| Cost | Budgets and scaling limits set | ☐ |
| Operations | Operational runbooks documented | ☐ |
| Operations | Incident response plan defined | ☐ |
| Security | Load testing passed | ☐ |
| Security | Security review completed | ☐ |

---

## Operational Runbook Template

| Element | Details |
|---------|---------|
| **Incident classification** | P1-P4 for AI workloads |
| **AI failure modes** | Tool failures, model degradation, hallucination spike |
| **Escalation paths** | On-call rotation, subject matter experts |
| **Recovery procedures** | Per failure type: rollback model, restart service, failover |
| **Post-incident review** | Root cause, impact, remediation, prevention |

<div class="key-point">

**Agent-specific failures** that traditional runbooks don't cover: tool invocation failures, reasoning loops, confidence collapse, escalation floods. Document how to handle each.

</div>

---

## The Full Journey — Workshop Series Recap

| Workshop | Theme | Outcome |
|----------|-------|---------|
| **WS1** | Understand | Architecture decisions, design checklist, deployment paths |
| **WS2** | Build | Deployed Landing Zone, RAG app, agent exploration |
| **WS3** | Operate | CI/CD, monitoring, governance, cost optimization |

**Partner outcome**: End-to-end capability to take customers from concept to production.

> You now have the architecture knowledge (WS1), hands-on deployment skill (WS2), and operational readiness (WS3) to guide any customer through an AI Landing Zone engagement.

---

## Key Resources

| Resource | Link |
|----------|------|
| AI Landing Zones Repo | [github.com/Azure/AI-Landing-Zones](https://github.com/Azure/AI-Landing-Zones) |
| Design Checklist | [AI-Landing-Zones-Design-Checklist.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Cost Guide | [AI-Landing-Zones-Cost-Guide.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md) |
| CAF AI Agent Adoption | [learn.microsoft.com](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) |
| CAF Govern & Secure | [learn.microsoft.com](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure) |
| CAF Manage Agents | [learn.microsoft.com](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage) |
| Azure Monitor Baseline Alerts | [azure.github.io](https://azure.github.io/azure-monitor-baseline-alerts/) |
| Partner Quick Reference | [PARTNER-QUICK-REFERENCE.md](../../docs/PARTNER-QUICK-REFERENCE.md) |

---

<!-- _class: title -->

# Q&A

### Questions? Feedback?

AI Center of Excellence V2 | Partner Enablement Team

---

<!-- _paginate: false -->

## Thank You

**Workshop Materials**: Available in the partner repository

**Feedback**: Survey link in chat

**Contact**: Arturo Quiroga (PSA) | Anahita Afshari (PSA)

AI Center of Excellence V2 | Q3 FY2026
