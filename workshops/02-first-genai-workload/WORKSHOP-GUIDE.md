# Workshop 2: Facilitation Guide

**Purpose**: Step-by-step guide for instructors delivering Workshop 2  
**Duration**: 3-4 hours (hands-on lab)  
**Format**: Instructor-led with live hands-on labs (virtual or in-person)

---

## 🎯 Before the Workshop

### 1 Week Before
- [ ] Confirm participant list and roles
- [ ] Ensure all participants completed Workshop 1 (or have equivalent knowledge)
- [ ] Send pre-workshop preparation email with:
  - [ ] Prerequisites checklist (Azure CLI, azd CLI, subscriptions, quota)
  - [ ] Link to [Deploy-Your-AI-App Repo](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
  - [ ] Instructions to verify Azure OpenAI quota in their target region
  - [ ] Link to [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
- [ ] Test the full deployment in your demo subscription (~45 min + verification)
- [ ] Prepare a pre-deployed environment as backup (in case live deployments fail during workshop)
- [ ] Review [Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md)

### Day Before
- [ ] Re-verify demo subscription — ensure deployment is still running and resources are healthy
- [ ] Prepare screen layouts: Terminal, Portal, AI Foundry tabs ready
- [ ] Review troubleshooting section at end of this guide
- [ ] Confirm co-facilitator or TA availability (strongly recommended for hands-on labs)

### 30 Minutes Before
- [ ] Start the meeting room/call
- [ ] Open all tabs: Portal, AI Foundry, Terminal with repo cloned
- [ ] Pre-type key commands in a text file for quick copy-paste during demo
- [ ] Share materials links and repo URL in chat
- [ ] Welcome early joiners — have them start setup validation immediately

---

## 📋 Detailed Facilitation Script

---

### Module 1: Quick Recap & Deployment Strategy (0:00 - 0:20)

#### Welcome & Setup Validation (5 min) — Slides 1-4
```
"Welcome back to the AI Landing Zones workshop series. Today is 
Workshop 2 — From RAG to Agents. This is a hands-on lab, so we'll 
be deploying real infrastructure and building on top of it.

Before we begin, let's validate your setup. Please run the following 
in your terminal right now:

  az --version        (need 2.61.0+)
  azd version         (need 1.15.0+)
  az account show     (confirm you're logged in)

Raise your hand — or type in chat — if anything fails. 
We have a few minutes to troubleshoot."
```

**Instructor action**: Walk the room or check chat. Common issues:
- CLI not installed → Pair with neighbor
- Not logged in → `az login` / `azd auth login`
- Wrong subscription → `az account set --subscription <id>`

#### Workshop 1 Recap (5 min) — Slides 5-6
```
"Quick recap of where we left off. In Workshop 1, we covered:
- AI Landing Zones are production-ready application landing zones 
  for AI workloads
- Two reference architectures: with and without Platform Landing Zone
- The Design Checklist with 40+ recommendations across 10 areas
- Four deployment paths: azd, Bicep, Terraform, Portal

Today we go from understanding to DOING. We'll deploy this Landing 
Zone, build a RAG application on it, and explore when customers 
should graduate from RAG to AI agents.

The narrative arc today: Deploy → Build → Decide → Operate."
```

#### What Gets Deployed (5 min) — Slides 7-8
```
"Let's preview what you're about to deploy — roughly 30+ Azure 
resources, all configured with production-grade security defaults.

[Walk through Slide 7 resource list]

We're using the 'without Platform Landing Zone' variant today for 
speed. In production, your enterprise customers would likely have an 
existing platform landing zone — but the AI Landing Zone layer is 
the same regardless.

All security controls we discussed in Workshop 1 are baked in — 
private endpoints, managed identity, RBAC, network segmentation. 
You don't need to configure these manually."
```

#### Deployment Path (5 min) — Slide 9
```
"We're using azd up today because it's the fastest path to a 
working deployment. In about 30-45 minutes, you'll have a 
production-grade environment.

[Show comparison table]

Important distinction: azd is perfect for labs, PoCs, and demos. 
For customer production deployments, partners should use Bicep or 
Terraform modules for full customization. See the IaC Decision 
Framework doc for the complete comparison.

Any questions before we start deploying?"
```

---

### Module 2: Deploy the Landing Zone — HANDS-ON LAB (0:20 - 1:20)

> **⏱ Total module time**: ~60 min  
> **Lab time**: ~15 min hands-on + ~30-45 min deployment wait  
> **Strategy**: Participants start deployment, then use wait time for Portal walkthrough

#### Step 1 — Clone the Repository (5 min) — Slide 11
```
"Let's begin. Open your terminal and run the clone command.
This is on the slide — I'll paste it in chat too:

  git clone --recurse-submodules \
    https://github.com/microsoft/Deploy-Your-AI-Application-In-Production.git
  cd Deploy-Your-AI-Application-In-Production

The --recurse-submodules flag is critical. It pulls in the Bicep 
infrastructure modules. If you skip it, the deployment will fail.

Once cloned, take 30 seconds to look at the repo structure:
- /infra  → Bicep templates (this is what deploys everything)
- /src    → Application code  
- /docs   → Documentation and parameter guide"
```

**Instructor action**: Verify everyone has cloned successfully. Check for:
- Git not installed → Use GitHub UI to download ZIP (less ideal)
- Submodules missing → `git submodule update --init --recursive`

#### Step 2 — Initialize and Configure (5 min) — Slide 12
```
"Now let's initialize the project:

  azd init

This will prompt you for an environment name. Use a short, 
unique name — I suggest your initials plus 'ws2', like 'aq-ws2'.

Next, review the parameters. The most important decisions:
- Region: Pick a region where you have Azure OpenAI quota. 
  Check your quota first if you're unsure.
- Model: GPT-4o is our default, but gpt-35-turbo works too if 
  quota is limited.

See the Parameter Guide linked in the resources for the full list."
```

#### Step 3 — Deploy (3 min) — Slide 13
```
"Ready? Let's deploy:

  azd up

This will take 30-45 minutes. You'll see resource groups being 
created, networking deployed, PaaS services configured, and 
finally the application code deployed.

DON'T close your terminal. Let it run.

While we wait, I'll take you on a guided tour through the Portal 
to show you what's being built."
```

**Instructor action**: Start your own `azd up` (or show the pre-deployed environment).

#### Portal Walkthrough during Deploy Wait (~30 min) — Slides 14-16

> **Note**: Use your pre-deployed environment for this walkthrough.

##### Networking Layer (10 min) — Slide 14
```
"Let me show you what's happening in the Portal with my 
pre-deployed environment.

[Navigate to Resource Group → Virtual Network]

First, the networking layer. Notice:
- The VNet has multiple subnets — one per service category
- Every PaaS service has a private endpoint — no public IPs
- NSGs on each subnet enforce traffic rules

This directly implements Design Checklist items N-R3 and N-R4 
from Workshop 1. The deployment templates do this automatically — 
partners don't need to wire this up manually.

[Click into a private endpoint]

See how this endpoint maps to a specific service? The DNS is 
configured in the private DNS zone so all traffic stays private."
```

##### AI Services Layer (10 min) — Slide 15
```
"Now let's look at the AI services.

[Navigate to AI Foundry Hub → Project]

AI Foundry Hub is the management layer. The Project is where 
your workloads run. Think of Hub as the organization level 
and Project as the team/workload level.

[Show OpenAI deployments]

Here are the model deployments — GPT-4o for generation, an 
embedding model for vectorizing your documents.

[Show AI Search]

AI Search is our retrieval layer — this is the 'R' in RAG. 
The index will be populated with your documents.

[Show Cosmos DB]

And Cosmos DB stores chat history and conversation memory — 
Design Checklist items D-R1 and D-R2."
```

##### Security Layer (10 min) — Slide 16
```
"Finally, the security layer — the most important part for 
enterprise customers.

[Show Managed Identities]

Every service authenticates using managed identity. No passwords, 
no connection strings, no API keys in code. This maps to Design 
Checklist item I-R1.

[Show Key Vault]

Key Vault manages any secrets that still need centralized storage.

[Show RBAC assignments]

And RBAC assignments follow least privilege — each service gets 
exactly the permissions it needs and nothing more.

[Show Defender for Cloud recommendations, if any]

Defender for Cloud monitors the entire deployment for security 
posture issues."
```

#### Step 4 — Validate Deployment (5 min) — Slide 17
```
"By now, deployments should be completing — or very close. 
Let's validate. Run:

  azd show

This lists all deployed resources and their status. 
Now let's check in the Portal:

✅ All resources created?
✅ Private endpoints active?
✅ RBAC assignments in place?
✅ No public network access?
✅ Diagnostic settings pointing to Log Analytics?

If anything looks wrong, check the troubleshooting section — 
I'll paste the link in chat."
```

**Common issues during validation**:
- Deployment timed out → Check `azd up` output for the failed step, re-run
- Insufficient quota → Switch region or model, then re-deploy
- RBAC propagation delay → Wait 5 min and check again

#### Takeaways (2 min) — Slide 18
```
"So, what did we just accomplish?

We deployed a complete, production-ready AI Landing Zone — 
30+ resources, private networking, managed identity, RBAC, 
monitoring — all from a single 'azd up' command.

This is what partners should be showing customers:
'Here's your secure AI foundation. Let's build on it.'

Let's take a break and then come back to build the application."
```

---

### ☕ BREAK (1:20 - 1:30) — 10 minutes

```
"Let's take a 10-minute break. When we come back, we'll deploy 
and test a RAG chat application on the infrastructure you just built.

If your deployment is still running, leave the terminal open."
```

---

### Module 3: Configure & Deploy RAG Application — HANDS-ON LAB (1:30 - 2:10)

#### RAG Architecture Overview (5 min) — Slide 19
```
"Welcome back. Now we build on top of the Landing Zone.

The application we're deploying is a RAG chat — Retrieval-Augmented 
Generation. Here's how it works:

  User asks a question
  → Container App receives the request
  → AI Foundry orchestrates the flow
  → AI Search retrieves relevant document chunks
  → OpenAI generates a response grounded in those chunks
  → Response returned to user

The key word is 'grounded.' The model doesn't make things up — 
it answers based on your data. That's the value of RAG."
```

#### Step 1 — Configure AI Foundry (10 min) — Slide 20
```
"Let's navigate to AI Foundry in the Portal.

[Open AI Foundry → Your Project]

Check the following:
1. Model deployments — you should see GPT-4o and an embedding model
2. Connections — verify AI Search, Cosmos DB, and Storage are connected
3. Tracing — enable if not already on (we'll use this in Module 5)

If anything is missing, the deployment may not have connected 
resources correctly. Check the azd output for errors."
```

**Instructor action**: Show your own AI Foundry project as reference.

#### Step 2 — Ingest Sample Data (10 min) — Slide 21
```
"Now we need data to retrieve from. The repo includes sample 
documents in the /data folder.

Let's upload them:
1. Navigate to the Storage Account → Blob containers
2. Find the 'documents' container
3. Upload the sample documents

Then configure the AI Search indexer:
1. Open AI Search → Indexers
2. The indexer should be pre-configured by the deployment
3. Run it to process the documents and create embeddings

This step turns your documents into searchable vectors. 
The quality of your index directly impacts the quality of 
responses — remember: garbage in, garbage out."
```

#### Step 3 — Deploy and Test (10 min) — Slide 22
```
"Let's test the application.

Navigate to the Container App endpoint — you can find the URL 
in the azd output or in the Portal under your Container App 
→ Overview → Application URL.

Open it in your browser. You should see a clean chat interface.

Try these sample queries:
1. A straightforward question from the sample data
2. A follow-up question (tests conversation memory via Cosmos DB)
3. A question OUTSIDE the data (tests grounding — it should 
   say it doesn't have that information, not hallucinate)

Notice how every response cites its source? That's RAG working 
as intended."
```

#### Understanding the Flow (5 min) — Slide 23
```
"Let's peek under the hood. Open AI Foundry → Tracing.

Find the trace from your last query and expand it. You can see:
- The search query that was sent to AI Search
- The documents that were retrieved
- The full prompt that was sent to the model (system + context + user)
- Token counts: prompt tokens + completion tokens
- Latency at each step

This is important for partners because customers will ask 
'how much does this cost?' and 'how fast is it?' — the answers 
are right here in the traces."
```

#### When RAG Is Enough (5 min) — Slide 24
```
"Before we move on to agents, let's be clear about when RAG 
is the right answer — because for many customers, it is.

RAG is enough when:
- The use case is document Q&A, knowledge base, or search
- Inputs are well-defined and outputs are predictable
- Low latency and cost matter more than complex reasoning
- No need for tool orchestration or multi-step workflows

The partner talking point: 'Not every AI workload needs an agent. 
Start with RAG. Prove value. Graduate when the use case demands it.'

This is a credibility builder — it shows you're giving honest, 
right-sized recommendations, not upselling complexity."
```

#### Takeaways (2 min) — Slide 25
```
"So we've now deployed infrastructure AND an application.

Key points:
- RAG is the foundation workload on AI Landing Zones
- Quality of retrieval = quality of responses 
- The Landing Zone provides everything RAG needs out of the box
- Most customers should start here

Next, let's explore when and how to go beyond RAG."
```

---

### Module 4: From RAG to Agents (2:10 - 2:40)

#### The RAG → Agent Spectrum (5 min) — Slide 26
```
"You just built a RAG application — a fixed pipeline: query, 
search, generate, respond. It works the same way every time.

Now imagine the customer says: 'I don't just want my users to 
ASK questions. I want the system to DO things — check order 
status, update records, file tickets, and handle edge cases.'

That's when you move from RAG to agents.

The key distinction:
- RAG: You design the pipeline. The model fills in the blanks.
- Agent: The model designs the pipeline. It decides what tools 
  to use, in what order, based on the user's intent.

This is from the CAF AI Agent Adoption framework — the same 
Cloud Adoption Framework you're already familiar with."
```

#### When to Graduate (5 min) — Slide 27
```
"The CAF provides a decision tree for this. Graduate to agents 
when the workload requires:

1. Dynamic decision-making — multi-step reasoning with 
   conditional logic ('if status is X, do Y, otherwise Z')
2. Complex orchestration — chaining multiple tools or APIs 
   together in a single interaction
3. Adaptive behavior — handling ambiguous inputs where the 
   system must interpret intent, not just match keywords

If none of those apply? Stay with RAG. Seriously.

The decision tree is in the CAF AI Agent Adoption docs — 
I'll share the exact link."
```

#### Three Agent Types (5 min) — Slide 28
```
"The CAF defines three agent types, in order of complexity:

1. Productivity Agents: Retrieve and synthesize information. 
   Very similar to what we just built — they add reasoning 
   but the infrastructure needs are minimal.

2. Action Agents: Perform specific tasks via APIs and tools. 
   Now you're adding Logic Apps, Functions, APIM connectors. 
   Your Landing Zone needs to support these integrations.

3. Automation Agents: Multi-step processes with minimal human 
   oversight. These need orchestration, triggers, monitoring, 
   and robust governance.

Same Landing Zone foundation — different workload complexity 
running on top."
```

#### Microsoft Foundry (5 min) — Slides 29-30
```
"Where do agents actually run? On Microsoft Foundry — which is 
what your AI Landing Zone powers.

Foundry gives you two agent types:
- Declarative agents: Prompt-based, behavior-driven. Easier to 
  build, easier to version. Good starting point.
- Hosted agents: Code-first with custom libraries. Full control 
  over the logic. For complex, custom workloads.

Here's the key insight — look at this side-by-side comparison:

[Show Slide 30]

Everything in Foundry's 'standard setup with private networking' 
column? You already deployed it. VNet, private endpoints, managed 
identity, AI Search, Cosmos DB — it's all there.

Your AI Landing Zone IS the enterprise Foundry environment. 
Partners who deploy the Landing Zone are already set up for agents."
```

#### Single vs. Multi-Agent (3 min) — Slide 31
```
"One more decision: single agent or multi-agent?

Start single unless you must separate for:
- Hard security or compliance boundaries
- Multiple teams owning separate domains
- Known future growth across business units

Multi-agent adds complexity: latency at handoffs, credential 
management across boundaries, state synchronization. 

Rule of thumb: prototype single, test, then decide."
```

#### Demo — Foundry Agents (Optional, 5 min) — Slide 32
```
"If time permits, let me show you the Foundry Agent Playground.

[Navigate to AI Foundry → Agents section]

Watch how the agent:
1. Receives a user query
2. Decides which tool to call (search, function, etc.)
3. Reasons about the results
4. May call additional tools
5. Synthesizes a final response

Compare this with the RAG flow from Module 3 — same 
infrastructure, fundamentally different behavior."
```

> **If no time**: "We won't be able to do the live demo, but 
> the Foundry Agent Quickstart link is in the resources — you 
> can try this in your own environment after the workshop."

#### Partner Conversation Framework (3 min) — Slide 33
```
"When you're sitting across from a customer, here's the flow:

1. Discover: 'What problem are you solving?'
2. Qualify: Use the decision tree — code, RAG, or agent?
3. Scope: Which agent type? Productivity, Action, or Automation?
4. Architecture: Single or multi-agent? SaaS or custom?
5. Deploy: AI Landing Zone → Configure Foundry standard setup
6. Iterate: Start simple, validate, then graduate

This is your playbook for turning Landing Zone conversations 
into agent workload conversations."
```

#### Takeaways (2 min) — Slide 34
```
"Module 4 summary:

- RAG is a subset of what agents can do. Start there.
- Graduate to agents when reasoning and orchestration are needed.
- The Landing Zone you deployed IS Foundry's standard setup.
- Three agent types match increasing infrastructure complexity.
- Use the decision tree and conversation framework with customers."
```

---

### Module 5: Monitoring & Observability (2:40 - 3:00)

#### What's Different About AI Monitoring (5 min) — Slide 35
```
"Traditional monitoring — CPU, memory, latency, error rates — 
still applies to AI workloads. But there's a new layer.

AI-specific monitoring adds:
- Token usage tracking (directly tied to cost)
- Response quality and relevance scoring
- Hallucination detection
- Retrieval quality (are the right documents being found?)
- Model drift over time

For agents, you also need:
- Tool execution monitoring (did the right tool get called?)
- Orchestration tracing (what was the reasoning chain?)
- Escalation tracking (when does the agent hand off to a human?)

Workshop 3 will go much deeper here. Today we'll look at what's 
already deployed and working."
```

#### What's Already Running (5 min) — Slide 36
```
"Good news — your azd up deployment already configured monitoring.

Let me show you what's there:

[Navigate to Application Insights → Live Metrics]

Application Insights is capturing every request to the Container 
App, including latency, error rates, and dependencies.

[Navigate to Log Analytics workspace]

Log Analytics has centralized diagnostic logs from every service — 
AI Search, Cosmos DB, OpenAI, Container Apps.

Key metrics to start watching:
- Response latency P50, P95, P99
- Token consumption per request
- Error rates by category
- AI Search query performance
- Cosmos DB RU consumption

These map to Design Checklist items M-R1 and M-R4."
```

#### AI Foundry Tracing (5 min) — Slide 37
```
"The most powerful monitoring tool for AI workloads is AI Foundry 
Tracing. Let's look at a trace from your Module 3 queries.

[Open AI Foundry → Tracing → Find a recent trace]

Expand the trace. You can see the complete chain:
1. Input received
2. Search query constructed
3. Documents retrieved (with relevance scores)
4. Full prompt assembled (system + context + user)
5. Model response generated
6. Token counts at each step
7. Latency at each step

This is where optimization happens. Slow search? Tune the index. 
Too many tokens? Reduce context window. High latency? Consider 
a smaller model for simple queries.

Workshop 3 will build dashboards around these metrics."
```

#### Takeaways (2 min) — Slide 38
```
"Module 5 takeaways:

- AI workloads need both traditional and AI-specific monitoring
- azd up deploys monitoring infrastructure by default
- AI Foundry Tracing gives end-to-end visibility
- Workshop 3 goes deeper: alerting, dashboards, GenAIOps, 
  cost optimization, and operational runbooks"
```

---

### Module 6: Wrap-up & Next Steps (3:00 - 3:15)

#### Workshop Summary (3 min) — Slide 39
```
"Let's recap what we accomplished today:

✅ Deployed a complete AI Landing Zone with 30+ resources
✅ Validated security controls against the Design Checklist
✅ Built and tested a RAG chat application end-to-end
✅ Learned when to graduate from RAG to AI agents
✅ Explored the Foundry agent platform running on your Landing Zone
✅ Reviewed monitoring and observability basics

You now have hands-on experience with the entire stack — from 
infrastructure to application to monitoring. This is what you 
bring to customer conversations."
```

#### Clean-up (2 min) — Slide 40
```
"If you want to remove all deployed resources:

  azd down

This tears down everything — the resource group and all contents.

OR — keep it running! Experiment with:
- Creating Foundry agents on top of the deployed infrastructure
- Testing model deployments with different parameters
- Exploring the monitoring dashboards

Just remember: resources cost money while they're running."
```

#### Resources (2 min) — Slide 41
```
"Key resources — all in the slide and I'll share in chat:

- AI Landing Zones repo on GitHub
- Deploy-Your-AI-App repo we used today
- CAF AI Agent Adoption guidance
- AI Foundry Agent Quickstart
- Design Checklist
- Partner Quick Reference Guide

These are your go-to links for customer conversations."
```

#### Next Steps (3 min) — Slides 42-43
```
"What to do after today:

1. Deploy again in your own subscription with different parameters
2. Create a Foundry agent on the deployed infrastructure
3. Read the full CAF AI Agent Adoption framework
4. Use the deployment + decision framework with your next customer
5. Attend Workshop 3: Landing Zones to Production — where we 
   cover CI/CD, GenAIOps, production monitoring, and scaling

Workshop 3 picks up exactly where we left off: you have a 
deployed workload. Now how do you operate it at scale?"
```

#### Q&A and Feedback (5 min) — Slide 44
```
"Questions? Let's open it up.

[Handle Q&A]

Before you leave, please fill out the feedback survey — the link 
is in the chat. Your feedback directly shapes the next workshop.

Thank you for your time today. Go build great things on Azure."
```

---

## 🛠 Troubleshooting Guide

### Deployment Issues

| Issue | Cause | Solution |
|-------|-------|---------|
| `azd up` fails at start | CLI not installed/outdated | `brew upgrade azure-dev` or install from docs |
| Deployment timeout | Slow region, resource limits | Re-run `azd up` — it resumes from last successful step |
| Insufficient quota | Not enough OpenAI TPM | Check quota: Portal → Azure OpenAI → Quotas, switch region |
| Submodules missing | Cloned without `--recurse-submodules` | `git submodule update --init --recursive` |
| RBAC errors | Permission propagation delay | Wait 5 min, retry; ensure Owner or Contributor + UAA |
| Private endpoint DNS issues | DNS zone not linked | Verify private DNS zones exist and are linked to VNet |
| Container App not starting | App code deployment failed | Check Container App logs in Log Analytics |

### Common Participant Questions

| Question | Response |
|----------|----------|
| "How much does this cost?" | ~$X/day depending on SKU selections. Main cost drivers: OpenAI TPM, AI Search tier, Cosmos DB RUs. Use `azd down` when not in use. |
| "Can I use Terraform instead of azd?" | Yes — see the IaC Decision Framework. Terraform modules available in the AI Landing Zones repo. |
| "What about data residency?" | Choose the region carefully. All data stays within the Azure region you select. Private endpoints ensure data doesn't traverse public internet. |
| "How do I add my own data?" | Replace the sample documents in Storage → configure the indexer → rebuild the index. Same process, different data. |
| "Is this production-ready?" | The infrastructure is production-grade. For production use: add CI/CD (Workshop 3), conduct load testing, tune model parameters, and implement LLMOps practices. |

---

## ⏱ Time Adaptation Guide

### Shorter Version (2.5 hours)
- Compress Module 1 to 10 min (skip detailed architecture walkthrough)
- During Module 2 deployment wait: do a shorter Portal walkthrough focusing on networking + security only
- Module 3: Demo-only approach (instructor deploys, participants follow along)
- Module 4: Keep all content (this is the critical new content)
- Module 5: Reduce to 10 min overview only
- Module 6: 10 min

### Longer Version (4+ hours)
- Expand Module 2: Include deeper IAM walkthrough, network topology deep dive
- Expand Module 3: Include data ingestion pipeline setup, custom data exercise
- Expand Module 4: Full Foundry agent build exercise (not just demo)
- Expand Module 5: Build a basic monitoring dashboard live
- Add Module 4b: Hands-on Foundry agent creation (30 min)

### Virtual Delivery Tips
- Use breakout rooms for hands-on steps (pairs work better than solo for troubleshooting)
- Share terminal and Portal in separate screens if dual-monitor
- Have a TA monitoring chat for deployment issues
- Record the session for async participants
- Post a "checkpoint" poll after each module: "Are you ready to move on?"

---

**Authors**: Arturo Quiroga (PSA) & Anahita Afshari (PSA)  
**Last Updated**: February 25, 2026
