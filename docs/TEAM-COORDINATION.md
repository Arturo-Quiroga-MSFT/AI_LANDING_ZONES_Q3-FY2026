# Team Coordination & Communication Plan

Coordination guide for AI Landing Zones initiative within AI Center of Excellence V2.

## 👥 Core Team

### Leadership
- **Jason Virtue** (PSA) - AI CoE Program Lead, Landing Zones Initiative Lead
- **Andressa Siqueira** (PSA) - Community Sync Facilitator

### Contributors
- **Arturo Quiroga** (PSA) - Landing Zones Architecture & Workshop Development
- **Ana Lopez Moreno** (PSA) - Gen AI OPS Accelerator, Hands-On Labs
- **Anahita Afshari** (PSA) - Landing Zones Collaboration, Workshop Development & Delivery
- **Devanshi Thakar** (PSA) - Responsible AI Integration
- **Lucy Rak** (PSA) - AI Discovery Cards, Featured Partner Program

---

## 🎯 Work Stream Ownership

### AI Landing Zones (Primary Focus)
**Lead**: Jason Virtue  
**Contributors**: Arturo Quiroga (Architecture & Deliverables), Anahita Afshari (Workshop Development)

**Scope**:
- Reference architecture documentation
- IaC template development (Bicep/Terraform/Portal)
- Workshop content creation
- Partner enablement materials
- Testing and validation

**Deliverables Owner**: Arturo Quiroga, Anahita Afshari

---

### Gen AI OPS Accelerator (Overlapping Focus)
**Lead**: Ana Lopez Moreno  
**Contributors**: Arturo Quiroga (infrastructure handoff)

**Scope**:
- Operational lifecycle management
- Hands-on labs for operations
- Accelerator repository with templates
- Best practices for production management

**Coordination Points**:
- Landing Zone → OPS handoff documentation
- Shared monitoring and observability templates
- CI/CD pipeline alignment

---

### Responsible AI
**Lead**: Devanshi Thakar  
**Support**: Christian Thilmany

**Scope**:
- Responsible AI Maturity Model Workshop
- Governance and compliance guidance
- Impact assessments
- Sensitive use case navigation

**Integration with Landing Zones**:
- Security and compliance requirements in architecture
- Governance templates and policies
- Responsible AI checkpoints in workshops

---

### AI Discovery Cards
**Lead**: Lucy  
**Support**: Regional leads

**Scope**:
- Customer and partner discovery workshops
- Use case identification and prioritization
- Featured Partner Program

**Connection to Landing Zones**:
- Discovery → Landing Zone implementation flow
- Partner success story pipeline
- Business value documentation

---

## 📅 Coordination Cadence

### Weekly Community Sync
**When**: Weekly (schedule TBD)  
**Format**: Virtual call  
**Led by**: Jason Virtue & Andressa  
**Purpose**: Program updates, cross-workstream coordination

**Standing Agenda**:
1. Program updates and announcements
2. Work stream progress reports
3. Cross-team dependencies and blockers
4. Partner engagement highlights
5. Open Q&A

---

### Landing Zones Working Sessions
**When**: Bi-weekly (or as needed)  
**Participants**: Jason, Arturo, Anahita Afshari  
**Purpose**: Deep-dive on Landing Zones deliverables

**Topics**:
- Architecture decision reviews
- Workshop content iteration
- Template testing and validation
- Partner feedback incorporation

---

### Landing Zones ↔ Gen AI OPS Sync
**When**: Bi-weekly  
**Participants**: Arturo, Ana Lopez Moreno, Jason  
**Purpose**: Ensure seamless handoff and avoid duplication

**Topics**:
- Infrastructure to operations boundary
- Shared asset coordination
- Workshop content alignment
- Accelerator repository structure

---

## 🔄 Communication Channels

### Primary Channels
- **Teams Channel**: [AI Center of Excellence] (link TBD)
- **Email Distribution**: ai-coe-v2@microsoft.com (confirm)
- **SharePoint**: [AI CoE SharePoint Site] (link TBD)

### Communication Guidelines
- **Quick Questions**: Teams chat
- **Decisions & Updates**: Teams channel posts
- **Documentation**: SharePoint + GitHub
- **Feedback & Issues**: GitHub issues (this repo)

---

## 🤝 How to Collaborate

### For Contributing to Landing Zones

1. **Reach Out**: Contact Jason Virtue or Arturo Quiroga
2. **Sync on Scope**: Align on what you want to contribute
3. **Create Content**: Use this repo structure
4. **Review**: Submit for team review before finalizing
5. **Test**: Validate with pilot partners if applicable
6. **Share**: Present in Community Sync

### For Requesting Support

1. **Check Existing Assets**: Review `/docs` and `/templates`
2. **Ask in Teams**: Post question in AI CoE channel
3. **Schedule Time**: Book working session if needed
4. **Document Outcome**: Update repo with learnings

---

## 📊 Progress Tracking

### Primary Tracking
- **This Repository**: `/docs/DELIVERABLES-ROADMAP.md`
- **Updates**: Weekly in Community Sync

### Partner Engagement Tracking
- **Discovery Cards Delivered**: Lucy maintains
- **Landing Zone Deployments**: Arturo tracks
- **Featured Partner Nominations**: Submit to Lucy

### Success Metrics
- Workshop delivery count
- Partner organizations enabled
- Templates reused/deployed
- Contribution to AI CoE V2 standardization

---

## 🚀 Getting Involved

### I want to...

**...build a workshop**
→ Contact Jason or Arturo to align on focus area

**...create IaC templates**
→ Review existing templates, coordinate with Arturo

**...deliver to partners**
→ Use existing materials, share feedback post-delivery

**...contribute to Gen AI OPS**
→ Connect with Ana Lopez Moreno

**...integrate Responsible AI**
→ Reach out to Devanshi Thakar

**...run Discovery Cards**
→ Contact Lucy for enablement

---

## 📝 Decision Log

Key decisions made by the team:

| Date | Decision | Owner | Status |
|------|----------|-------|--------|
| Jan 29, 2026 | Repository structure established | Arturo | ✅ Complete |
| TBD | Prioritize Bicep over Terraform initially | Jason | 📋 Pending |
| TBD | Workshop pilot partners identified | Team | 📋 Pending |

---

## 🎓 Knowledge Sharing

### Internal Learning Sessions (Planned)
- Deep-dive: Azure AI Foundry Service
- Deep-dive: Container Apps for AI workloads
- Deep-dive: Private networking for AI services
- Best practices: Bicep for AI infrastructure

**Volunteer to Lead?** Post in Teams channel

---

## 🔗 Key Links

**Official Resources**:
- [Azure AI Landing Zones GitHub](https://github.com/Azure/AI-Landing-Zones)
- [Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Deploy AI App in Production](https://github.com/microsoft/Deploy-Your-AI-Application-In-Production)

**Internal Resources**:
- [Community Sync Recording](link TBD)
- [AI CoE SharePoint](link TBD)
- [Partner Success Stories](link TBD)

---

## ❓ FAQ

**Q: How do I avoid duplicating work?**  
A: Check this repo first, post in Teams before creating new content

**Q: Who reviews my contributions?**  
A: Jason or Arturo for Landing Zones, Ana for Gen AI OPS

**Q: Can I adapt content for my region?**  
A: Yes! Share regional adaptations back with the team

**Q: How do I get access to lab environments?**  
A: See Community Sync notes on CDX provisioning with Ben

**Q: What if I find an error in templates?**  
A: Create a GitHub issue or post in Teams

---

**Last Updated**: January 29, 2026  
**Maintained by**: Arturo Quiroga  
**Questions?** Post in AI CoE Teams channel or contact team leads
