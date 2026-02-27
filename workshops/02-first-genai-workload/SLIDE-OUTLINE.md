# Workshop 2: Slide Deck Outline

**Purpose**: Structure for presentation deck to accompany Workshop 2  
**Target Duration**: 3-4 hours (hands-on lab emphasis)  
**Format**: Use this as a guide when creating PowerPoint/Google Slides  
**Narrative Arc**: Deploy Landing Zone → Build RAG App → Understand when to graduate to Agents

---

## Section 0: Welcome & Setup Validation (2-3 slides)

### Slide 1: Title Slide
- **Title**: From RAG to Agents — Deploying Your First Gen AI Workload
- **Subtitle**: Partner Enablement Workshop (Hands-On)
- **Footer**: AI Center of Excellence V2 | Q3 FY2026

### Slide 2: Agenda
- Module 1: Quick Recap & Deployment Strategy
- Module 2: Deploy the Landing Zone (HANDS-ON LAB)
- ☕ Break
- Module 3: Configure & Deploy RAG Application (HANDS-ON LAB)
- Module 4: From RAG to Agents (Conceptual + Demo)
- Module 5: Monitoring & Observability
- Module 6: Wrap-up & Next Steps

### Slide 3: Learning Objectives
- Deploy a complete AI Landing Zone using `azd up`
- Configure AI Foundry with standard (private) setup
- Deploy a sample RAG chat application end-to-end
- Distinguish RAG vs. AI agents in practice
- Explore Microsoft Foundry agent capabilities
- Implement basic monitoring and observability

### Slide 4: Setup Validation Checklist
- **Pre-flight checks** (participants validate right now):
  - [ ] Azure CLI 2.61.0+ → `az --version`
  - [ ] Azure Developer CLI 1.15.0+ → `azd version`
  - [ ] Logged in → `az account show`
  - [ ] Sufficient OpenAI quota in target region
  - [ ] Owner or Contributor + UAA role on subscription
- **If anything fails**: Pair with a neighbor, or follow along with instructor demo

---

## Section 1: Quick Recap & Deployment Strategy (4-5 slides)

### Slide 5: Workshop 1 Recap (60-Second Version)
- AI Landing Zone = production-ready application landing zone for AI workloads
- Two architectures: with/without Platform Landing Zone
- Design Checklist: 40+ recommendations across 10 areas
- Four deployment paths: azd, Bicep, Terraform, Portal
- **Today**: We deploy and build on top of this foundation

### Slide 6: Today's Narrative — RAG to Agents
- **Start**: Deploy the infrastructure (Landing Zone)
- **Build**: Classic RAG chat application (baseline workload)
- **Explore**: When and how to graduate to AI agents
- **Operate**: Monitoring and observability basics
- **The key question partners must answer**: Does this customer need agents, or is RAG enough?

### Slide 7: What Gets Deployed (~30+ Resources)
**Diagram**: High-level architecture of Deploy-Your-AI-App resources
- AI Foundry (hub + project)
- Azure OpenAI Service (model endpoints)
- Azure AI Search (vector search, RAG retrieval)
- Cosmos DB (chat history, memory)
- Container Apps (application runtime)
- Storage Account (document storage)
- Key Vault (secrets)
- Virtual Network + Private Endpoints + NSGs
- Managed Identities
- Log Analytics + Application Insights
- Microsoft Fabric (data foundation)
- Microsoft Purview (data governance)

### Slide 8: Today's Architecture — Without Platform LZ
- **Why standalone for this lab**: Faster deployment, self-contained, no hub dependency
- In production: enterprise customers would use "with platform LZ" variant
- **Diagram**: Reference architecture (without platform)
- All the same security controls apply — private endpoints, managed identity, no public exposure

### Slide 9: Deployment Path — Why azd up
| Consideration | azd up | Bicep | Terraform |
|--------------|--------|-------|-----------|
| **Speed** | ~45 min | ~30-60 min | ~30-60 min |
| **Setup** | Minimal | Moderate | Moderate |
| **Customization** | Limited | Full | Full |
| **Best for** | Labs, PoCs, demos | Production (Azure-native) | Production (multi-cloud) |
- Today we use `azd up` for speed — partners should use Bicep/Terraform for customer deployments
- See [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md) for full comparison

---

## Section 2: Deploy the Landing Zone — HANDS-ON LAB (8-10 slides)

### Slide 10: Lab Overview
- **Goal**: Deploy a complete AI Landing Zone with ~30 Azure resources
- **Time**: ~60 minutes (including deploy wait time)
- **Steps**: Clone → Configure → Deploy → Validate
- **Important**: Deployment takes ~30-45 min — we'll use that time for a guided Portal walkthrough

### Slide 11: Step 1 — Clone the Repository
```bash
git clone --recurse-submodules \
  https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git
cd Deploy-Your-AI-Application-In-Production
```
- `--recurse-submodules` is critical — pulls in Bicep modules
- Review the repo structure: `/infra`, `/docs`, `/src`

### Slide 12: Step 2 — Initialize and Configure
```bash
azd init
```
- Set environment name (use workshop naming convention)
- Review key parameters:
  - Region selection (quota matters!)
  - Resource naming prefix
  - SKU selections (balance cost vs. capability)
- **Reference**: [Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md)

### Slide 13: Step 3 — Deploy
```bash
azd up
```
- Deployment takes ~30-45 minutes
- What's happening behind the scenes:
  1. Bicep templates compiled
  2. Resource group created
  3. Networking deployed (VNet, subnets, NSGs)
  4. PaaS services deployed with private endpoints
  5. RBAC assignments configured
  6. Application code deployed
- **While we wait**: Let's explore what's being built...

### Slide 14: Portal Walkthrough — Networking Layer
**Show during deployment wait time**
- Virtual network and subnet structure
- Private endpoints — notice no public IP addresses
- NSG rules — default deny, explicit allow
- **Checklist validation**: N-R3 (Private Endpoints), N-R4 (NSGs)

### Slide 15: Portal Walkthrough — AI Services Layer
**Show during deployment wait time**
- AI Foundry hub and project structure
- Azure OpenAI deployments and model endpoints
- AI Search index configuration
- Cosmos DB for chat history
- **Checklist validation**: D-R1 (Thread Storage), D-R2 (File Storage)

### Slide 16: Portal Walkthrough — Security Layer
**Show during deployment wait time**
- Managed identities — no credentials in code
- Key Vault — secrets management
- RBAC assignments — least privilege
- Defender for Cloud recommendations
- **Checklist validation**: I-R1 (Managed Identity), I-R3 (Entra ID), S-R1 (Defender)

### Slide 17: Step 4 — Validate Deployment
- Check deployment succeeded: `azd show`
- Verify in Portal:
  - [ ] All resources created in resource group
  - [ ] Private endpoints active and connected
  - [ ] RBAC assignments correct
  - [ ] No public endpoints exposed
  - [ ] Diagnostic settings configured
- **Troubleshooting**: Common issues and fixes

### Slide 18: Key Takeaways — Module 2
- A complete production-ready Landing Zone in ~45 minutes
- Security-first by default (private endpoints, managed identity, RBAC)
- Design Checklist items are already implemented in the templates
- This is what partners should demonstrate to customers

---

## Section 3: Configure & Deploy RAG Application — HANDS-ON LAB (6-8 slides)

### Slide 19: RAG Application Architecture
**Diagram**: Data flow for the RAG chat application
```
User Query → Container App → AI Foundry → AI Search (retrieve) → OpenAI (generate) → Response
                                              ↑
                                        Document Index
                                        (embeddings)
```
- **Retrieval**: AI Search finds relevant document chunks
- **Augmentation**: Retrieved context is added to the prompt
- **Generation**: OpenAI model generates the response
- This is **deterministic retrieval** — the same query returns similar results every time

### Slide 20: Step 1 — Configure AI Foundry
- Navigate to AI Foundry in the Portal
- Review the project structure
- Verify model deployments (GPT-4o, embedding model)
- Check connections to AI Search, Cosmos DB, Storage

### Slide 21: Step 2 — Ingest Sample Data
- Upload sample documents to Storage Account
- Configure AI Search indexer
- Create embeddings for vector search
- Verify index population and search results
- **Key concept**: Quality of retrieval = quality of agent responses

### Slide 22: Step 3 — Deploy and Test the Chat App
- Access the Container App endpoint
- Test with sample queries
- Observe the RAG pattern in action:
  - Query → Search → Retrieved context → Generated response
  - Note: responses are grounded in your data, not hallucinated
- Try edge cases: questions outside the data, ambiguous queries

### Slide 23: Step 4 — Understand What's Happening
- Open AI Foundry tracing to see the full request flow
- Token usage: prompt tokens + completion tokens = cost
- Latency breakdown: search time + model inference time
- **Important observation**: The flow is predictable and repeatable

### Slide 24: When RAG Is Enough
- Customer needs document Q&A, knowledge base, FAQ → **RAG is sufficient**
- Inputs are well-defined, outputs are predictable → **RAG is sufficient**
- Low latency and cost are priorities → **RAG is sufficient**
- No need for tool orchestration or multi-step reasoning → **RAG is sufficient**
- **Partner talking point**: "Not every AI workload needs an agent. Start here and graduate when the use case demands it."

### Slide 25: Key Takeaways — Module 3
- RAG is the foundation workload on AI Landing Zones
- Quality of retrieval directly impacts response quality
- The Landing Zone provides all the infrastructure RAG needs
- RAG is predictable, cost-effective, and well-understood
- Know when RAG is enough before recommending agents

---

## Section 4: From RAG to Agents (8-10 slides)

### Slide 26: The RAG → Agent Spectrum
- What we just built: **Classic RAG** (retrieve + generate)
- What comes next: **AI Agents** (reason + plan + act + retrieve + generate)
- **Key distinction**:
  - RAG: Fixed pipeline — query → search → generate
  - Agent: Dynamic pipeline — model decides what tools to use, when, and in what order
- **Source**: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)

### Slide 27: When to Graduate to Agents
Refer to the [AI Agent Decision Tree](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents):
- **Dynamic decision-making**: Task requires multi-step reasoning with conditional logic
- **Complex orchestration**: Need to chain multiple tools, APIs, or services together
- **Adaptive behavior**: Inputs are ambiguous, system must interpret intent
- **Example**: Customer support agent that checks order status, processes returns, AND escalates to human — all in one conversation

### Slide 28: Three Agent Types on Your Landing Zone
| Agent Type | What It Does | Adds to Your LZ | Example |
|------------|-------------|-----------------|---------|
| **Productivity** | Retrieve & synthesize | Minimal — similar to RAG | Internal knowledge assistant |
| **Action** | Perform specific tasks | Logic Apps, Functions, APIM | Ticket creation, data updates |
| **Automation** | Multi-step processes | Orchestration, triggers, governance | Supply chain optimization |
- Same Landing Zone foundation — different workload complexity on top

### Slide 29: Microsoft Foundry — Your Agent Platform
- **Foundry is what runs on the Landing Zone** you just deployed
- Two types of custom agents:
  - **Declarative agents**: Prompt-based, behavior-driven — simpler to update and version
  - **Hosted agents**: Code-first, custom libraries — full control over logic
- **Workflows**: Orchestrate multi-agent or multi-step processes
- **Setup alignment**: Foundry's standard setup with private networking = **your Landing Zone**
- **Source**: [Technology Plan](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)

### Slide 30: Foundry Standard Setup = Your Landing Zone
**Side-by-side comparison**:
| Foundry Standard Setup | AI Landing Zone Provides |
|-----------------------|------------------------|
| Private networking | ✅ VNet, Private Endpoints, NSGs |
| Managed Identity | ✅ No credentials in code |
| Enterprise data controls | ✅ Purview, Key Vault, RBAC |
| AI Search integration | ✅ Already deployed |
| Cosmos DB for memory | ✅ Already deployed |
- **Key insight**: Partners who deploy the Landing Zone are already set up for Foundry agents
- **Source**: [Foundry Environment Setup](https://learn.microsoft.com/azure/ai-foundry/agents/environment-setup)

### Slide 31: Single Agent vs. Multi-Agent
- **Start with single agent** unless you must separate:
  - Crossing security/compliance boundaries
  - Multiple teams own separate domains
  - Known future growth across business units
- **Multi-agent trade-offs**: Latency at handoffs, credential management, state sync, higher cost
- **Decision framework**:
  - Low complexity, single domain → Single agent
  - Hard security boundaries → Multi-agent from start
  - Unclear → Prototype single, test, then decide
- **Source**: [Single vs. Multiple Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents)

### Slide 32: Demo — Foundry Agent Playground *(If Time/Access Permits)*
- Navigate to AI Foundry → Agents
- Create a simple agent with:
  - System instructions
  - Knowledge source (AI Search — already connected!)
  - A tool (e.g., a simple function)
- Show how the agent reasons and selects tools dynamically
- Compare with the deterministic RAG flow from Module 3

### Slide 33: The Partner Conversation Framework
- **Discovery**: "What problem are you solving? Is it Q&A, task automation, or complex orchestration?"
- **Qualify**: Use the decision tree — deterministic code, RAG, or agent?
- **Scope**: Which agent type? Productivity, Action, or Automation?
- **Architecture**: Single or multi-agent? SaaS or custom build?
- **Infrastructure**: Deploy AI Landing Zone → configure Foundry standard setup
- **Iterate**: Start simple (RAG or single agent), validate, then graduate

### Slide 34: Key Takeaways — Module 4
- RAG is a subset of what agents can do — start here
- Graduate to agents when reasoning and tool orchestration are genuinely needed
- The Landing Zone you deployed is already agent-ready (Foundry standard setup)
- Use the decision tree & agent types to qualify customer workloads
- Start single-agent, prove value, then consider multi-agent

---

## Section 5: Monitoring & Observability (3-4 slides)

### Slide 35: Monitoring AI Workloads — What's Different
- Traditional monitoring (CPU, memory, latency) still applies
- **AI-specific monitoring** adds new dimensions:
  - Token usage and cost tracking
  - Model response quality and relevance
  - Hallucination detection
  - Model drift over time
  - RAG retrieval quality (are the right documents being found?)
- **For agents**: Add tool execution monitoring, orchestration tracing, escalation tracking

### Slide 36: What's Already Deployed (from `azd up`)
- **Application Insights**: Request tracing, error rates, latency
- **Log Analytics**: Centralized logs, diagnostic settings
- **AI Foundry Tracing**: Model call traces, token usage
- **Key metrics to watch**:
  - Response latency (P50, P95, P99)
  - Token consumption (prompt + completion)
  - Error rate by type
  - AI Search query performance
  - Cosmos DB RU consumption
- **Checklist items**: M-R1 (Monitor models, resources, data), M-R4 (Diagnostic settings)

### Slide 37: AI Foundry Tracing Walkthrough
- Open AI Foundry → Tracing
- Find a trace from the RAG query you ran in Module 3
- Inspect the full chain: search → prompt construction → model call → response
- Identify optimization opportunities: slow search? Large prompts? High token usage?

### Slide 38: Key Takeaways — Module 5
- AI workloads need both traditional and AI-specific monitoring
- `azd up` deploys monitoring infrastructure by default
- AI Foundry tracing gives visibility into the full request chain
- Workshop 3 will go deeper: alerting, dashboards, GenAIOps

---

## Section 6: Wrap-up (3-4 slides)

### Slide 39: Workshop Summary
**Today we accomplished**:
✅ Deployed a complete AI Landing Zone (~30 resources)
✅ Validated security controls against the Design Checklist
✅ Built and tested a RAG chat application
✅ Explored when and how to graduate from RAG to AI agents
✅ Reviewed monitoring and observability basics

### Slide 40: Clean-up
```bash
# Remove all deployed resources
azd down

# Or keep for experimentation!
# Remember: costs accrue while resources are running
```

### Slide 41: Key Resources
| Resource | Link |
|----------|------|
| AI Landing Zones Repo | github.com/Azure/AI-Landing-Zones |
| Deploy-Your-AI-App | github.com/microsoft/Deploy-Your-AI-Application-In-Production |
| CAF AI Agent Adoption | learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/ |
| AI Foundry Agent Quickstart | learn.microsoft.com/azure/ai-foundry/agents/quickstart |
| **Azure Architecture Diagram Builder** | github.com/Arturo-Quiroga-MSFT/azure-architecture-diagram-builder |
| Design Checklist | (link) |
| Partner Quick Reference | (internal) |

### Slide 42: Next Steps
1. **Repeat**: Deploy again in your own subscription with different parameters
2. **Experiment**: Try creating a Foundry agent on the deployed infrastructure
3. **Read**: Review the full [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) guidance
4. **Apply**: Use the deployment + decision framework with your next customer
5. **Continue**: Attend **Workshop 3 — Landing Zones to Production** for GenAIOps, CI/CD, scaling

### Slide 43: Workshop 3 Preview
**Landing Zones to Production (GenAIOps Bridge)**
- CI/CD pipelines for AI applications
- Lifecycle management and model versioning
- Production monitoring, alerting, and dashboards
- Cost optimization and scaling strategies
- Operational runbooks and incident response

### Slide 44: Q&A & Thank You
- Questions?
- Feedback survey (link in chat)
- AI Center of Excellence V2 | Partner Enablement Team

---

## 📝 Slide Design Notes

### Visual Consistency
- Match Workshop 1 branding and style
- Use Microsoft brand colors
- Include architecture diagrams from official repos
- Use terminal/code screenshots for lab steps
- Include Portal screenshots for walkthrough slides

### Lab Slide Formatting
- Lab slides should have clear **step numbers** and **code blocks**
- Include expected wait times ("Deployment takes ~30-45 min")
- Add "⚠️ Common Issue" callouts where participants may get stuck
- Include "✅ Checkpoint" markers so participants can verify progress

### Speaker Notes
- Include timing guidance per slide
- Add backup content for when deployment is running
- Include troubleshooting steps for common errors

---

**Total Estimated Slides**: 42-48  
**Target Creation Time**: 5-7 hours  
**Authors**: Arturo Quiroga (PSA) & Anahita Afshari (PSA)  
**Created**: February 25, 2026
