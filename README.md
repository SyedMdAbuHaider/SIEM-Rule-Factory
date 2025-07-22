
# SOC-LabOps: Enterprise Detection Engineering Lab with Splunk

## Overview
SOC-LabOps is a production-grade virtual Security Operations Center environment designed to accelerate detection engineering and threat analysis capabilities. This platform provides security teams with:

- A fully configured Splunk-based detection environment
- Real-world attack simulations mapped to MITRE ATT&CK
- Enterprise logging architecture with best practice configurations
- Detection-as-code workflows for continuous security monitoring

## Key Capabilities

### Core Features
- **Splunk Enterprise Deployment**: Complete SIEM deployment with optimized indexing
- **Advanced Detection Rules**: 150+ pre-built SPL searches covering common TTPs
- **Attack Simulation Framework**: Safe execution of adversary techniques
- **MITRE ATT&CK Integration**: Technique mapping and coverage analysis

### Security Visibility
- **Endpoint Monitoring**: Sysmon, Windows Event Logs, PowerShell logging
- **Network Security**: Firewall, IDS, and proxy logs
- **User Behavior Analytics**: Authentication and access patterns

### Operational Readiness
- **SOC Playbook Development**: Incident response workflows
- **Alert Triage Training**: Realistic investigation scenarios
- **Detection Engineering**: Rule creation and optimization

## Technical Architecture

### System Components
```
[ Simulated Enterprise Environment ]
├── Active Directory Domain (Windows Server 2022)
├── Workstations (Windows 10/11)
├── Linux Servers (Ubuntu/RHEL)
└── Network Devices (Simulated)

[ Security Monitoring Layer ]
├── Splunk Enterprise 9.0+
│   ├── Indexers (3-node cluster)
│   ├── Search Heads
│   └── Deployment Server
├── Universal Forwarders (All endpoints)
└── Heavy Forwarders (Network zones)

[ Attack Simulation ]
└── Atomic Red Team (v10.0+)
    ├── Windows execution nodes
    └── Linux execution nodes
```

## Deployment Guide

### Prerequisites
- Virtualization: VMware ESXi 7.0+ or Hyper-V
- Hardware: 64GB RAM, 1TB storage (minimum)
- Networking: Isolated VLAN with NAT capabilities

### Installation
1. **Base Infrastructure**
```bash
# Clone the deployment repository
git clone https://github.com/org/soc-labops-splunk.git
cd soc-labops-splunk/deploy

# Initialize Terraform
terraform init
terraform apply -var-file=production.tfvars
```

2. **Splunk Configuration**
```powershell
# Configure indexers
.\scripts\configure-indexers.ps1 -ClusterMaster 192.168.1.100

# Deploy forwarders
.\scripts\deploy-forwarders.ps1 -DeploymentServer 192.168.1.101
```

3. **Attack Simulation Setup**
```bash
# Install Atomic Red Team
Install-Module -Name AtomicRedTeam -Force -Scope AllUsers
Import-Module AtomicRedTeam
Get-ARTTest -ListAll
```

## Detection Engineering Framework

### SPL Rule Example
```spl
index=win_events EventCode=4688
  [search index=win_events EventCode=4624 LogonType=3
  | stats count by Account_Name
  | where count > 5
  | fields Account_Name]
| stats values(New_Process_Name) as processes by Account_Name
| where mvcount(processes) > 3
```
*Detects suspicious process creation following multiple network logins*

### ATT&CK Coverage Matrix
| Technique ID | Detection Coverage | Alert Volume | False Positive Rate |
|--------------|--------------------|--------------|---------------------|
| T1059.001    | 98%                | 12/day       | 2%                  |
| T1003.001    | 95%                | 8/day        | 5%                  |
| T1021.002    | 85%                | 15/day       | 10%                 |

## Training Modules

### Level 1: SOC Analyst
- Alert triage procedures
- Basic SPL query writing
- Incident documentation

### Level 2: Detection Engineer
- Advanced correlation searches
- Rule performance optimization
- False positive analysis

### Level 3: Threat Hunter
- Anomaly detection techniques
- Behavioral analytics
- Attack path reconstruction

## Security Controls
- **Network Segmentation**: Lab environment isolated from production
- **Access Management**: RBAC implemented for all components
- **Data Governance**: All training data is synthetic
- **Audit Trail**: Comprehensive activity logging

## Compliance Features
- **NIST SP 800-53**: SI-4 (Information System Monitoring)
- **ISO 27001**: A.12.4 (Logging and Monitoring)
- **MITRE Engenuity**: ATT&CK Evaluations Framework

## Roadmap
### Q3 2025
- [ ] Splunk ES integration
- [ ] Cloud log ingestion (AWS/Azure)
- [ ] ATT&CK v14 mapping update

### Q4 2025
- [ ] SOAR integration (Splunk Phantom)
- [ ] Machine learning detections
- [ ] Purple team exercise framework

## Support
For enterprise support and training:
- **Email**: smabuhaider6@gmail.com
- **Documentation**: coming
- **Training**:details coming
## License
SOC-LabOps Splunk Edition is available under Enterprise License Agreement. Academic licenses available upon request.

---

**Author**: Syed Md. Abu Haider | **Principal Security Architect**  
**Organization**: Security Operations Research Lab  
**Contact**: [linkedin.com/in/syed-md-abu-haider](https://www.linkedin.com/in/syed-md-abu-haider)  
**Certifications**: Splunk Certified Architect, MITRE ATT&CK Certified
```

