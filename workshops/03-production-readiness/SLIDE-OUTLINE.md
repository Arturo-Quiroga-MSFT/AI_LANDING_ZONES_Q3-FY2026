# Workshop 3: Slide Deck Outline

**Purpose**: Structure for presentation deck to accompany Workshop 3  
**Target Duration**: 4 hours  
**Format**: Conceptual + demo-heavy (less hands-on than WS2, more architecture and patterns)  
**Narrative Arc**: You deployed it (WS2) → Now operate it at scale

> **🔧 For Ana, George, Guilherme**: Slides marked with *(GEN AI OPS)* need your content. Fill in pipeline details, monitoring patterns, and any accelerator material you have.

---

## Section 0: Welcome & Context (2-3 slides)

### Slide 1: Title Slide
- **Title**: Landing Zones to Production — The GenAIOps Bridge
- **Subtitle**: Partner Enablement Workshop (Advanced)
- **Footer**: AI Center of Excellence V2 | Q3 FY2026

### Slide 2: Agenda
- Module 1: CI/CD for AI Workloads
- Module 2: Production Monitoring & Observability
- Module 3: Agent Governance & Security
- Module 4: Cost Optimization & Scaling
- Module 5: Wrap-up & Production Planning

### Slide 3: Where We Are in the Journey
- WS1: **Understand** (concepts, architectures, decision frameworks)
- WS2: **Build** (deploy LZ, RAG app, explore agents)
- WS3: **Operate** ← you are here (CI/CD, monitoring, governance, cost)
- "You have a deployed workload. Now: how do you run it in production?"

---

## Section 1: CI/CD for AI Workloads (10-12 slides)

### Slide 4: The Two Pipelines *(GEN AI OPS)*
- **Infrastructure pipeline**: Deploy/update Landing Zone (Bicep/Terraform)
- **Application pipeline**: Build, test, deploy AI app (container + model config)
- These are separate pipelines with different triggers and approval gates

### Slide 5: Infrastructure Pipeline Pattern *(GEN AI OPS)*
- Trigger: PR merge to `infra/` branch
- Steps: Lint → Validate → What-if/Plan → Approve → Deploy
- Tools: GitHub Actions or Azure DevOps
- *TODO: Add sample pipeline YAML*

### Slide 6: Application Pipeline Pattern *(GEN AI OPS)*
- Trigger: PR merge to `src/` branch
- Steps: Build container → Run tests → Push to ACR → Deploy to Container Apps
- Include model evaluation step before deploy
- *TODO: Add sample pipeline YAML*

### Slide 7: Model Deployment & Versioning *(GEN AI OPS)*
- Model versioning strategy (which model, which version, which config)
- Prompt versioning: track system prompts as code
- Blue/green deployment for model swaps
- Rollback strategy: when and how to revert

### Slide 8: Testing AI Workloads *(GEN AI OPS)*
- Unit tests: deterministic logic, API contracts
- Integration tests: end-to-end flow (query → search → model → response)
- Model evaluation: response quality, groundedness, relevance scoring
- Load testing: token throughput, latency under load

### Slide 9: Environments & Promotion
- Dev → Staging → Production promotion path
- Environment-specific parameters (model SKU, search tier, network config)
- Approval gates between environments
- Feature flags for gradual rollout

### Slide 10: Key Takeaways — Module 1
- Separate infra and app pipelines
- Treat prompts and model config as code
- Test AI workloads at multiple levels
- Automate but gate production deployments

---

## Section 2: Production Monitoring & Observability (8-10 slides)

### Slide 11: Monitoring Stack Overview *(GEN AI OPS)*
- Application Insights → request tracing, errors, latency
- Log Analytics → centralized logs, KQL queries
- AI Foundry Tracing → model-level visibility
- Azure Workbooks or Grafana → dashboards
- Alerts → proactive notification

### Slide 12: The AI Monitoring Pyramid
```
        [Business KPIs]
       /               \
    [Model Quality]     [User Experience]
   /                                     \
 [Infrastructure Health]    [Cost Metrics]
```
- Monitor bottom-up: infra → model → business value

### Slide 13: Key Metrics Dashboard *(GEN AI OPS)*
- Response latency (P50, P95, P99)
- Token consumption (prompt + completion, cost per request)
- Error rates by category (model errors, search failures, app errors)
- Retrieval quality (% relevant results from AI Search)
- Availability (uptime %)
- *TODO: Add sample dashboard screenshot or template*

### Slide 14: Agent-Specific Observability
- Tool call monitoring: which tools called, success/failure rate
- Reasoning chain tracing: full decision path per request
- Escalation tracking: when agent hands off to human
- Drift detection: are agent behaviors changing over time?
- [CAF Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)

### Slide 15: Alerting Rules *(GEN AI OPS)*
| Alert | Threshold | Severity |
|-------|-----------|----------|
| Latency P95 | > X ms | Warning |
| Error rate | > X% | Critical |
| Token budget | > X% of daily limit | Warning |
| Model drift score | > X | Warning |
| Availability | < 99.X% | Critical |
- *TODO: Fill in recommended thresholds*

### Slide 16: SLA Definition for AI Workloads
- What SLA metrics make sense for AI? (not just uptime)
- Response quality SLA: % of grounded responses
- Latency SLA: P95 response time target
- Cost SLA: max cost per 1K requests
- Agent SLA: % tasks completed without human escalation

### Slide 17: Key Takeaways — Module 2
- AI monitoring = traditional monitoring + model-specific metrics
- Build dashboards around the monitoring pyramid
- Define SLAs that include quality, not just availability
- Agent workloads need tool call and reasoning observability

---

## Section 3: Agent Governance & Security (8-10 slides)

### Slide 18: CAF Govern & Secure Phase
- The 4-phase CAF AI Agent lifecycle: Plan → **Govern & Secure** → Build → Manage
- This phase happens BEFORE you build agents in production
- [CAF Govern & Secure](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)

### Slide 19: Data Access Controls
- What data can each agent access?
- Principle of least privilege applied to agent data access
- Data classification: which data sources are agent-accessible
- Row-level and document-level security in AI Search

### Slide 20: Tool Permission Boundaries
- Which APIs/tools can each agent invoke?
- Tool allowlists per agent type (Productivity, Action, Automation)
- Rate limiting and budget caps per tool
- Approval workflows for sensitive tool operations

### Slide 21: Human-in-the-Loop Policies
- When must agents escalate to humans?
- Confidence threshold policies
- Sensitive action policies (financial, PII, deletion)
- Escalation routing: who gets what, and how fast
- Audit: log every escalation decision

### Slide 22: Responsible AI Guardrails
- Content filtering for agent outputs
- Grounding enforcement: agents must cite sources
- Hallucination detection and mitigation
- Bias monitoring for agent decisions
- [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/)

### Slide 23: Multi-Agent Security
- Credential isolation between agents
- Cross-boundary trust models
- State synchronization security
- Network segmentation for agent-to-agent communication
- When NOT to use multi-agent (complexity vs. value)

### Slide 24: Agent Audit Trail
- Log every: tool call, data access, decision, escalation, output
- Retention policies for agent logs
- Compliance reporting for regulated industries
- Forensic analysis: reconstruct agent decision chain

### Slide 25: Key Takeaways — Module 3
- Governance before deployment, not after
- Least privilege for data and tools
- Human-in-the-loop is a design decision, not an afterthought
- Responsible AI guardrails are mandatory, not optional
- Audit everything

---

## Section 4: Cost Optimization & Scaling (5-6 slides)

### Slide 26: AI Workload Cost Model
| Cost Component | Driver | Optimization Lever |
|---------------|--------|-------------------|
| Model inference | Tokens (prompt + completion) | Smaller models, shorter prompts, caching |
| AI Search | Tier + query volume | Right-size tier, optimize index |
| Compute | Container App instances | Autoscaling, right-size SKU |
| Storage | Document + chat history | Lifecycle policies, archive |
| Networking | Private endpoints, egress | Minimize cross-region traffic |

### Slide 27: Model Selection Economics
- GPT-4o vs. GPT-4o-mini vs. GPT-3.5-turbo: cost per 1K tokens
- "Route simple queries to smaller models, complex to larger"
- Prompt optimization: reduce token count without losing quality
- Response caching for common queries

### Slide 28: Scaling Patterns
- Azure Container Apps autoscaling (HTTP, KEDA, custom)
- Azure OpenAI provisioned throughput vs. pay-as-you-go
- AI Search replica scaling for query throughput
- Cosmos DB autoscale RUs

### Slide 29: Cost Allocation & Showback
- Tagging strategy: by team, project, environment, workload
- Azure Cost Management budgets and alerts
- Per-request cost tracking (tokens × price per token)
- Chargeback models for shared AI infrastructure

### Slide 30: Key Takeaways — Module 4
- Understand the cost model before deploying to production
- Model selection is the biggest cost lever
- Autoscale everything, right-size everything
- Tag resources for showback from day one

---

## Section 5: Wrap-up & Production Planning (4-5 slides)

### Slide 31: Production Readiness Checklist
- [ ] CI/CD pipelines: infra + app (Module 1)
- [ ] Monitoring dashboards and alerts configured (Module 2)
- [ ] Agent governance policies defined and enforced (Module 3)
- [ ] Cost budgets and scaling limits set (Module 4)
- [ ] Operational runbooks documented
- [ ] Incident response plan defined
- [ ] Responsible AI review completed
- [ ] Load testing passed
- [ ] Security review / penetration test completed

### Slide 32: Operational Runbook Template
- Incident classification (P1-P4) for AI workloads
- Agent-specific failure modes: tool failures, model degradation, hallucination spike
- Escalation paths and on-call rotation
- Recovery procedures per failure type
- Post-incident review template

### Slide 33: The Full Journey — Workshop Series Recap
- **WS1**: Understand the architecture, make decisions
- **WS2**: Deploy infrastructure, build RAG, explore agents
- **WS3**: Operationalize with CI/CD, monitoring, governance, cost
- **Partner outcome**: End-to-end capability to take customers from concept to production

### Slide 34: Resources
| Resource | Link |
|----------|------|
| AI Landing Zones Repo | github.com/Azure/AI-Landing-Zones |
| CAF AI Agent Adoption | learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/ |
| CAF Govern & Secure | learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure |
| CAF Manage Agents | learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage |
| Azure Monitor Baseline Alerts | azure.github.io/azure-monitor-baseline-alerts/ |
| Partner Quick Reference | (internal) |

### Slide 35: Q&A & Thank You
- Questions?
- Feedback survey link
- AI Center of Excellence V2 | Partner Enablement Team

---

## 📝 Slide Design Notes

- Match WS1/WS2 branding and style
- More architecture diagrams, fewer code blocks (compared to WS2)
- Include real pipeline YAML screenshots where possible
- Dashboard screenshots > dashboard descriptions
- Agent governance slides should feel "new and important" — use callout boxes

---

**Total Estimated Slides**: 33-38  
**Target Creation Time**: 6-8 hours  
**Authors**: Arturo Quiroga (PSA), Ana Lopez Moreno (PSA), George Bittencourt (PSA) & Guilherme Nogueira (PSA)  
**Created**: February 25, 2026
