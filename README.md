# Azure AI Landing Zones - Partner Guidance IP

Technical assets and guidance for Microsoft partners implementing Azure AI Landing Zones for production-ready Generative AI workloads.

## 🎯 Project Overview

This repository contains comprehensive guidance, workshops, and reference architectures to help Microsoft partners design, deploy, and operate enterprise-scale Azure AI Landing Zones. The content builds upon the official [Azure AI Landing Zones](https://github.com/Azure/AI-Landing-Zones) framework and incorporates best practices from Azure Foundry templates.

> **📌 Key Concept**: Azure AI Landing Zones are **application landing zones** within the [Cloud Adoption Framework (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/). They are NOT a separate landing zone type—they deploy INTO existing Azure Landing Zone architectures or as standalone environments. See [AI in Azure Landing Zones](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/#ai-in-azure-landing-zones) for official guidance.

**Target Audience**: Microsoft partners, solution architects, and technical consultants working with enterprise customers on AI adoption.

**Program**: AI Center of Excellence V2 - Partner Enablement

## 📋 Key Deliverables

### Partner Enablement Guides
- **[Partner Quick Reference Guide](docs/PARTNER-QUICK-REFERENCE.md)**: Curated navigation through official AI Landing Zone resources — includes CAF AI Agent Adoption guidance
- **[IaC Decision Framework](docs/IAC-DECISION-FRAMEWORK.md)**: Guidance for choosing between azd, Bicep, Terraform, or Portal — includes Foundry agent environment setup options
- **[Partner Engagement Methodology](docs/PARTNER-ENGAGEMENT-METHODOLOGY.md)**: 3-phase delivery framework for customer engagements
- **[Deliverables Roadmap](docs/DELIVERABLES-ROADMAP.md)**: Project plan with task ownership and milestones

### Workshops
- **[Workshop 1: Landing Zone Fundamentals](workshops/01-landing-zone-fundamentals/)**: 2-3 hour introduction to AI Landing Zones, agent taxonomy, and decision frameworks (draft)
- **[Workshop 2: From RAG to Agents](workshops/02-first-genai-workload/)**: 3-4 hour hands-on lab — deploy Landing Zone, build RAG app, explore AI agents (draft)
- **Workshop 3: Landing Zones to Production**: Gen AI OPS bridge + agent governance (planned)

### Presentations
- **[Partner Pitch Deck Outline](presentations/PARTNER-PITCH-DECK-OUTLINE.md)**: 17-20 slide business-value deck with CAF AI Agents framework

### Architecture
- **[Diagram References](architecture/diagrams/DIAGRAM-REFERENCES.md)**: Central index of all architecture diagrams with usage map across workshops and docs

### Tools & Workbooks
- **AI Landing Zones Workbook**: Excel-based assessment and planning tool (in `/workbooks/`)
- **Design Checklist**: Interactive version of official checklist for customer engagements

## 📁 Repository Structure

```
.
├── docs/                       # Partner enablement guides and documentation
│   ├── PARTNER-QUICK-REFERENCE.md       # Start here — curated navigation + CAF AI Agents
│   ├── IAC-DECISION-FRAMEWORK.md        # IaC selection + Foundry setup guidance
│   ├── PARTNER-ENGAGEMENT-METHODOLOGY.md  # 3-phase delivery framework
│   ├── DELIVERABLES-ROADMAP.md          # Project plan and tasks
│   └── TEAM-COORDINATION.md            # Collaboration guide
├── workshops/                  # Hands-on lab guides and exercises
│   ├── 01-landing-zone-fundamentals/    # Workshop 1 (draft)
│   └── 02-first-genai-workload/         # Workshop 2 (draft)
├── presentations/              # Partner-facing presentation decks
│   └── PARTNER-PITCH-DECK-OUTLINE.md    # Business-value pitch deck
├── architecture/               # Architecture diagrams and design patterns
│   └── diagrams/DIAGRAM-REFERENCES.md   # Diagram index with usage map
├── workbooks/                  # Excel-based assessment and planning tools
├── templates/                  # Reusable templates (IaC, checklists, etc.)
└── reference-materials/        # Links and external resources
```

## 🏗️ Architecture Scope

The AI Landing Zone architecture includes:

- **Azure AI Foundry Service**: Managed AI development platform
- **Generative AI Microservices**: Container-based application patterns
- **Enterprise Security**: Private endpoints, network isolation, identity management
- **Data & Knowledge**: Integration with Cosmos DB, AI Search, and enterprise data sources
- **Governance**: Policy management, compliance, and monitoring

## 🚀 Getting Started

1. **Start Here**: Read the [Partner Quick Reference Guide](docs/PARTNER-QUICK-REFERENCE.md) for curated paths through official resources
2. **Choose IaC Approach**: Use the [IaC Decision Framework](docs/IAC-DECISION-FRAMEWORK.md) to select deployment method
3. **Learn Fundamentals**: Work through [Workshop 1](workshops/01-landing-zone-fundamentals/) — concepts, architectures, and decision frameworks
4. **Deploy Hands-On**: Follow [Workshop 2](workshops/02-first-genai-workload/) — deploy a Landing Zone, build a RAG app, explore agents
5. **Review Workbooks**: Check `/workbooks/` for Excel-based assessment tools
6. **Track Progress**: See [Deliverables Roadmap](docs/DELIVERABLES-ROADMAP.md) for project status

## 📚 Key References

### MS Learn Training Path
- **[AI Center of Excellence Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/)** (1 hr 34 min) - Start here!
  - [Introduction to AI Center of Excellence](https://learn.microsoft.com/training/modules/intro-ai-center-excellence/) (29 min)
  - [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) (28 min)
  - [Guide AI workload operations](https://learn.microsoft.com/training/modules/guide-ai-operations-center-excellence/) (37 min)

### Official Microsoft Resources
- [Azure AI Landing Zones (Official)](https://github.com/Azure/AI-Landing-Zones)
- [AI Landing Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Deploy Your AI Application in Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
- [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) — Plan, Govern, Build, and Manage AI agents
- [Microsoft Foundry Documentation](https://learn.microsoft.com/azure/ai-foundry/)

### Framework Alignment
- [Cloud Adoption Framework - AI Scenario](https://learn.microsoft.com/azure/cloud-adoption-framework/scenarios/ai/)
- [Cloud Adoption Framework - AI Agents](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/)
- [Well-Architected Framework - AI Workloads](https://learn.microsoft.com/azure/well-architected/ai/)

## 👥 Contributors

### AI Landing Zones Team
- **Arturo Quiroga** - Partner Solutions Architect (PSA) - Architecture & Deliverables
- **Anahita Afshari** - Partner Solutions Architect (PSA) - Workshop Development
- **Jason Virtue** - Partner Solutions Architect (PSA) - Program Lead

### Gen AI OPS Collaboration
- **Ana Lopez Moreno** - Partner Solutions Architect (PSA) - Gen AI OPS Accelerator
- **George Bittencourt** - Partner Solutions Architect (PSA) - Gen AI OPS
- **Guilherme Nogueira** - Partner Solutions Architect (PSA) - Gen AI OPS


## 📅 Timeline

- **Q3 FY2026**: Initial development and partner feedback
- **Jan 29, 2026**: Phase 1 complete — Partner enablement guides and Workshop 1 foundation
- **Feb 25, 2026**: CAF AI Agents integration across all deliverables, Workshop 2 scaffold complete, P0-P2 enhancements done
- **Feb 28, 2026**: Workshop 3 planning review
- **Mar 2026**: Workshop pilots, IaC template development, V2 contribution ready for AI CoE

## 🤝 Contributing

This is an internal Microsoft project for partner enablement. Team members should:
- Review the [Team Coordination Guide](docs/TEAM-COORDINATION.md) for collaboration processes
- Check the [Deliverables Roadmap](docs/DELIVERABLES-ROADMAP.md) for task ownership
- Follow the "reference, don't recreate" principle - link to official docs when possible

## 📄 License

Microsoft Internal Use - Partner Enablement

---

**Last Updated**: February 25, 2026  
**Status**: Active Development 🚧  
**Phase**: 2 In Progress — Workshops & CAF AI Agents Integration
