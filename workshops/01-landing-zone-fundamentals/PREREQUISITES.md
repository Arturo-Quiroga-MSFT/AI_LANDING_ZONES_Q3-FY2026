---
title: Workshop 1 Prerequisites and Pre-Work
description: Complete prerequisites checklist, required Microsoft Learn modules, and pre-work materials for Workshop 1 AI Landing Zone Fundamentals
author: Arturo Quiroga (PSA)
ms.date: 2026-03-17
ms.topic: reference
---

## Overview

This document defines the complete prerequisites for **Workshop 1: AI Landing Zone Fundamentals**. Share this with participants at least **one week before** the workshop. Completing these prerequisites ensures all attendees start from a common baseline and maximizes hands-on time during the session.

## Knowledge Prerequisites

Participants should have working familiarity with the following concepts before attending.

### Required

* Azure fundamentals: subscriptions, resource groups, regions, and the resource hierarchy
* Azure Portal navigation: creating resources, viewing activity logs, managing access
* Networking basics: virtual networks, subnets, DNS, and IP addressing
* Identity concepts: Azure Active Directory/Microsoft Entra ID, RBAC roles

### Helpful but Not Required

* Infrastructure as Code concepts (Bicep or Terraform)
* Cloud Adoption Framework (CAF) basics
* Azure Well-Architected Framework (WAF) awareness
* Experience with Azure AI services (Azure OpenAI, AI Search)

## Required Microsoft Learn Modules (Pre-Work)

Complete these modules **before** the workshop. Total estimated time: **~1 hour 30 minutes**.

### Mandatory Modules

| # | Module | Duration | Why It Matters |
|---|--------|----------|----------------|
| 1 | [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) | 28 min | Core foundation — covers what AI Landing Zones are, why they exist, and how they fit into CAF. This is the single most important pre-read. |
| 2 | [Introduction to Azure Landing Zones](https://learn.microsoft.com/training/modules/intro-to-azure-landing-zones/) | 30 min | Establishes the platform vs. application landing zone distinction that Workshop 1 builds on. |
| 3 | [Design a Governance Strategy](https://learn.microsoft.com/training/modules/cloud-adoption-framework-govern/) | 30 min | Provides context for the governance and policy recommendations in the Design Checklist walkthrough. |

### Recommended Modules (Strongly Encouraged)

These modules deepen understanding but are not strictly required. Prioritize them if time allows.

| # | Module | Duration | Why It Matters |
|---|--------|----------|----------------|
| 4 | [AI Center of Excellence Learning Path](https://learn.microsoft.com/training/paths/ai-center-excellence/) (full path) | 1 hr 34 min | Comprehensive coverage of AI adoption strategy, governance, and organizational readiness. The mandatory Module 1 above is part of this path. |
| 5 | [Introduction to Azure AI Foundry](https://learn.microsoft.com/training/modules/introduction-to-azure-ai-foundry/) | 23 min | Introduces the primary AI development platform used in the landing zone reference architecture. |
| 6 | [Secure Azure AI Services](https://learn.microsoft.com/training/modules/secure-azure-ai-services/) | 45 min | Security patterns for AI services that align with the Design Checklist security recommendations. |

### Optional Deep-Dives

For participants who want to go further or have specific interest areas.

| # | Module | Duration | Topic |
|---|--------|----------|-------|
| 7 | [Manage Azure Landing Zones with Terraform](https://learn.microsoft.com/training/modules/manage-azure-landing-zone-terraform/) | 45 min | IaC with Terraform for landing zones |
| 8 | [What is Azure AI Search?](https://learn.microsoft.com/training/modules/intro-to-azure-search/) | 25 min | RAG retrieval layer fundamentals |
| 9 | [Plan AI agent workloads (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/business-strategy-plan) | 15 min read | When to use AI agents vs. classic RAG |

## Required Access and Tooling

### Must Have (All Participants)

* **Microsoft account** with access to [Microsoft Learn](https://learn.microsoft.com/) (to complete the pre-work modules)
* **GitHub account** (free tier sufficient) to browse the official repositories:
  * [Azure/AI-Landing-Zones](https://github.com/Azure/AI-Landing-Zones)
  * [Deploy-Your-AI-Application-In-Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)
* **Internet access** during the workshop for documentation references

### Recommended (For Hands-On Exercises)

* **Azure subscription** with Contributor role (for optional exercises)
  * If participants plan to deploy resources, review the [Cost Considerations](#cost-considerations) section below
* **VS Code** with the following extensions:
  * Azure Account
  * Bicep (if following Bicep path)
  * HashiCorp Terraform (if following Terraform path)
* **Azure CLI** (v2.60+) installed and authenticated
* **Azure Developer CLI (`azd`)** installed (for the `azd up` demo path)

## Pre-Work Materials to Review

Beyond the Microsoft Learn modules, participants should skim these resources (15-20 minutes total).

| Priority | Resource | Time | Description |
|----------|----------|------|-------------|
| Required | [AI Landing Zones GitHub README](https://github.com/Azure/AI-Landing-Zones#readme) | 5 min | Official project overview and repository structure |
| Required | [Partner Quick Reference Guide](../../docs/PARTNER-QUICK-REFERENCE.md) | 10 min | Curated navigation through official resources |
| Recommended | [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) | 10 min | Skim the 10 design areas and recommendation format (deep-dive happens in Module 3) |
| Optional | [CAF AI Agent Adoption](https://learn.microsoft.com/azure/cloud-adoption-framework/ai-agents/) | 10 min | Framework for planning AI agent workloads |
| Optional | [IaC Decision Framework](../../docs/IAC-DECISION-FRAMEWORK.md) | 5 min | Bicep vs. Terraform decision guidance |

## Cost Considerations

> **WARNING — Azure Costs Can Be Significant**
>
> If participants deploy resources during or after the workshop, be aware of the following high-cost services that are part of the AI Landing Zone architecture:
>
> * **Azure Firewall** — ~$900-1,250/month (Standard SKU). This is the single largest cost driver in the "with Platform Landing Zone" architecture.
> * **Azure Bastion** — ~$140-200/month (Standard SKU)
> * **Azure AI Services / Azure OpenAI** — Pay-per-use; costs depend on model selection and token volume
> * **Azure AI Search** — $75-300+/month depending on tier and replica count
> * **Azure DDoS Protection** — ~$2,944/month (Standard plan); evaluate if required
> * **Azure Cosmos DB** — Costs vary based on throughput; can be $25-500+/month
>
> **Estimated total for a full "with Platform LZ" deployment: $1,500-3,500+/month**
>
> **Estimated total for a "without Platform LZ" deployment: $300-1,200+/month**

### Cost Mitigation Strategies

* **Delete resources immediately after the workshop.** Do NOT leave a full landing zone running if it's not actively in use.
* Use `azd down` to tear down all resources deployed with `azd up`.
* For Bicep/Terraform deployments, run the corresponding destroy commands or delete the resource group.
* Consider using the "without Platform Landing Zone" architecture for learning purposes — it avoids Azure Firewall, Bastion, and DDoS Protection costs.
* Set up [Azure Cost Management budget alerts](https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets) before deploying.
* Use **dev/test pricing** where available.
* Consider Azure free trial credits ($200) or Visual Studio subscriber credits, but be aware that the full "with Platform LZ" deployment may exceed these.

### Resource Cleanup Checklist

After the workshop, ensure the following resources are removed:

* [ ] Delete the resource group(s) used for the deployment
* [ ] Verify no orphaned resources remain (private DNS zones, managed identities)
* [ ] Remove any role assignments created during the exercise
* [ ] Check for soft-deleted Key Vaults and purge if needed
* [ ] Confirm no reserved capacity or committed-use purchases were made accidentally

## Self-Assessment Checklist

Before attending, participants should be confident answering "yes" to the following:

* [ ] I completed the 3 mandatory Microsoft Learn modules listed above
* [ ] I can explain what a resource group and subscription are in Azure
* [ ] I understand the difference between a virtual network and a subnet
* [ ] I know what RBAC roles are and how they control access in Azure
* [ ] I have browsed the AI Landing Zones GitHub repository README
* [ ] I have reviewed the Partner Quick Reference Guide
* [ ] I understand the cost implications of deploying Azure resources (if I plan to do hands-on exercises)

## Facilitator Notes

### One Week Before

* Send this document (or a link to it) to all registered participants.
* Include a clear **deadline** for completing the mandatory Microsoft Learn modules (e.g., "Complete by [date], 2 days before the workshop").
* Emphasize the **cost warnings** — participants who plan to deploy resources should set up budget alerts in advance.

### Day of the Workshop

* Do a quick poll: "Who completed the pre-work modules?" to gauge the room.
* If fewer than 50% completed the pre-work, allocate 10 extra minutes to Module 1 for foundational context.
* Remind participants about resource cleanup and costs before any deployment exercise.

### Post-Workshop

* Send a reminder to **delete all deployed resources** within 24 hours.
* Share additional learning paths for participants who want to continue (see Recommended and Optional modules above).
