# Architecture Diagram References

**Purpose**: Central index of architecture diagrams used across workshops, presentations, and documentation  
**Usage**: Reference these when building slide decks, customer proposals, or technical documentation  
**Last Updated**: February 25, 2026

---

## 🏗️ AI Landing Zone Reference Architectures

### With Platform Landing Zone (Enterprise)
- **Source**: [AI-Landing-Zones Repo](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-with-platform.png)
- **Used in**: Workshop 1 (Module 2), Partner Quick Reference, Partner Pitch Deck
- **Description**: Full enterprise architecture with hub networking, firewall, DNS, Bastion, and shared services. AI Landing Zone deploys into an existing application landing zone subscription.

### Without Platform Landing Zone (Standalone)
- **Source**: [AI-Landing-Zones Repo](https://github.com/Azure/AI-Landing-Zones/blob/main/media/AI-Landing-Zone-without-platform.png)
- **Used in**: Workshop 1 (Module 2), Workshop 2 (Module 2 lab), Partner Quick Reference
- **Description**: Standalone deployment with its own networking. Used for PoCs, greenfield, and workshop labs.

---

## 🤖 CAF AI Agent Adoption Diagrams

### AI Agent Adoption Process (4-Phase)
- **Source**: [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)
- **Phases**: Plan → Govern & Secure → Build → Manage
- **Used in**: Partner Quick Reference (Agent Adoption section), Workshop 1 (Slide 10), Pitch Deck (Slide 7)
- **Notes**: Follows the same CAF lifecycle pattern; emphasize alignment with Landing Zone phasing

### Business Strategy & Planning
- **Source**: [Business Strategy & Plan](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan)
- **Key visual**: Use case prioritization matrix (Business Impact × Technical Feasibility × User Desirability)
- **Used in**: Pitch Deck (Slides 9-10), Workshop 1 (Scenario 5)

### Agent Decision Tree — When NOT to Use Agents
- **Source**: [Business Strategy — When Not to Use Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan#when-not-to-use-ai-agents)
- **Key visual**: Decision flowchart — deterministic code → RAG → agent
- **Used in**: Workshop 1 (Slide 10b), Workshop 2 (Module 4, Slide 27), Partner Quick Reference

### Technology Solutions Plan
- **Source**: [Technology Plan](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy)
- **Key visuals**: Build option spectrum (SaaS → PaaS → IaaS), Agent type comparison table
- **Used in**: Workshop 1 (Slide 10), Workshop 2 (Module 4, Slides 29-30), Pitch Deck (Slide 12)

### Single Agent vs. Multiple Agents
- **Source**: [Single vs. Multiple Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/single-agent-multiple-agents)
- **Key visual**: Decision criteria for single vs. multi-agent architecture
- **Used in**: Workshop 2 (Module 4, Slide 31), Partner Quick Reference

### Build & Secure Process
- **Source**: [Build Secure Process](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/build-secure-process)
- **Key visual**: Agent build lifecycle with security integration points
- **Used in**: Workshop 2 (Module 4 background), Workshop 3 (governance)

### Govern & Secure AI Agents
- **Source**: [Govern & Secure](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/govern-secure)
- **Key visuals**: Agent governance framework, security controls overlay
- **Used in**: Workshop 3 (agent governance module), Pitch Deck (Slide 8)
- **Notes**: Critical for regulated industry conversations

### Manage AI Agents
- **Source**: [Manage AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/manage)
- **Key visual**: Agent operations lifecycle (monitor, optimize, iterate)
- **Used in**: Workshop 3 (operations module), Workshop 2 (Module 5 preview)

---

## 🔧 Foundry & Deployment Diagrams

### AI Foundry Agent Environment Setup
- **Source**: [Foundry Environment Setup](https://learn.microsoft.com/azure/ai-foundry/agents/environment-setup)
- **Key visuals**: Basic vs. Standard setup comparison, network topology
- **Used in**: Workshop 2 (Module 4, Slide 30), IaC Decision Framework, Partner Quick Reference
- **Landing Zone alignment**: Foundry Standard (private networking) = AI Landing Zone architecture

### Agent Design Patterns
- **Source**: [Agent Design Patterns](https://learn.microsoft.com/azure/architecture/ai-ml/guide/ai-agent-design-patterns)
- **Key visuals**: Sequential, parallel, and conditional orchestration patterns
- **Used in**: Workshop 2 (Module 4 background), Workshop 3 (advanced topics)

---

## 📊 Presentation Decks

### CAF AI Agent Adoption — LevelUp Deck
- **File**: `presentations/CAF-AI-Agent-Adoption-LevelUp-2026-02-25.pptx`
- **Content**: End-to-end CAF AI Agent adoption walkthrough
- **Covers**: Plan → Govern & Secure → Build → Manage phases, agent taxonomy, technology options
- **Use for**: Partner deep-dives on CAF AI Agents framework, complements the Partner Pitch Deck Outline

### Deploy-Your-AI-App Architecture
- **Source**: [Deploy-Your-AI-Application-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
- **Key visual**: Full resource topology (~30 services)
- **Used in**: Workshop 2 (Module 2, Slide 7), IaC Decision Framework

---

## 📊 Usage Map

| Diagram | WS1 | WS2 | WS3 | Pitch Deck | Partner QR |
|---------|:---:|:---:|:---:|:----------:|:----------:|
| LZ with Platform | ✅ | — | ✅ | ✅ | ✅ |
| LZ without Platform | ✅ | ✅ | — | — | ✅ |
| Agent Adoption 4-Phase | ✅ | — | ✅ | ✅ | ✅ |
| Agent Decision Tree | ✅ | ✅ | — | — | ✅ |
| Technology Build Options | ✅ | ✅ | — | ✅ | ✅ |
| Single vs. Multi-Agent | — | ✅ | ✅ | — | ✅ |
| Govern & Secure Agents | — | — | ✅ | ✅ | — |
| Manage Agents | — | ✅ | ✅ | — | — |
| Foundry Setup | — | ✅ | ✅ | — | ✅ |
| Agent Design Patterns | — | ✅ | ✅ | — | — |
| Deploy-Your-AI-App | — | ✅ | ✅ | — | — |

---

## 🎨 Custom Diagram Guidance

When creating custom diagrams for presentations:
- Use [Microsoft Azure Architecture Icons](https://learn.microsoft.com/azure/architecture/icons/)
- Follow [Microsoft brand guidelines](https://www.microsoft.com/design/fluent/) for colors
- Tools: Visio, draw.io, PowerPoint, or Excalidraw
- Export as both PNG (for slides) and SVG (for docs)
- Store custom diagrams in this folder with descriptive names

### Naming Convention
```
<topic>-<detail>-<version>.png
```
Examples:
- `ai-landing-zone-with-platform-v1.png`
- `agent-decision-tree-simplified-v1.png`
- `foundry-standard-setup-mapping-v1.png`

---

**Authors**: Arturo Quiroga (PSA) & Anahita Afshari (PSA)
