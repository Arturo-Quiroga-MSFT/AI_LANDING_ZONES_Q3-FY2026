# Templates & Accelerators

Reusable infrastructure-as-code templates, scripts, and tools for deploying and managing AI Landing Zones.

## 📁 Directory Structure

```
templates/
├── bicep/                    # Azure Bicep templates
├── terraform/                # Terraform modules
├── arm/                      # ARM templates for portal deployment
├── workshop-environments/    # Lab setup scripts
├── monitoring/               # Observability templates
├── pipelines/                # CI/CD templates
├── governance/               # Policies and compliance
├── testing-scripts/          # Validation and testing
└── assessment-tools/         # Discovery and planning tools
```

---

## 🏗️ Bicep Templates

**Location**: `/templates/bicep/`

Modular Azure Bicep templates for deploying AI Landing Zone components.

### Core Modules
- `main.bicep` - Full Landing Zone deployment
- `networking.bicep` - VNet, subnets, private endpoints
- `ai-foundry.bicep` - Azure AI Foundry Service
- `container-apps.bicep` - Container Apps environment
- `data-services.bicep` - Cosmos DB, Storage, AI Search
- `security.bicep` - Key Vault, managed identities, RBAC

### Usage
```bash
az deployment sub create \
  --location eastus \
  --template-file bicep/main.bicep \
  --parameters bicep/parameters.json
```

**Status**: 📋 Planned

---

## 🌍 Terraform Modules

**Location**: `/templates/terraform/`

Reusable Terraform modules for multi-cloud or hybrid scenarios.

### Module Structure
- `modules/networking/` - Network infrastructure
- `modules/ai-foundry/` - AI Foundry resources
- `modules/compute/` - Container Apps and VMs
- `modules/data/` - Data and storage services
- `modules/security/` - Security and identity

### Usage
```hcl
module "ai_landing_zone" {
  source = "./modules/landing-zone"
  
  resource_group_name = "rg-ai-landing-zone"
  location           = "eastus"
  environment        = "production"
}
```

**Status**: 📋 Planned

---

## 🔧 Workshop Environments

**Location**: `/templates/workshop-environments/`

Automated setup scripts for instructor-led workshops.

### Components
- `setup-lab.sh` - Provision workshop infrastructure
- `cleanup-lab.sh` - Remove workshop resources
- `validate-environment.sh` - Pre-workshop health check
- `student-credentials.sh` - Generate access for participants

### Workshop Modes
1. **Single Tenant**: All participants share one environment
2. **Multi Tenant**: Each participant gets isolated resources
3. **Hybrid**: Shared infrastructure with isolated data planes

**Status**: 📋 Planned

---

## 📊 Monitoring Templates

**Location**: `/templates/monitoring/`

Azure Monitor workbooks, Log Analytics queries, and dashboards.

### Available Templates
- AI Foundry performance workbook
- Container Apps observability dashboard
- Cost tracking and optimization
- Security and compliance monitoring

### KQL Queries
- Model inference latency
- Token consumption tracking
- Error rate analysis
- Resource utilization

**Status**: 📋 Planned

---

## 🔄 CI/CD Pipelines

**Location**: `/templates/pipelines/`

Continuous integration and deployment templates.

### Azure DevOps
- `azure-pipelines-bicep.yml` - Bicep deployment pipeline
- `azure-pipelines-terraform.yml` - Terraform deployment pipeline
- `azure-pipelines-app.yml` - Application deployment

### GitHub Actions
- `.github/workflows/deploy-infrastructure.yml`
- `.github/workflows/deploy-app.yml`
- `.github/workflows/run-tests.yml`

**Status**: 📋 Planned

---

## 🛡️ Governance Templates

**Location**: `/templates/governance/`

Azure Policy definitions, naming conventions, and compliance configurations.

### Policy Sets
- Naming convention enforcement
- Required tags for cost allocation
- Security baseline policies
- Compliance (HIPAA, SOC2, etc.)

### Cost Management
- Budget alerts by component
- Reservation recommendations
- FinOps dashboards

**Status**: 📋 Planned

---

## ✅ Testing & Validation Scripts

**Location**: `/templates/testing-scripts/`

Automated testing and validation tools.

### Test Categories
- **Connectivity Tests**: Private endpoint reachability
- **Service Health**: Component availability checks
- **Security Tests**: Validate network isolation
- **Performance Tests**: Baseline latency and throughput

### Usage
```bash
./testing-scripts/validate-deployment.sh --resource-group rg-ai-lz
```

**Status**: 📋 Planned

---

## 📋 Assessment Tools

**Location**: `/templates/assessment-tools/`

Discovery and planning tools for customer engagements.

### Tools Included
- Customer readiness questionnaire
- Landing Zone design decision tree
- SKU sizing calculator
- TCO estimation spreadsheet
- Implementation timeline planner

**Status**: 📋 Planned

---

## 🎯 Using These Templates

### For Partners
1. **Assessment**: Use assessment tools to understand customer needs
2. **Planning**: Select appropriate templates based on requirements
3. **Deployment**: Follow workshop guides or use IaC templates directly
4. **Validation**: Run testing scripts to verify deployment
5. **Operations**: Implement monitoring and CI/CD pipelines

### For Instructors
1. **Lab Setup**: Use workshop-environment scripts
2. **Student Access**: Generate credentials for participants
3. **Monitoring**: Track lab usage and costs
4. **Cleanup**: Automated teardown after session

---

## 🤝 Contributing Templates

To contribute a new template:
1. Create the template in the appropriate subdirectory
2. Include a README.md with usage instructions
3. Add parameter examples and expected outputs
4. Test in a clean environment
5. Submit for review

**Template Standards**:
- Follow Azure naming conventions
- Include parameter validation
- Document prerequisites
- Provide examples
- Include cleanup/deletion instructions

---

## 🔗 Related Resources

- [AI Landing Zones Design Checklist](https://github.com/Azure/AI-Landing-Zones/blob/main/docs/AI-Landing-Zones-Design-Checklist.md)
- [Azure Bicep Documentation](https://learn.microsoft.com/azure/azure-resource-manager/bicep/)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

---

**Program**: AI Center of Excellence V2  
**Maintained by**: Arturo Quiroga  
**Last Updated**: January 29, 2026
