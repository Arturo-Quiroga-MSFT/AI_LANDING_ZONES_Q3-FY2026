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

# From RAG to Agents
### Deploying Your First Gen AI Workload
#### Partner Enablement Workshop (Hands-On)

AI Center of Excellence V2 | Q3 FY2026

---

## Agenda

| Time | Module | Description |
|------|--------|-------------|
| 0:00 | Welcome & Setup | Verify prerequisites, agenda |
| 0:15 | Module 1 | Quick Recap & Deployment Strategy |
| 0:35 | **Module 2** | **Deploy the Landing Zone (HANDS-ON)** |
| 1:35 | ☕ Break | 15 minutes |
| 1:50 | **Module 3** | **Configure & Deploy RAG App (HANDS-ON)** |
| 2:30 | Module 4 | From RAG to Agents |
| 3:00 | Module 5 | Monitoring & Observability |
| 3:20 | Module 6 | Wrap-up & Next Steps |

---

## Learning Objectives

After this workshop you will be able to:

- **Deploy** a complete AI Landing Zone using `azd up`
- **Configure** AI Foundry with standard (private) setup
- **Deploy** a sample RAG chat application end-to-end
- **Distinguish** RAG vs. AI agents in practice
- **Explore** Microsoft Foundry agent capabilities
- **Implement** basic monitoring and observability
- **Assess** when a customer should graduate from RAG to agents

---

## Setup Validation Checklist

**Run these now — raise your hand if anything fails:**

```bash
az --version          # Need 2.61.0+
azd version           # Need 1.15.0+
az account show       # Must be logged in
az cognitiveservices usage list --location eastus2 -o table  # Check quota
```

- [ ] Azure CLI ≥ 2.61.0
- [ ] Azure Developer CLI ≥ 1.15.0
- [ ] Logged in to correct subscription
- [ ] Sufficient OpenAI quota in target region
- [ ] Owner or Contributor + UAA role

> **If anything fails**: Pair with a neighbor, or follow along with the instructor demo

---

<!-- _class: title -->

# Module 1
### Quick Recap & Deployment Strategy

---

## Workshop 1 Recap (60-Second Version)

- **AI Landing Zone** = production-ready application landing zone for AI workloads
- **Two architectures**: with Platform LZ (enterprise) / without (standalone)
- **Design Checklist**: 40+ recommendations across 10 design areas
- **Four deployment paths**: azd, Bicep, Terraform, Portal (Deploy to Azure)

**Today**: We deploy and build on top of this foundation

📚 [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) | [Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md)

---

## Today's Narrative — RAG to Agents

```
  Deploy Infrastructure    Build Baseline Workload    Explore What's Next    Operate
  ┌──────────────────┐    ┌──────────────────────┐   ┌─────────────────┐   ┌─────────────┐
  │  AI Landing Zone │ →  │   Classic RAG App     │ → │   AI Agents     │ → │  Monitoring  │
  │  (azd up)        │    │   (chat + search)     │   │   (when ready)  │   │  & Ops       │
  └──────────────────┘    └──────────────────────┘   └─────────────────┘   └─────────────┘
```

**The key question partners must answer:**
> Does this customer need agents, or is RAG enough?

---

## What Gets Deployed (~30+ Resources)

| Layer | Resources |
|-------|-----------|
| **AI Services** | AI Foundry (hub + project), Azure OpenAI, AI Search |
| **Data** | Cosmos DB (chat history), Storage Account (documents) |
| **Compute** | Container Apps (app runtime) |
| **Security** | Key Vault, Managed Identities, Private Endpoints, NSGs |
| **Networking** | Virtual Network, Subnets, Private DNS Zones |
| **Monitoring** | Log Analytics, Application Insights |
| **Governance** | Microsoft Fabric, Microsoft Purview |

All deployed with security-first defaults: **no public endpoints, managed identity, RBAC**

---

## Today's Architecture — Without Platform LZ

**Why standalone for this lab:**
- Faster deployment, self-contained, no hub dependency
- Same security controls apply — private endpoints, managed identity
- In production: enterprise customers use the "with platform LZ" variant

**Key insight**: The architecture is the same. The difference is whether networking and identity are shared (platform) or self-contained (standalone).

📚 [Architecture diagrams](https://github.com/Azure/AI-Landing-Zones#reference-architectures)

---

## Deployment Path — Why azd up

| Consideration | azd up | Bicep | Terraform |
|--------------|--------|-------|-----------|
| **Speed** | ~45 min | ~30-60 min | ~30-60 min |
| **Setup** | Minimal | Moderate | Moderate |
| **Customization** | Limited | Full | Full |
| **Best for** | Labs, PoCs | Production (Azure-native) | Production (multi-cloud) |

Today we use `azd up` for speed — partners should use Bicep/Terraform for customer deployments

📚 [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)

---

<!-- _class: title -->

# Module 2
### Deploy the Landing Zone
#### 🔬 HANDS-ON LAB (~60 min)

---

## Lab Overview

- **Goal**: Deploy a complete AI Landing Zone with ~30 Azure resources
- **Time**: ~60 minutes (including deployment wait time)
- **Steps**: Clone → Configure → Deploy → Validate
- **During deployment** (~30-45 min wait): Guided Portal walkthrough

> ⚠️ **Cost Warning**: Standard deployment costs ~$2,128-3,098/month. **Delete all resources after the workshop!** See [Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md)

---

## Step 1 — Clone the Repository

```bash
git clone --recurse-submodules \
  https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git

cd Deploy-Your-AI-Application-In-Production
```

- `--recurse-submodules` is critical — pulls in Bicep modules
- Review the repo structure: `/infra`, `/docs`, `/src`

---

## Step 2 — Initialize and Configure

```bash
azd init
```

**Key parameters to set:**
- **Environment name**: Use workshop naming convention
- **Region**: Choose based on quota availability
- **Resource naming prefix**: Differentiate from other deployments
- **SKU selections**: Balance cost vs. capability

📚 [Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md) | [Roles & Scopes](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md)

---

## Step 3 — Deploy

```bash
azd up
```

**What's happening behind the scenes (~30-45 min):**

1. Bicep templates compiled
2. Resource group created
3. Networking deployed (VNet, subnets, NSGs)
4. PaaS services deployed with private endpoints
5. RBAC assignments configured
6. Application code deployed to Container Apps

**While we wait → let's explore what's being built...**

---

## Portal Walkthrough — Networking Layer

*Show during deployment wait time*

**What to look for in the Portal:**
- Virtual network and subnet structure
- Private endpoints — **no public IP addresses**
- NSG rules — default deny, explicit allow
- Private DNS zones for PaaS services

**Design Checklist validation:**
- ✅ N-R3: Private Endpoints for all PaaS services
- ✅ N-R4: NSGs on all subnets
- ✅ N-R8: Private DNS zones configured

---

## Portal Walkthrough — AI Services Layer

*Show during deployment wait time*

**What to look for in the Portal:**
- AI Foundry hub and project structure
- Azure OpenAI deployments and model endpoints
- AI Search index configuration
- Cosmos DB for chat history storage

**Design Checklist validation:**
- ✅ D-R1: Thread/chat storage (Cosmos DB)
- ✅ D-R2: File storage (Storage Account)

---

## Portal Walkthrough — Security Layer

*Show during deployment wait time*

**What to look for in the Portal:**
- Managed identities — no credentials in code
- Key Vault for secrets management
- RBAC assignments — least privilege
- Defender for Cloud recommendations

**Design Checklist validation:**
- ✅ I-R1: Managed Identity throughout
- ✅ I-R3: Entra ID for authentication (not API keys)
- ✅ S-R1: Defender for Cloud enabled

---

## Step 4 — Validate Deployment

```bash
azd show
```

**Verify in the Portal:**
- [ ] All resources created in resource group
- [ ] Private endpoints active and connected
- [ ] RBAC assignments correct
- [ ] No public endpoints exposed
- [ ] Diagnostic settings configured

> **Troubleshooting**: If deployment failed, check quota limits, region availability, and role assignments. Run `azd down` and retry with adjusted parameters.

---

## Key Takeaways — Module 2

- ✅ A complete production-ready Landing Zone in ~45 minutes
- ✅ Security-first by default (private endpoints, MI, RBAC)
- ✅ Design Checklist items are already implemented in the templates
- ✅ This is what partners should demonstrate to customers

**The infrastructure is deployed. Now let's build a workload on it.**

---

<!-- _class: title -->

# ☕ Break
### 15 minutes — we'll resume with Module 3

---

<!-- _class: title -->

# Module 3
### Configure & Deploy RAG Application
#### 🔬 HANDS-ON LAB (~40 min)

---

## RAG Application Architecture

```
User Query → Container App → AI Foundry → AI Search (retrieve)
                                               ↓
                                         Document Index
                                         (embeddings)
                                               ↓
                                    OpenAI (generate) → Response
```

- **Retrieval**: AI Search finds relevant document chunks via vector search
- **Augmentation**: Retrieved context is added to the LLM prompt
- **Generation**: OpenAI model generates the grounded response

This is **deterministic retrieval** — same query returns similar results every time

---

## Step 1 — Configure AI Foundry

Navigate to **AI Foundry** in the Portal:

1. Review the project structure (hub → project)
2. Verify model deployments (GPT-4o, embedding model)
3. Check connections to AI Search, Cosmos DB, Storage
4. Confirm private networking is active (standard setup)

**Key concept**: AI Foundry's standard setup with private networking = your Landing Zone

---

## Step 2 — Ingest Sample Data

1. Upload sample documents to Storage Account
2. Configure AI Search indexer
3. Create embeddings for vector search
4. Verify index population and search results

> **Key concept**: Quality of retrieval = quality of responses. Garbage in, garbage out — even with the best model.

---

## Step 3 — Deploy and Test the Chat App

1. Access the Container App endpoint
2. Test with sample queries
3. Observe the RAG pattern in action:
   - Query → Search → Retrieved context → Generated response
   - Responses are **grounded in your data**, not hallucinated

**Try edge cases:**
- Questions outside the data scope
- Ambiguous queries
- Multi-turn conversations (check Cosmos DB chat history)

---

## Step 4 — Understand What's Happening

Open **AI Foundry → Tracing** to see the full request flow:

- **Token usage**: prompt tokens + completion tokens = cost
- **Latency breakdown**: search time + model inference time
- **Important observation**: The flow is **predictable and repeatable**

| Metric | What to Watch |
|--------|--------------|
| Search latency | Is AI Search returning results fast enough? |
| Token count | Are prompts too large? Right-size the context window |
| Response quality | Are retrieved documents relevant? |
| Cost per query | Prompt + completion tokens × model pricing |

---

## When RAG Is Enough

**RAG is sufficient** when:
- ✅ Customer needs document Q&A, knowledge base, FAQ
- ✅ Inputs are well-defined, outputs are predictable
- ✅ Low latency and cost are priorities
- ✅ No need for tool orchestration or multi-step reasoning

> **Partner talking point**: "Not every AI workload needs an agent. Start with RAG and graduate when the use case demands it."

**RAG is the baseline workload** — the one you should lead with for most customer conversations.

---

## Key Takeaways — Module 3

- ✅ RAG is the foundation workload on AI Landing Zones
- ✅ Quality of retrieval directly impacts response quality
- ✅ The Landing Zone provides all the infrastructure RAG needs
- ✅ RAG is predictable, cost-effective, and well-understood
- ✅ Know when RAG is enough before recommending agents

---

<!-- _class: title -->

# Module 4
### From RAG to Agents

---

## The RAG → Agent Spectrum

| | Classic RAG | AI Agent |
|--|------------|----------|
| **Pipeline** | Fixed: query → search → generate | Dynamic: model decides what to do |
| **Tools** | Only retrieval | Retrieval + actions + APIs + functions |
| **Reasoning** | None (template-driven) | Multi-step, conditional, adaptive |
| **Predictability** | High | Lower (nondeterministic) |
| **Cost** | Lower | Higher (more model calls, tool invocations) |
| **Governance** | Simpler | Complex (tool safety, escalation, audit) |

📚 [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)

---

## When to Graduate to Agents

Use the [AI Agent Decision Tree](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents):

**Don't use agents when:**
- Task is structured, predictable, rule-based → **Deterministic code**
- Goal is static knowledge retrieval / Q&A → **Classic RAG**

**Use agents when the task requires:**
- 🔄 **Dynamic decision-making** — multi-step reasoning with conditional logic
- 🔗 **Complex orchestration** — chaining tools, APIs, services together
- 🎯 **Adaptive behavior** — ambiguous inputs, intent interpretation

**Example**: Customer support agent that checks order status, processes returns, AND escalates to human — all in one conversation

---

## Three Agent Types on Your Landing Zone

| Agent Type | What It Does | Adds to Your LZ | Example |
|------------|-------------|-----------------|---------|
| **Productivity** | Retrieve & synthesize | Minimal — similar to RAG | Internal knowledge assistant |
| **Action** | Perform specific tasks | Logic Apps, Functions, APIM | Ticket creation, data updates |
| **Automation** | Multi-step processes | Orchestration, triggers, governance | Supply chain optimization |

**Same Landing Zone foundation** — different workload complexity on top

📚 [CAF AI Agent Types](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)

---

## Microsoft Foundry — Your Agent Platform

**Foundry is what runs on the Landing Zone** you just deployed

| Agent Build Option | Description |
|--------------------|-------------|
| **Declarative agents** | Prompt-based, behavior-driven — simpler to update and version |
| **Hosted agents** | Code-first, custom libraries — full control over logic |
| **Workflows** | Orchestrate multi-agent or multi-step processes |

**Setup alignment**: Foundry's standard setup with private networking = **your Landing Zone**

📚 [Foundry Environment Setup](https://learn.microsoft.com/azure/ai-foundry/agents/environment-setup) | [Technology Plan](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)

---

## Foundry Standard Setup = Your Landing Zone

| Foundry Standard Requirement | AI Landing Zone Provides |
|-----------------------------|------------------------|
| Private networking | ✅ VNet, Private Endpoints, NSGs |
| Managed Identity | ✅ No credentials in code |
| Enterprise data controls | ✅ Purview, Key Vault, RBAC |
| AI Search integration | ✅ Already deployed |
| Cosmos DB for memory | ✅ Already deployed |
| Diagnostic settings | ✅ Log Analytics + App Insights |

> **Key insight**: Partners who deploy the Landing Zone are already set up for Foundry agents. There is no separate infrastructure step.

---

## Single Agent vs. Multi-Agent

**Start with single agent** unless you must separate:

- Crossing security/compliance boundaries
- Multiple teams own separate domains
- Known future growth across business units

| Decision Factor | Single Agent | Multi-Agent |
|----------------|-------------|-------------|
| Complexity | Lower | Higher |
| Latency | Lower | Higher (handoff overhead) |
| Credential mgmt | Simpler | Per-agent credentials |
| State sync | Built-in | Must coordinate |
| Cost | Lower | Higher |

> **Rule of thumb**: Prototype single, test, then decide

📚 [Single vs. Multiple Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents)

---

## Demo — Foundry Agent Playground

*If time and access permits:*

1. Navigate to **AI Foundry → Agents**
2. Create a simple agent with:
   - System instructions
   - Knowledge source (AI Search — already connected!)
   - A tool (e.g., a simple function)
3. Show how the agent **reasons and selects tools dynamically**
4. Compare with the **deterministic RAG flow** from Module 3

> This is the moment partners see the difference between RAG and agents in action

---

## The Partner Conversation Framework

1. **Discovery**: "What problem are you solving? Q&A, task automation, or complex orchestration?"
2. **Qualify**: Use the decision tree — deterministic code, RAG, or agent?
3. **Scope**: Which agent type? Productivity, Action, or Automation?
4. **Architecture**: Single or multi-agent? SaaS or custom build?
5. **Infrastructure**: Deploy AI Landing Zone → configure Foundry standard setup
6. **Iterate**: Start simple (RAG or single agent), validate, then graduate

---

## Key Takeaways — Module 4

- ✅ RAG is a subset of what agents can do — start here
- ✅ Graduate to agents when reasoning and tool orchestration are genuinely needed
- ✅ The Landing Zone you deployed is already agent-ready (Foundry standard setup)
- ✅ Use the decision tree & agent types to qualify customer workloads
- ✅ Start single-agent, prove value, then consider multi-agent

---

<!-- _class: title -->

# Module 5
### Monitoring & Observability

---

## Monitoring AI Workloads — What's Different

Traditional monitoring (CPU, memory, latency) **still applies** — but AI adds new dimensions:

| AI-Specific Monitoring | Why It Matters |
|-----------------------|---------------|
| Token usage & cost tracking | Predict and control spend |
| Response quality & relevance | Detect degradation early |
| Hallucination detection | Trust and safety |
| Model drift over time | Performance regression |
| RAG retrieval quality | Right documents found? |
| **For agents**: tool execution | Are tools being called correctly? |

**Checklist items**: M-R1 (Monitor models, resources, data) through M-R6

---

## What's Already Deployed (from azd up)

| Tool | What It Monitors |
|------|-----------------|
| **Application Insights** | Request tracing, error rates, latency |
| **Log Analytics** | Centralized logs, diagnostic settings |
| **AI Foundry Tracing** | Model call traces, token usage |

**Key metrics to watch:**
- Response latency (P50, P95, P99)
- Token consumption (prompt + completion)
- Error rate by type
- AI Search query performance
- Cosmos DB RU consumption

---

## AI Foundry Tracing Walkthrough

1. Open **AI Foundry → Tracing**
2. Find a trace from the RAG query you ran in Module 3
3. Inspect the full chain:
   - Search query → document retrieval → prompt construction → model call → response
4. Identify optimization opportunities:
   - Slow search? Tune index configuration
   - Large prompts? Right-size the context window
   - High token usage? Optimize chunking strategy

> Workshop 3 will go deeper: alerting, dashboards, GenAIOps pipelines

---

## Key Takeaways — Module 5

- ✅ AI workloads need both traditional and AI-specific monitoring
- ✅ `azd up` deploys monitoring infrastructure by default
- ✅ AI Foundry tracing gives visibility into the full request chain
- ✅ Token usage = cost — monitor it closely
- ✅ Workshop 3 will cover production monitoring in depth

---

<!-- _class: title -->

# Module 6
### Wrap-up & Next Steps

---

## Workshop Summary

**Today we accomplished:**

✅ Deployed a complete AI Landing Zone (~30 resources)
✅ Validated security controls against the Design Checklist
✅ Built and tested a RAG chat application
✅ Explored when and how to graduate from RAG to AI agents
✅ Reviewed monitoring and observability basics

---

## ⚠️ Clean-up — DELETE YOUR RESOURCES

```bash
# Remove all deployed resources
azd down
```

> **Standard deployment costs ~$2,128-3,098/month.** Delete everything now unless you are actively experimenting. Set [budget alerts](https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets) if keeping resources.

📚 [Cost Guide](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md)

---

## Key Resources

| Resource | Link |
|----------|------|
| AI Landing Zones Repo | [github.com/Azure/AI-Landing-Zones](https://github.com/Azure/AI-Landing-Zones) |
| Deploy-Your-AI-App | [github.com/microsoft/Deploy-Your-AI-App-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production) |
| Design Checklist | [AI-Landing-Zones-Design-Checklist.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) |
| Cost Guide | [AI-Landing-Zones-Cost-Guide.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Cost-Guide.md) |
| CAF AI Agent Adoption | [learn.microsoft.com](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) |
| Foundry Agent Quickstart | [learn.microsoft.com](https://learn.microsoft.com/azure/ai-foundry/agents/quickstart) |
| Diagram Builder | [github.com/Arturo-Quiroga-MSFT](https://github.com/Arturo-Quiroga-MSFT/azure-architecture-diagram-builder) |

---

## Next Steps

1. **Repeat**: Deploy again in your own subscription with different parameters
2. **Experiment**: Create a Foundry agent on the deployed infrastructure
3. **Read**: Review the full [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) guidance
4. **Apply**: Use the deployment + decision framework with your next customer
5. **Continue**: Attend **Workshop 3 — Production Readiness** for GenAIOps, CI/CD, scaling

---

## Workshop 3 Preview

### Production Readiness (GenAIOps Bridge)

- CI/CD pipelines for AI applications
- Lifecycle management and model versioning
- Production monitoring, alerting, and dashboards
- Cost optimization and scaling strategies
- Operational runbooks and incident response

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
