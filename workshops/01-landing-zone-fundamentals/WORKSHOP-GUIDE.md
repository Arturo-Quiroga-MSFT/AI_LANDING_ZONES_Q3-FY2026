# Workshop 1: Facilitation Guide

**Purpose**: Step-by-step guide for instructors delivering Workshop 1  
**Duration**: 2-3 hours  
**Format**: Instructor-led (virtual or in-person)

---

## 🎯 Before the Workshop

### 1 Week Before
- [ ] Confirm participant list and roles
- [ ] Send pre-workshop preparation email with:
  - [ ] Link to [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md)
  - [ ] Link to [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
  - [ ] Prerequisites reminder
- [ ] Test all links in presentation
- [ ] Prepare demo subscription (optional)

### Day Before
- [ ] Review presentation and talking points
- [ ] Prepare backup content for common questions
- [ ] Test connectivity and screen sharing
- [ ] Confirm co-facilitator roles (if applicable)

### 30 Minutes Before
- [ ] Open all browser tabs with reference links
- [ ] Start meeting room/call
- [ ] Share materials link in chat
- [ ] Welcome early joiners

---

## 📋 Detailed Facilitation Script

### Opening (0:00 - 0:15)

#### Welcome (5 min)
```
"Welcome to the AI Landing Zones Fundamentals workshop. I'm [Name], 
and I'll be facilitating today's session.

This workshop is part of the AI Center of Excellence partner enablement 
program. Our goal today is to equip you with the knowledge to help your 
customers deploy production-ready AI workloads on Azure faster and more 
securely.

By the end of today, you'll be able to:
- Explain what AI Landing Zones are and why they matter
- Navigate the official design guidance
- Choose the right deployment approach for different scenarios
- Have meaningful technical conversations with customers"
```

#### Introductions (5 min)
```
"Let's do quick introductions. Please share:
- Your name
- Your role and organization
- One thing you hope to learn today

[Go around the room or use chat]"
```

#### Logistics (5 min)
```
"A few housekeeping items:
- We'll run for about [2-3] hours
- There's a break after Module 2
- Questions are welcome anytime - raise hand or use chat
- Materials are linked in the chat
- [Recording notice if applicable]

Any questions before we begin?"
```

---

### Module 1: What is AI Landing Zone? (0:15 - 0:40)

#### Opening Hook (2 min)
```
"Let me start with a question: How many of you have had customers 
ask about deploying Gen AI applications?

[Wait for responses]

And how many have seen those conversations stall when security, 
governance, or scalability comes up?

[Wait for responses]

That's exactly what AI Landing Zones are designed to solve."
```

#### Key Concepts (10 min)

**Talking Points**:
- Define AI Landing Zone: "A secure, resilient, and scalable reference architecture"
- It's not just documentation—it includes working IaC code
- Purpose-built for Azure AI Foundry and Gen AI workloads
- Aligns with existing Azure best practices (CAF, WAF)

**Show**: Official [README](https://github.com/Azure/AI-Landing-Zones#readme)

```
"Notice it's hosted on the Azure GitHub organization—this is official 
Microsoft guidance, not a community project. It has contributors from 
the Azure architecture team."
```

#### CAF/WAF Alignment (8 min)

**Talking Points**:
- AI Landing Zone = Application Landing Zone in CAF terms
- Part of "AI Ready" stage in AI adoption journey
- Follows WAF design principles for AI workloads

**Show**: CAF AI Ready diagram from slide deck

```
"This isn't a one-off solution. It integrates with the broader 
cloud adoption story your customers are likely already familiar with."
```

#### Use Cases (5 min)

**Talking Points**:
- Chat applications with RAG
- AI Agents
- Document processing
- Code modernization
- Content generation

```
"The architecture is flexible enough to support multiple patterns. 
You don't need separate landing zones for different use cases—one 
foundation supports many workloads."
```

#### Check for Understanding
```
"Quick check: Can someone explain in their own words what makes 
AI Landing Zone different from just deploying Azure AI services 
directly?

[Desired answer: It's a pre-built foundation with security, 
networking, governance built in—not starting from scratch]"
```

---

### Module 2: Reference Architectures (0:40 - 1:10)

#### Two Options Introduction (3 min)
```
"There are two main architecture patterns, and choosing between them 
depends on your customer's starting point.

Option 1: With Platform Landing Zone - for enterprises with existing 
Azure infrastructure

Option 2: Without Platform Landing Zone - for greenfield or standalone 
deployments

Both are production-ready. Let's look at each."
```

#### With Platform Landing Zone (10 min)

**Show**: [Architecture diagram](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)

**Talking Points**:
- Leverages existing hub-spoke networking
- Uses central services: Firewall, Bastion, DNS
- AI workload is an application landing zone subscription
- Best for: enterprises, regulated industries, large deployments

```
"Walk through the layers from top to bottom:
- Management plane at the top
- Hub networking in the middle
- Application landing zone with AI services
- Notice all the private endpoints—no public exposure"
```

**Discussion Prompt**:
```
"Who here has customers with existing Azure Landing Zones deployed? 
What's your experience integrating new workloads?"
```

#### Without Platform Landing Zone (10 min)

**Show**: [Architecture diagram](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)

**Talking Points**:
- Self-contained in a single subscription
- Includes its own networking, security, governance
- Faster to deploy for isolated scenarios
- Best for: PoCs, smaller orgs, quick starts
- Can migrate to platform model later

```
"This is essentially a 'complete' landing zone in miniature. 
It's not less secure—it just manages everything internally 
rather than relying on shared platform services."
```

#### Component Deep-Dive (10 min)

**Walk through key layers**:

1. **AI Layer**: AI Foundry, AI Services, AI Search
2. **Compute Layer**: Container Apps, App Service
3. **Data Layer**: Cosmos DB, Storage, (optional) Fabric
4. **Security Layer**: Private endpoints, Key Vault, Managed Identity
5. **Governance Layer**: Defender, Purview, Policy, Monitor

```
"Note how every PaaS service connects via private endpoint. 
This is a non-negotiable in enterprise deployments."
```

#### Check for Understanding
```
"When would you recommend the standalone architecture over the 
platform-integrated one?

[Desired answers: PoC, greenfield, smaller org, faster deployment, 
customer without existing ALZ]"
```

---

### Break (1:10 - 1:20)

```
"Let's take a 10-minute break. When we come back, we'll dive into 
the Design Checklist—the most practical tool you'll use with customers.

Feel free to explore the repos we've shared in the meantime."
```

---

### Module 3: Design Checklist Walkthrough (1:20 - 2:00)

#### Introduction (5 min)

**Show**: [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)

```
"This is your new best friend for customer engagements. The Design 
Checklist has 40+ recommendations across 10 design areas.

Think of it as:
- Assessment tool for brownfield environments
- Design guide for greenfield deployments
- Conversation framework with customers

Let's walk through the key areas."
```

#### 10 Design Areas Overview (5 min)

**Show table from slide deck**

```
"Quick orientation:
- Networking: 9 recommendations
- Identity: 6 recommendations
- Security: 5 recommendations
- Monitoring: 6 recommendations
- Cost: 4 recommendations
- Data: 3 recommendations
- Governance: 5 recommendations
- Reliability: 1 recommendation
- Resource Org: 4 recommendations
- Compute: 1 recommendation

We'll focus on the first four—they're where most conversations start."
```

#### Networking Deep-Dive (8 min)

**Walk through N-R1 to N-R9**

```
"Networking is usually the most complex area. Let me highlight the 
critical ones:

N-R3: Private endpoints everywhere - This is non-negotiable
N-R6: APIM as AI Gateway - Important for cost control and monitoring
N-R7: Firewall for egress - Control what the AI can access
N-R9: Restrict outbound by default - Data exfiltration prevention

These come up in almost every enterprise conversation."
```

#### Identity Deep-Dive (5 min)

**Walk through I-R1 to I-R6**

```
"Identity recommendations center on one theme: eliminate credentials.

I-R1: Managed Identity everywhere
I-R3: Entra ID instead of API keys
I-R6: Disable key-based access entirely

The goal is zero secrets in code or config."
```

#### Security Deep-Dive (5 min)

**Walk through S-R1 to S-R5**

```
"Security recommendations connect to the broader Azure security story:

S-R1: Defender for Cloud - Use existing tooling
S-R3: Purview - Data governance for AI
S-R4: MITRE ATLAS - AI-specific threat modeling
S-R5: AI Content Safety - Protect against prompt attacks"
```

#### Monitoring Deep-Dive (5 min)

**Walk through M-R1 to M-R6**

```
"Monitoring AI workloads has unique challenges:

M-R3: AI Foundry tracing - Understand what the model is doing
M-R5: Model drift detection - Know when accuracy degrades

This connects to the Gen AI OPS topic—Day 2 operations."
```

#### How to Use the Checklist (7 min)

```
"Practical usage:

1. ASSESSMENT: Walk through checklist with customer current state
2. GAP ANALYSIS: Identify what's missing or non-compliant
3. PRIORITIZATION: P0 (must-have), P1 (should-have), P2 (nice-to-have)
4. IMPLEMENTATION: Use IaC templates to deploy
5. VALIDATION: Re-run checklist post-deployment

This becomes your engagement framework."
```

**Activity** (if time allows):
```
"Take 2 minutes: Pick one design area and identify which recommendation 
you think customers most often miss. Share in chat."
```

---

### Module 4: Deployment Options (2:00 - 2:25)

#### Four Paths Introduction (3 min)

```
"Now that we understand what to build, let's talk about how to build it.

There are four deployment paths:
A. Azure Developer CLI (azd up) - Fastest
B. Bicep - Azure-native
C. Terraform - Multi-cloud
D. Portal - Coming soon

Each has its place. Let me show you when to use which."
```

#### Path A: azd up (5 min)

**Show**: [Deploy-Your-AI-App repo](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

```
"This is the fastest path to production:

git clone --recurse-submodules [repo]
azd up

In about 45 minutes, you have 30+ Azure resources deployed with:
- AI Foundry
- Microsoft Fabric
- Purview integration
- AI Search
- All networking configured

Use this for PoCs, demos, or when speed matters most."
```

#### Path B & C: Bicep vs Terraform (7 min)

**Show**: [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md)

```
"For custom deployments, the choice is usually Bicep or Terraform.

Bicep:
- Azure-native, first-class support
- No state file management
- Best Azure feature coverage
- Choose if: Azure-only, Azure DevOps, Microsoft-aligned

Terraform:
- Multi-cloud capable
- Flexible state management
- Mature ecosystem
- Choose if: Multi-cloud, existing Terraform investment

Both use Azure Verified Modules—same foundation, different syntax."
```

**Discussion**:
```
"What's the IaC landscape like with your customers? 
Mostly Bicep, Terraform, or mixed?"
```

#### Decision Framework (5 min)

**Show decision tree from slide deck**

```
"Simple decision tree:

1. Need fastest deployment? → azd up
2. Multi-cloud strategy? → Terraform
3. Azure-native team? → Bicep
4. No IaC expertise? → azd up (or wait for Portal)

There's a detailed framework in our partner resources if you need 
to justify the choice to a customer."
```

---

### Module 5: Partner Engagement Scenarios (2:25 - 2:45)

#### Four Scenarios Overview (3 min)

```
"Let's translate this to real customer conversations. 
I'll walk through four common scenarios we see."
```

#### Scenario 1: Enterprise with ALZ (5 min)

```
"Customer: Large enterprise, existing Azure Landing Zones, 
mature cloud practice

Approach:
- Use Bicep/Terraform with Platform LZ architecture
- Focus checklist on integration points
- Networking and Identity are key discussions
- Likely needs governance alignment

Questions to ask:
- 'What's your current ALZ configuration?'
- 'What central services exist (Firewall, Bastion)?'
- 'What governance policies apply?'"
```

#### Scenario 2: Greenfield/PoC (5 min)

```
"Customer: New to AI, exploring options, needs quick validation

Approach:
- Use azd up for fastest deployment
- Standalone architecture is fine
- Focus checklist on Resource Org and Cost
- Plan for evolution if PoC succeeds

Questions to ask:
- 'What's your timeline for this PoC?'
- 'What happens if it succeeds?'
- 'Who needs to see the results?'"
```

#### Scenario 3: Regulated Industry (4 min)

```
"Customer: Healthcare, finance, government—heavy compliance

Approach:
- Bicep with extensive security review
- Full checklist coverage, especially Security and Governance
- Document everything for auditors
- Involve compliance early

Questions to ask:
- 'What compliance frameworks apply?'
- 'What's your audit schedule?'
- 'Who approves architecture decisions?'"
```

#### Scenario 4: Cost-Sensitive (3 min)

```
"Customer: Limited budget, needs to optimize from day one

Approach:
- Start minimal, grow as needed
- Focus checklist on Cost area (CO-R1 to CO-R4)
- Consider PTU vs PAYGO carefully
- Auto-shutdown for non-prod

Questions to ask:
- 'What's your budget?'
- 'How predictable is your workload?'
- 'What's essential vs nice-to-have?'"
```

---

### Wrap-up (2:45 - 3:00)

#### Summary (5 min)

```
"Let's recap what we covered today:

1. AI Landing Zone is a production-ready foundation for Gen AI workloads
2. Two architecture options: with or without Platform Landing Zone
3. Design Checklist is your primary customer engagement tool
4. Four deployment paths: azd, Bicep, Terraform, Portal
5. Match your approach to customer context

The common thread: don't reinvent the wheel. Microsoft has done 
the hard work—your job is to apply it to customer situations."
```

#### Next Steps (3 min)

```
"Here's what I recommend as follow-up:

1. PRACTICE: Deploy a test environment using azd up
2. READ: Go through the Design Checklist in detail
3. APPLY: Use the Quick Reference Guide with your next customer
4. CONTINUE: Join Workshop 2 for hands-on deployment

Workshop 2 is where we actually deploy and configure a full 
Gen AI workload. That's the hands-on practice."
```

#### Q&A (5 min)

```
"We have about 5 minutes for questions. What would you like to 
discuss further?

[Handle questions]

For anything we can't answer today, feel free to reach out to 
the AI CoE team or post in our Teams channel."
```

#### Closing (2 min)

```
"Thank you for your time today. Please complete the feedback 
survey I'll send shortly—it helps us improve.

Materials are in the chat. The Design Checklist and Quick Reference 
Guide are your key resources.

Good luck with your customer engagements!"
```

---

## 📝 Instructor Tips

### Handling Common Questions

**"How is this different from just using Azure AI Foundry?"**
```
"AI Foundry is the development platform. AI Landing Zone is the 
enterprise foundation—networking, security, governance—that makes 
AI Foundry production-ready. Think of it as the difference between 
running code on your laptop vs deploying it in a hardened data center."
```

**"Can we use this for non-Gen AI workloads?"**
```
"Yes. The architecture supports both generative and non-generative AI 
workloads. The AI Foundry component handles various AI scenarios, 
including traditional ML."
```

**"What's the cost of a typical deployment?"**
```
"It varies significantly based on configuration. The Deploy-Your-AI-App 
repo has cost estimates in the documentation. Key variables are: 
compute size, PTU vs PAYGO, region, and optional services like Fabric."
```

**"Is this production-ready or just for demos?"**
```
"Production-ready by design. It implements the Well-Architected 
Framework for AI workloads. Many customers deploy to production 
directly from these templates."
```

### Adapting for Time

**If running short (2-hour version)**:
- Shorten Module 3 (Checklist) to overview only
- Skip detailed scenario discussions in Module 5
- Point to docs for self-study

**If running long (3+ hours)**:
- Add hands-on exploration of repos
- Include live demo of azd up (if prepared)
- Deeper Q&A after each module

---

## 📊 Post-Workshop

### Feedback Collection
Send survey within 24 hours asking:
1. Overall satisfaction (1-5)
2. What was most valuable?
3. What was confusing or missing?
4. Would you recommend to colleagues? (1-10)

### Follow-up Email
Send within 48 hours with:
- Recording link (if applicable)
- All resource links
- Workshop 2 registration
- Contact info for questions

---

**Workshop Owner**: Anahita Afshari (PSI)  
**Last Updated**: January 29, 2026  
**Status**: 🚧 Draft - Ready for Review
