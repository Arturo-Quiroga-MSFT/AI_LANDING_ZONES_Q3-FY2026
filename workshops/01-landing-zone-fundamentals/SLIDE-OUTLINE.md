# Workshop 1: Slide Deck Outline

**Purpose**: Structure for presentation deck to accompany Workshop 1  
**Target Duration**: 2-3 hours (adjust per section)  
**Format**: Use this as a guide when creating PowerPoint/Google Slides

---

## Section 0: Title & Welcome (3-5 slides)

### Slide 1: Title Slide
- **Title**: AI Landing Zones Fundamentals
- **Subtitle**: Partner Enablement Workshop
- **Footer**: AI Center of Excellence V2 | Q3 FY2026

### Slide 2: Agenda
- Module 1: What is AI Landing Zone?
- Module 2: Reference Architectures
- Module 3: Design Checklist Walkthrough
- Module 4: Deployment Options
- Module 5: Partner Engagement Scenarios

### Slide 3: Learning Objectives
- Explain what Azure AI Landing Zones are
- Identify key architecture components
- Navigate the Design Checklist
- Choose appropriate deployment approach
- Plan customer engagements

### Slide 4: Housekeeping
- Duration: 2-3 hours
- Breaks: 10 min after Module 2
- Questions: Welcome anytime
- Materials: Links in chat
- Recording: [Yes/No]

---

## Section 1: What is AI Landing Zone? (6-8 slides)

### Slide 5: The AI Challenge
- Enterprises want to deploy Gen AI workloads
- Production requires: security, governance, scalability
- Starting from scratch is slow and risky
- **Key Question**: How do we accelerate production-ready AI deployments?

### Slide 6: AI Landing Zone Definition
- "A secure, resilient, and scalable reference architecture"
- Purpose-built for AI Apps & Agents
- Implements Azure best practices from Day 0
- Available as: Bicep, Terraform, Portal (coming soon)
- **Source**: [Azure/AI-Landing-Zones](https://github.com/Azure/AI-Landing-Zones)

### Slide 7: Where AI Landing Zones Fit in CAF
- **CAF Landing Zone Hierarchy**:
  - **Platform Landing Zone**: Shared services (Identity, Connectivity, Management) owned by central IT
  - **Application Landing Zone**: Where workloads deploy - **AI Landing Zone goes here**
- AI is just another workload from CAF perspective
- NOT a separate landing zone type
- **Ref**: [AI in Azure Landing Zones](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/#ai-in-azure-landing-zones)

### Slide 8: Platform vs Application Landing Zone
- **Platform Team Provides** (in "with platform" scenario):
  - Hub virtual network, Azure Firewall, VPN/ExpressRoute
  - Azure Bastion for jump box access
  - Private DNS zones, DDoS protection
  - Governance policies at management group level
- **Workload Team Owns** (AI Landing Zone):
  - Spoke virtual network subnets, NSGs
  - AI Foundry, AI Search, Cosmos DB, App Service
  - Private endpoints to PaaS services
  - Workload-specific monitoring
- **Partner Question**: Does your customer have existing Platform LZ?

### Slide 9: CAF AI Scenario Alignment
- AI Landing Zone is part of "AI Ready" stage
- Specifically: "AI on Azure Platforms (PaaS)"
- Links to CAF AI Strategy and Checklist
- **Diagram**: Include CAF AI Ready visual

### Slide 9: WAF AI Workload Alignment
- Follows WAF design principles for AI
- Covers: Reliability, Security, Cost, Operations, Performance
- **Diagram**: Include WAF AI architecture pattern

### Slide 10: Supported Use Cases & AI Agent Types
- **Classic RAG workloads** (deterministic retrieval): Chat, document Q&A, knowledge mining, content processing
- **AI Agent workloads** (adaptive reasoning): Agents that reason, plan, and use tools dynamically
- Microsoft's CAF identifies a **spectrum of 3 agent types** with increasing complexity:

| Agent Type | What It Does | Example |
|------------|-------------|--------|
| **Productivity Agents** | Retrieve & synthesize information | Knowledge management, customer service support |
| **Action Agents** | Perform specific tasks in workflows | Ticket creation, system monitoring, data updates |
| **Automation Agents** | Multi-step processes, minimal oversight | Supply chain optimization, complex approval flows |

- **Key Partner Question**: Does your customer need classic RAG or AI agents? (See decision tree, next slide)
- **Source**: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)

### Slide 10a: AI Agent Architecture — 5 Core Components
- **Diagram**: Agent architecture (model + 4 components feeding into it)
- Every AI agent is built on 5 components:
  1. **Generative AI Model** — The reasoning engine (processes instructions, generates outputs)
  2. **Instructions** — Define scope, boundaries, and behavioral guidelines
  3. **Retrieval (Knowledge)** — Grounding data and context (reduces hallucinations)
  4. **Actions (Tools)** — Functions, APIs, systems the agent calls to perform tasks
  5. **Memory** — Conversation history and state for multi-turn continuity
- **Key Insight**: Components 3 (Retrieval) and 4 (Actions) are what the Landing Zone infrastructure directly supports — AI Search, Cosmos DB, APIs, Logic Apps, Functions
- **Source**: [What is an AI agent?](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/#what-is-an-ai-agent)

### Slide 10b: When to Use Agents vs. Classic RAG (Decision Tree)
- **Diagram**: Reference the [AI agent decision tree](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents)
- **Don't use agents when**:
  - Task is structured, predictable, rule-based → Use deterministic code
  - Goal is static knowledge retrieval / Q&A → Use classic RAG
- **Use agents when the task requires**:
  - Dynamic decision-making (multi-step reasoning, conditional logic)
  - Complex orchestration (chaining tools, APIs, services)
  - Adaptive behavior (ambiguous inputs, intent interpretation)
- **Partner Talking Point**: "Not every AI workload needs an agent. Start with the simplest approach that solves the problem. Classic RAG is cheaper, faster, and more predictable. Graduate to agents when reasoning and tool orchestration are genuinely required."
- **Source**: [Business plan for AI agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan)

### Slide 11: Key Takeaways - Module 1
- AI Landing Zone = production-ready AI foundation
- Supports both classic RAG and AI agent workloads
- Aligns with CAF (including AI Agent Adoption guidance) and WAF
- Accelerates enterprise AI adoption
- Reduces risk and time-to-production
- **New**: Use the agent decision tree to help partners qualify the right workload type

---

## Section 2: Reference Architectures (8-10 slides)

### Slide 12: Two Architecture Options
- **Option 1**: With Platform Landing Zone (Enterprise)
- **Option 2**: Without Platform Landing Zone (Standalone)
- Both are production-ready
- Choose based on customer context

### Slide 13: With Platform Landing Zone
- **Diagram**: Full architecture image from repo
- Leverages existing hub-spoke networking
- Uses central Firewall, Bastion, DNS
- Best for: Enterprises with existing ALZ
- **Source**: [Architecture Diagram](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)

### Slide 14: Without Platform Landing Zone
- **Diagram**: Standalone architecture image from repo
- Self-contained application landing zone
- Includes own networking and security
- Best for: Greenfield, PoCs, smaller orgs
- **Source**: [Architecture Diagram](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)

### Slide 15: Key Components - AI Layer
- **Azure AI Foundry**: Development platform
- **AI Services**: Model endpoints
- **AI Search**: RAG retrieval
- **Connections**: Service integrations

### Slide 16: Key Components - Compute Layer
- **Container Apps**: Microservices runtime
- **App Service**: Web front-ends
- **Functions**: Event-driven compute
- **Scaling**: Auto-scale capabilities

### Slide 17: Key Components - Data Layer
- **Cosmos DB**: Chat history, context storage
- **Storage Account**: Document storage, files
- **AI Search**: Vector search, embeddings
- **(Optional) Fabric**: Enterprise data foundation

### Slide 18: Key Components - Security Layer
- **Private Endpoints**: No public exposure
- **Key Vault**: Secrets management
- **Managed Identity**: No credentials in code
- **NSGs & Firewall**: Network isolation
- **Bastion**: Secure admin access

### Slide 19: Key Components - Governance Layer
- **Defender for Cloud**: Security posture
- **Purview**: Data governance
- **Azure Policy**: Compliance automation
- **Azure Monitor**: Observability

### Slide 20: Choosing Your Architecture
| Factor | With Platform LZ | Without Platform LZ |
|--------|-----------------|---------------------|
| Existing ALZ | ✅ Recommended | ⚠️ Consider migration |
| Greenfield | ⚠️ More setup | ✅ Faster start |
| Enterprise | ✅ Best fit | ⚠️ May need upgrade |
| PoC/Pilot | ⚠️ Overkill | ✅ Right-sized |

### Slide 21: Key Takeaways - Module 2
- Two validated architecture options
- Choose based on customer context
- All components are Azure PaaS
- Security-first design by default

---

## Section 3: Design Checklist Walkthrough (10-12 slides)

### Slide 22: The Design Checklist
- 40+ recommendations across 10 areas
- Based on CAF + WAF best practices
- Use for greenfield and brownfield
- **Link**: [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)

### Slide 23: 10 Design Areas Overview
**Table**: Area | # Recommendations | Key Focus
- Networking (N-R1 to N-R9)
- Identity (I-R1 to I-R6)
- Security (S-R1 to S-R5)
- Monitoring (M-R1 to M-R6)
- Cost (CO-R1 to CO-R4)
- Data (D-R1 to D-R3)
- Governance (G-R1 to G-R5)
- Reliability (R-R1)
- Resource Org (R-R1 to R-R4)
- Compute (C-R1)

### Slide 24: Deep Dive - Networking
**Key Recommendations**:
- N-R1: DDoS Protection
- N-R2: Bastion for jumpbox access
- N-R3: Private endpoints everywhere
- N-R4: NSGs on all subnets
- N-R5: WAF via App Gateway/Front Door
- N-R6: APIM as AI Gateway
- N-R7: Firewall for egress control
- N-R8: Private DNS zones
- N-R9: Restrict outbound by default

### Slide 25: Deep Dive - Identity
**Key Recommendations**:
- I-R1: Managed Identity with least privilege
- I-R2: MFA + PIM for sensitive accounts
- I-R3: Entra ID for authentication (not API keys)
- I-R4: Conditional Access policies
- I-R5: RBAC with least privilege
- I-R6: Disable key-based access

### Slide 26: Deep Dive - Security
**Key Recommendations**:
- S-R1: Defender for Cloud recommendations
- S-R2: Microsoft Cloud Security Baseline
- S-R3: Purview for data protection
- S-R4: MITRE ATLAS + OWASP for AI risks
- S-R5: AI Content Safety for outputs

### Slide 27: Deep Dive - Monitoring
**Key Recommendations**:
- M-R1: Monitor models, resources, data
- M-R2: Azure Monitor Baseline Alerts
- M-R3: AI Foundry tracing and evaluation
- M-R4: Diagnostic settings to Log Analytics
- M-R5: Model and data drift detection
- M-R6: Network Watcher troubleshooting

### Slide 28: Deep Dive - Cost
**Key Recommendations**:
- CO-R1: Understand AI Foundry pricing
- CO-R2: Combine PTU + PAYGO endpoints
- CO-R3: Consider global deployment types
- CO-R4: Auto-shutdown for non-prod

### Slide 29: Deep Dive - Governance
**Key Recommendations**:
- G-R1: Built-in AI-related policies
- G-R2: Regulatory compliance (NIST AI RMF)
- G-R3: Responsible AI dashboard
- G-R4: AI Content Safety for testing
- G-R5: Policy to govern model catalog

### Slide 30: How to Use the Checklist
1. **Assessment**: Walk through with customer
2. **Gap Analysis**: Identify missing items
3. **Prioritization**: P0/P1/P2 classification
4. **Implementation**: Track completion
5. **Validation**: Post-deployment review

### Slide 31: Key Takeaways - Module 3
- Design Checklist is your primary tool
- 10 areas cover comprehensive requirements
- Use with every customer engagement
- Reference, don't recreate

---

## Section 4: Deployment Options (6-8 slides)

### Slide 32: Four Deployment Paths
| Path | Tool | Speed | Customization |
|------|------|-------|---------------|
| A | azd up | ~45 min | Limited |
| B | Bicep | ~30-60 min | Full |
| C | Terraform | ~30-60 min | Full |
| D | Portal | Manual | Limited |

### Slide 33: Path A - Azure Developer CLI (azd)
- Repository: Deploy-Your-AI-Application-In-Production
- Single command: `azd up`
- 30+ resources pre-configured
- Best for: PoCs, demos, fast start
- **Link**: [Repository](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

### Slide 34: Path B - Bicep
- Repository: AI-Landing-Zones/bicep
- Azure-native IaC
- AVM (Azure Verified Modules) based
- Best for: Azure-only, full control
- **Link**: [Bicep Folder](https://github.com/Azure/AI-Landing-Zones/tree/main/bicep)

### Slide 35: Path C - Terraform
- Repository: AI-Landing-Zones/terraform
- Multi-cloud capable
- AVM (Azure Verified Modules) based
- Best for: Multi-cloud, Terraform teams
- **Link**: [Terraform Folder](https://github.com/Azure/AI-Landing-Zones/tree/main/terraform)

### Slide 36: Decision Framework
**Include decision tree visual from IaC Decision Framework doc**

Key questions:
1. Need fastest deployment? → azd
2. Multi-cloud strategy? → Terraform
3. Azure-native team? → Bicep

### Slide 37: Key Takeaways - Module 4
- Multiple valid deployment paths
- Choose based on customer context
- All paths are production-ready
- See IaC Decision Framework for details

---

## Section 5: Partner Engagement Scenarios (5-7 slides)

### Slide 38: Four Common Scenarios
1. Enterprise with existing ALZ
2. Greenfield/PoC deployment
3. Regulated industry
4. Cost-sensitive deployment

### Slide 39: Scenario 1 - Enterprise Customer
**Context**: Large org with existing Azure Landing Zones
**Recommendation**: Bicep/Terraform + Platform LZ architecture
**Focus Areas**: Networking, Identity integration
**Key Questions**:
- What's their current ALZ configuration?
- What governance policies exist?
- Integration requirements?

### Slide 40: Scenario 2 - Greenfield/PoC
**Context**: New to Azure or exploring AI
**Recommendation**: azd up (Deploy-Your-AI-App)
**Focus Areas**: Fast deployment, validation
**Key Questions**:
- Timeline for PoC?
- Expansion plans?
- Who needs access?

### Slide 41: Scenario 3 - Regulated Industry
**Context**: Healthcare, finance, government
**Recommendation**: Bicep + extensive security review
**Focus Areas**: All Security (S-R1-5), Governance (G-R1-5)
**Key Questions**:
- Compliance requirements?
- Data residency needs?
- Audit requirements?

### Slide 42: Scenario 4 - Cost-Sensitive
**Context**: Limited budget, cost optimization critical
**Recommendation**: Minimal deployment + Cost checklist
**Focus Areas**: Cost (CO-R1-4), Compute (C-R1)
**Key Questions**:
- Budget constraints?
- Workload predictability?
- Scale requirements?

### Slide 43: Scenario 5 - Customer Building AI Agents
**Context**: Customer moving beyond chat/RAG to autonomous or semi-autonomous AI agents
**Recommendation**: Standard Foundry setup (private networking) on AI Landing Zone + CAF AI Agent Adoption framework
**Focus Areas**: Security (S-R1-5), Governance (G-R1-5), Compute (C-R1), Monitoring (M-R1-6)
**Key Questions**:
- What tasks will the agent perform? (Retrieval only? Actions? Multi-step automation?)
- Single agent or multi-agent? (Use the decision tree from Slide 10b)
- Who owns governance? (Agent-specific: Responsible AI, testing nondeterministic behavior)
- SaaS agents sufficient? (M365 Copilot, Dynamics 365 agents before custom build)

| Agent Type | LZ Infrastructure Needs | Additional Components |
|------------|------------------------|----------------------|
| Productivity Agent | Standard (AI Search, Cosmos DB, Foundry) | Minimal — similar to RAG |
| Action Agent | Standard + APIs/integrations | Logic Apps, Functions, APIM |
| Automation Agent | Full + orchestration + rigorous governance | Workflows, triggers, audit trails, human-in-the-loop gates |

**Source**: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) | [Single vs. Multi-Agent](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents)

### Slide 44: Key Takeaways - Module 5
- Tailor approach to customer context
- Use Design Checklist as conversation guide
- Different scenarios need different paths
- Ask discovery questions upfront
- **New**: Use the CAF agent decision tree to qualify agent workloads and scope infrastructure

---

## Section 6: Wrap-up (3-5 slides)

### Slide 45: Workshop Summary
**Today we covered**:
✅ What AI Landing Zones are and why they matter
✅ Classic RAG vs. AI Agents — when to use each
✅ Two reference architecture options
✅ 10 design areas and key recommendations
✅ Four deployment paths
✅ Five partner engagement scenarios (including AI Agents)

### Slide 46: Key Resources
| Resource | Link |
|----------|------|
| AI Landing Zones Repo | github.com/Azure/AI-Landing-Zones |
| Deploy-Your-AI-App | github.com/microsoft/Deploy-Your-AI-Application-In-Production |
| **CAF AI Agent Adoption** | learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/ |
| **Azure Architecture Diagram Builder** | github.com/Arturo-Quiroga-MSFT/azure-architecture-diagram-builder |
| Design Checklist | (link) |
| Partner Quick Reference | (internal) |
| IaC Decision Framework | (internal) |

### Slide 47: Next Steps
1. **Practice**: Deploy a test environment
2. **Read**: Review Design Checklist in detail
3. **Explore**: Review the [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) guidance
4. **Apply**: Use with next customer engagement
5. **Continue**: Attend Workshop 2 (hands-on deployment)

### Slide 48: Workshop 2 Preview
**From RAG to Agents: Deploying Your First Gen AI Workload**
- Hands-on lab: Deploy Landing Zone + RAG chat application
- Configure AI Foundry with standard (private) setup
- Understand when & how to graduate from RAG to agents
- Explore Microsoft Foundry agent capabilities
- Implement monitoring and observability

### Slide 49: Q&A
- Questions?
- Feedback?
- Contact: [facilitator info]

### Slide 50: Thank You
- AI Center of Excellence V2
- Partner Enablement Team
- [Date and version]

---

## 📝 Slide Design Notes

### Visual Consistency
- Use Microsoft brand colors
- Include architecture diagrams from official repos
- Keep text minimal, speak to the points
- Use tables for comparisons

### Speaker Notes
- Include talking points in speaker notes
- Add timing guidance per slide
- Include backup Q&A content

### Animations
- Minimal animations (professional)
- Progressive reveal for lists if needed
- Avoid distracting transitions

### Accessibility
- High contrast text
- Alt text for images
- Readable font sizes (24pt+ body, 32pt+ headers)

---

**Total Estimated Slides**: 48-53  
**Target Creation Time**: 4-6 hours  
**Authors**: Anahita Afshari (PSA) & Arturo Quiroga (PSA)  
**Last Updated**: February 25, 2026
