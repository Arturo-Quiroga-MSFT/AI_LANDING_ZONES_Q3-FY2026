# AI Landing Zones - Deliverables Roadmap

**Co-Leads**: Arturo Quiroga (PSA) & Anahita Afshari (PSA)  
**Program**: AI Center of Excellence V2  
**Focus Areas**: AI Landing Zones (Primary) | Gen AI OPS (Secondary/Overlapping)  
**Timeline**: Q3 FY2026

---

## 🎯 Strategic Objectives

1. **Standardize** on best-in-class AI Landing Zone architecture patterns
2. **Enable** partners to deliver production-ready Gen AI workloads
3. **Bridge** the gap between infrastructure (Landing Zones) and operations (Gen AI OPS)
4. **Test & Validate** reference implementations for real-world scenarios

---

## 📦 Phase 1: Foundation & Architecture (Weeks 1-3)

### 1.0 Partner Enablement Foundation ✅ COMPLETED
**Status**: ✅ Done  
**Priority**: P0

- [x] **Partner Quick Reference Guide** 👤 *Arturo* → `/docs/PARTNER-QUICK-REFERENCE.md`
  - Curated navigation through official AI Landing Zone resources
  - 4 partner personas with tailored learning paths
  - Quick links to all official documentation sections
  
- [x] **IaC Decision Framework** 👤 *Arturo* → `/docs/IAC-DECISION-FRAMEWORK.md`
  - Decision tree: azd vs Bicep vs Terraform vs Portal
  - Comparison matrix with partner-focused criteria
  - Scenario-based recommendations

- [x] **Workshop 1 Foundation** 👤 *Anahita* → `/workshops/01-landing-zone-fundamentals/`
  - README, SLIDE-OUTLINE (49 slides), WORKSHOP-GUIDE created
  - Needs: EXERCISES.md, actual PowerPoint file

---

### 1.1 Partner Navigation Guides (Reference Official Content)
**Status**: 🔄 Reframed  
**Priority**: P1  
**Approach**: *Create partner cheat sheets that navigate official content—don't recreate what exists*

> **📌 Key Insight**: The official repos already have comprehensive coverage:
> - **Design Checklist**: 40+ recommendations across Networking (N-R1-9), Identity (I-R1-6), Security (S-R1-5)
> - **Architecture Diagrams**: With/without Platform Landing Zone variants
> - **Deploy-Your-AI-App**: Security Guidelines, Required Roles & Scopes docs

- [ ] **Quick Decision Cards** 👤 *Arturo* *(Optional enhancement)*
  - 1-page cheat sheets for common partner questions
  - Maps partner scenarios → official checklist sections
  - *Reference*: [AI-Landing-Zones-Design-Checklist.md](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
  
- [ ] **Network Patterns Quick Reference** 👤 *Anahita* *(Optional enhancement)*
  - 1-page summary linking to N-R1 through N-R9
  - Visual decision tree for hub-spoke vs standalone
  - *Reference*: Official architecture diagrams + Design Checklist Networking section
  
- [ ] **Security & Identity Cheat Sheet** 👤 *Arturo* *(Optional enhancement)*
  - Quick reference linking to I-R1-6 and S-R1-5 
  - Common partner security questions answered
  - *Reference*: [Required Roles & Scopes](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md)

**Deliverables** (Simplified):
- `/docs/cheatsheets/decisions.md` - 1-page decision helper *(Arturo, optional)*
- `/docs/cheatsheets/networking.md` - Network patterns quick ref *(Anahita, optional)*
- `/docs/cheatsheets/security-identity.md` - Security quick ref *(Arturo, optional)*

> **💡 Recommendation**: Skip creating these entirely unless partners specifically request them. The existing official docs + our Quick Reference Guide should suffice.

---

### 1.2 Component Deep-Dives
**Status**: � Reframed  
**Priority**: P2 *(Deprioritized - official docs cover this well)*

> **📌 Official Coverage**: The Design Checklist covers Compute (C-R1), Data (D-R1-3), and all component configuration. The Deploy-Your-AI-App repo includes working Bicep for AI Foundry, Container Apps, Cosmos DB, AI Search.

- [ ] **Partner Configuration Scenarios** 👤 *Both* *(Only if needed)*
  - Real-world parameter combinations for common partner scenarios
  - Troubleshooting tips beyond official docs
  - *Approach*: Add as workshop exercises rather than standalone docs

**Deliverables** (Simplified):
- Integrated into Workshop 2 hands-on labs instead of standalone documents
- Focus on partner-specific scenarios not covered in official docs

---

## 📦 Phase 2: Hands-On Enablement (Weeks 3-5)

### 2.1 Workshop Development
**Status**: � In Progress  
**Priority**: P0

- [~] **Workshop 1: AI Landing Zone Fundamentals** 👤 *Anahita* (Lead) + *Arturo* (Review) → **Foundation Complete**
  - Duration: 2-3 hours
  - Audience: Partner architects and engineers
  - Topics:
    - Landing Zone concepts and Azure integration
    - Network security and private connectivity
    - Identity and access management
    - Cost estimation and governance
  
- [ ] **Workshop 2: Deploying Your First Gen AI Workload** 👤 *Arturo* (Lead) + *Anahita* (Review)
  - Duration: 3-4 hours (hands-on)
  - Audience: Technical partners with Azure experience
  - Topics:
    - Deploy foundational Landing Zone infrastructure
    - Configure AI Foundry Service and connections
    - Deploy sample chat application with RAG
    - Implement monitoring and observability

- [ ] **Workshop 3: Landing Zones to Production (Gen AI OPS Bridge)** 👤 *Arturo* (Lead) + *Ana Lopez Moreno* (Gen AI OPS Input)
  - Duration: 4 hours
  - Audience: Advanced partners planning production deployments
  - Topics:
    - CI/CD pipelines for AI applications
    - Lifecycle management and versioning
    - Monitoring, logging, and alerting
    - Cost optimization and scaling strategies

**Deliverables**:
- `/workshops/01-landing-zone-fundamentals/` with slides and guides *(Anahita)*
- `/workshops/02-first-genai-workload/` with step-by-step lab *(Arturo)*
- `/workshops/03-production-readiness/` with advanced topics *(Arturo + Ana)*

---

### 2.2 Lab Infrastructure & Scripts
**Status**: 📋 Planned  
**Priority**: P1

- [ ] **Automated Lab Deployment** 👤 *Arturo*
  - Bicep/Terraform templates for workshop environments
  - Setup scripts for instructor-led sessions
  - Teardown and cleanup automation
  
- [ ] **Testing & Validation Scripts** 👤 *Anahita*
  - Connectivity testing
  - Service health checks
  - Sample application deployment validation

**Deliverables**:
- `/templates/workshop-environments/` with IaC templates *(Arturo)*
- `/templates/testing-scripts/` with validation tools *(Anahita)*

---

## 📦 Phase 3: Templates & Accelerators (Weeks 5-7)

### 3.1 IaC Templates (Landing Zone Focus)
**Status**: 📋 Planned  
**Priority**: P0

- [ ] **Bicep Template Library** 👤 *Arturo*
  - Modular resource deployments
  - Parameters file examples for common scenarios
  - Naming convention guidance
  
- [ ] **Terraform Module Library** 👤 *Anahita*
  - Reusable modules for core components
  - Variable configuration examples
  - State management guidance

- [ ] **Portal Deployment Templates** 👤 *Anahita*
  - ARM templates for portal-based deployment
  - Quick-start configurations

**Deliverables**:
- `/templates/bicep/` with modular Bicep files *(Arturo)*
- `/templates/terraform/` with reusable modules *(Anahita)*
- `/templates/arm/` with portal templates *(Anahita)*

---

### 3.2 Operational Templates (Gen AI OPS Overlap)
**Status**: 📋 Planned  
**Priority**: P1

- [ ] **Monitoring & Observability** 👤 *Arturo* + *Ana Lopez Moreno*
  - Azure Monitor workbook templates
  - Log Analytics queries for AI workloads
  - Application Insights configuration
  
- [ ] **CI/CD Pipeline Templates** 👤 *Anahita*
  - Azure DevOps YAML pipelines
  - GitHub Actions workflows
  - Deployment checklists
  
- [ ] **Cost Management** 👤 *Anahita*
  - Cost allocation tags
  - Budget alerts and policies
  - FinOps best practices for AI workloads

**Deliverables**:
- `/templates/monitoring/` with dashboards and queries *(Arturo + Ana)*
- `/templates/pipelines/` with CI/CD examples *(Anahita)*
- `/templates/governance/` with policies and cost controls *(Anahita)*

---

## 📦 Phase 4: Partner Enablement Assets (Weeks 7-9)

### 4.1 Presentation Materials
**Status**: 📋 Planned  
**Priority**: P0

- [ ] **Partner Pitch Deck** 👤 *Anahita*
  - Why AI Landing Zones matter
  - Business value and ROI
  - Success stories and case studies
  
- [ ] **Technical Deep-Dive Deck** 👤 *Arturo*
  - Architecture walkthrough
  - Component-by-component explanation
  - Integration patterns
  
- [ ] **Executive Briefing** 👤 *Anahita* + *Arturo*
  - Strategic alignment with Azure AI
  - Competitive differentiation
  - Roadmap and future capabilities

**Deliverables**:
- `/presentations/partner-pitch-deck.pptx` *(Anahita)*
- `/presentations/technical-deep-dive.pptx` *(Arturo)*
- `/presentations/executive-briefing.pptx` *(Both)*

---

### 4.2 Partner Tools & Resources
**Status**: 📋 Planned  
**Priority**: P1

- [ ] **Assessment & Discovery Tools** 👤 *Anahita*
  - Customer readiness assessment questionnaire
  - Landing Zone design decision tree
  - Sizing and SKU selection guide
  
- [ ] **Implementation Checklists** 👤 *Arturo*
  - Pre-deployment checklist
  - Security validation checklist
  - Go-live readiness checklist
  
- [ ] **Troubleshooting Guide** 👤 *Arturo*
  - Common issues and solutions
  - Support escalation paths
  - FAQ for partners

**Deliverables**:
- `/templates/assessment-tools/` with questionnaires *(Anahita)*
- `/docs/implementation-checklist.md` *(Arturo)*
- `/docs/troubleshooting-guide.md` *(Arturo)*

---

## 📦 Phase 5: Testing & Refinement (Weeks 9-11)

### 5.1 Real-World Validation
**Status**: 📋 Planned  
**Priority**: P0

- [ ] **Pilot Workshop Delivery** 👤 *Anahita* + *Arturo* (Co-deliver)
  - Run workshops with 2-3 partner organizations
  - Gather feedback on content and labs
  - Measure effectiveness and learning outcomes
  
- [ ] **Reference Implementation Testing** 👤 *Arturo*
  - Deploy all template variations
  - Test in different Azure regions
  - Validate against security and compliance benchmarks
  
- [ ] **Documentation Review** 👤 *Anahita*
  - Technical accuracy review with product group
  - Partner feedback incorporation
  - Accessibility and clarity improvements

**Deliverables**:
- Updated content based on pilot feedback *(Both)*
- Test reports and validation results *(Arturo)*
- Final documentation review sign-off *(Anahita)*

---

### 5.2 Gen AI OPS Integration Points
**Status**: 📋 Planned  
**Priority**: P1

- [ ] **Operational Runbooks** 👤 *Arturo* + *Ana Lopez Moreno*
  - Day-2 operations guide
  - Incident response procedures
  - Performance tuning guidelines
  
- [ ] **Lifecycle Management** 👤 *Anahita* + *Ana Lopez Moreno*
  - Model versioning and updates
  - Application update procedures
  - Infrastructure evolution patterns
  
- [ ] **Cross-Program Alignment** 👤 *Arturo* + *Anahita* (Both)
  - Coordinate with Ana's Gen AI OPS accelerator
  - Ensure seamless handoff from Landing Zone to OPS
  - Identify shared assets and avoid duplication

**Deliverables**:
- `/docs/operations/` folder with runbooks *(Arturo + Ana)*
- Coordination plan with Gen AI OPS team *(Both)*
- Shared template repository structure *(Both)*

---

## 📊 Success Metrics

### Delivery Metrics
- [ ] 3 workshop modules completed and tested
- [ ] 5+ reusable IaC templates validated
- [ ] 10+ partner organizations enabled
- [ ] 90%+ participant satisfaction in workshops

### Impact Metrics
- [ ] Partners can deploy Landing Zone in <2 hours
- [ ] 80% reduction in common deployment errors
- [ ] Documented in 3+ customer success stories
- [ ] Contributing to AI CoE V2 standardization

---

## 🤝 Collaboration Points

### Internal Coordination
- **Jason Virtue (PSA)**: Overall AI CoE program lead, Landing Zones initiative
- **Ana Lopez Moreno (PSA)**: Gen AI OPS accelerator, hands-on labs
- **Anahita Afshari (PSA)**: Landing Zones collaboration, workshop development and delivery
- **Devanshi Thakar (PSA)**: Responsible AI integration
- **Lucy**: Discovery Cards and partner program alignment

### Cross-Program Touchpoints
- **Landing Zone → Gen AI OPS**: Operational handoff and Day-2 concerns
- **Discovery Cards → Landing Zones**: Customer discovery to technical implementation
- **Responsible AI → Landing Zones**: Security and compliance integration

---

## 📅 Key Milestones

| Milestone | Target Date | Status |
|-----------|-------------|--------|
| Repository structure complete | Jan 29, 2026 | ✅ Done |
| Partner Quick Reference Guide | Jan 30, 2026 | ✅ Done |
| IaC Decision Framework | Jan 30, 2026 | ✅ Done |
| Workshop 1 foundation (outline) | Jan 30, 2026 | ✅ Done |
| Phase 1 cheat sheets | Feb 7, 2026 | 🔄 Optional (official docs sufficient) |
| Workshop 1 complete (slides + exercises) | Feb 14, 2026 | 🚧 In Progress |
| Workshop 2 draft complete | Feb 21, 2026 | 📋 Planned |
| Pilot workshop delivery | Feb 28, 2026 | 📋 Planned |
| Final review and refinement | Mar 7, 2026 | 📋 Planned |
| V2 contribution ready | Mar 14, 2026 | 📋 Planned |

---

## 📝 Notes & Considerations

### From Community Sync (Jan 26, 2026)
- CoE V2 emphasizes **broader team involvement** and contribution
- Need to **standardize on best architectural flavor** across Bicep/Terraform/Portal
- Strong emphasis on **hands-on, practical enablement** (learning from Peru delivery)
- Integration with **AI transformation offer** sales motion
- Focus on **production readiness** and scaling workloads

### Key Decisions Needed
1. Which IaC approach to prioritize first? (Recommend: Bicep for Azure-native, then Terraform)
2. Lab environment strategy: Shared subscription vs individual environments?
3. How to handle regional differences in Azure service availability?
4. Level of integration with existing Enterprise Landing Zones?

### Risks & Mitigations
- **Risk**: Content duplication with official Azure repo
  - **Mitigation**: ✅ Adopted "reference, don't recreate" approach. Our guides navigate to official content.
- **Risk**: Templates become outdated as services evolve
  - **Mitigation**: Version control, quarterly review cycles, link to official repos
- **Risk**: Workshop complexity too high for target audience
  - **Mitigation**: Multiple difficulty levels, optional deep-dives

---

## 📚 Official Resources We Reference (Don't Recreate)

### 🎓 MS Learn Training (Recommended for All Partners)

| Module | Duration | Topics |
|--------|----------|--------|
| [**AI Center of Excellence Learning Path**](https://learn.microsoft.com/training/paths/ai-center-excellence/) | 1 hr 34 min | Complete path covering all modules below |
| [Introduction to AI Center of Excellence](https://learn.microsoft.com/training/modules/intro-ai-center-excellence/) | 29 min | AI adoption, governance, roles & responsibilities |
| [Introduction to AI Landing Zones](https://learn.microsoft.com/training/modules/intro-ai-landing-zones/) | 28 min | Landing zone concepts, platform vs workload teams |
| [Guide AI workload operations](https://learn.microsoft.com/training/modules/guide-ai-operations-center-excellence/) | 37 min | GenAIOps, security, compliance, cost, monitoring |

### GitHub Repositories & Documentation

| Resource | What It Covers | We Add |
|----------|---------------|--------|
| [AI-Landing-Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md) | 40+ recommendations across Networking, Identity, Security, Compute, Data, Monitoring, Governance, Cost, Reliability | Partner navigation + scenario mapping |
| [AI-Landing-Zones Architecture Diagrams](https://github.com/Azure/AI-Landing-Zones) | With/without Platform LZ variants, Bicep & Terraform implementations | When to use which pattern |
| [Deploy-Your-AI-App Required Roles](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/roles-scopes.md) | IAM requirements for deployment | Partner-specific permission scenarios |
| [Deploy-Your-AI-App Security Guidelines](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/SECURITY.md) | Security best practices | Hands-on workshop exercises |
| [azd Parameter Guide](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production/blob/main/docs/ParameterGuide.md) | All deployment parameters | Common partner configurations |

---

**Last Updated**: January 30, 2026  
**Next Review**: February 5, 2026
