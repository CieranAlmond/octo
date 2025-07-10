# Security at a Fast-Growing Startup

You have just joined a very fast-growing startup as the only security person. The company has roughly 100 employees, and the CTO has been making decisions based on functional need — security has not always been considered.

You’ve been hired by the CTO for your security knowledge and unique perspective.

The company has:
- Built a custom CRM solution sold to clients
- Hosted it on AWS
- Uses CI/CD tooling to make a handful of production changes per day
- Relies on SaaS tools for all other services (email, office, etc.)
- Encourages staff to purchase their own IT (laptops, accessories) and expense it

---

## How would you identify and prioritise potential security problems?

Initial thoughts/assumptions:
- Small org, immature functions, you're first security hire – so be pragmatic and resource-conscious
- AWS likely misconfigured – check for public buckets, overly permissive roles
- CI/CD probably lacks deployment control, peer review, security scans
- SaaS likely sprawling; what data is going where?
- Laptops/BYOD: asset management, encryption, VPNs, antivirus, MDM (Azure Intune), etc
- No phishing training

Approach:
- Org is small; go for pragmatic, high impact moves, be security enabler, not blocker
- CRM has customer PII – reputational risk if breached while growing
- Focus on reducing immediate risk, not building perfect governance
- Assume little or no documentation

Scoping operation:
- Review of AWS
- Review of CI/CD & deployment
- Review of company assets & third-party SaaS

---

## Review Areas

### AWS Architecture
- Architecture diagrams for CRM?
- How are CRM endpoints exposed?
- How is authentication handled?

AWS account(s):
- IAM roles + permissions — who has access and why?
- Is MFA required for AWS? Using SSO via Okta/Ping?
- Network segregation? VPCs, security groups?
- Are S3/RDS encrypted?
- Logging/monitoring — CloudTrail, CloudWatch, GuardDuty?
- Availability — is there redundancy? backups?
- Secrets management — how are production secrets handled?

---

### CI/CD Pipelines
- Who can deploy to prod?
- Are there peer reviews before merging?
- Any SAST/DAST scanning?
- Separate environments (dev/test/prod)? Are they mirrored?

---

### Company assets / third parties
- BYOD — any device controls?
- Is there an asset inventory?
- Are laptops:
  - Encrypted?
  - Up to date?
  - Running antivirus / DLP?
- Is MDM deployed?
- JML process — are assets/data retrieved on offboarding?
- SaaS vendor list:
  - What data is shared?
  - How is it shared?
  - Data type/volume?

---

## Info Gathering

Talk to SMEs:
- “Can you walk me through how you do X?”
- “How is Y handled today?”

Use:
- Documentation
- Policies / procedures

---

## Prioritisation: Risk x Likelihood matrix

### High priority
- Implement phishing training
- Encrypt databases with PII
- Protect assets (MDM, JML, remote wipes, AV/DLP)
- Scan repos for plaintext secrets
- Enforce MFA for all systems

### Medium priority
- Enable logging + alerts for IOC
- Company-issued laptops with default security image (VPN, AV, DLP)
- Peer review for deployments
- Monthly/quarterly IAM reviews
- Asset inventory

### Low priority
- Vendor risk assessments
- Define policies/procedures (JML, governance)
- Diagram AWS architecture
- Build medium/long-term security roadmap
- Infosec policy, guidance (e.g. password best practices)
- Begin security standard scoping (e.g. CE, ISO 27001)

---

## The company has grown

- 5,000+ employees
- CRM, AWS, CI/CD scaled well (100+ daily deployments)
- Expanded via global acquisitions
- Bigger clients now expect SOC 2 / ISO 27001
- CTO wants to stay tech-first, avoid manual GRC

---

## Updated Perspective

Now it's about adding structure + governance, not firefighting

### Revisit Prioritisation
- Many “low priority” items become high priority

New high priority:
- Policies, procedures, guidelines (centralised)
- Controls & control owners
- Risk register
- Subsidiary integration to parent governance/control set
- Global compliance: GDPR, APRA (AU), DORA (EU)

---

## ISO 27001

### Challenges:

#### Documentation
- Lack of central documentation
- Existing processes operate in silos
- Need to perform gap analysis
- Must drive team buy-in to fix process weaknesses

#### Technical Gaps
- Varying stacks, inconsistent processes
- Need for standard SDLC, patch mgmt
- Automated playbooks (e.g. CIS via Ansible) can help

#### Resource Constraints
- People wearing multiple hats
- Convince teams to prioritise security controls

#### Risk Awareness
- ISO requires risk-based thinking
- Risk mindset likely missing in fast-growth mode
- Need to introduce proactive risk mgmt

#### Cultural Shift

Management Buy-In:
- Why implement ISO?
  - Reduce breach risk
  - Improve reputation
  - Unlock enterprise sales
- Use real-world examples as rationale

Employee Buy-In:
- Frame benefits in their language:
  - DevOps: "standardised playbooks = time saved"
  - GRC: "less firefighting"

---

## Automating GRC

### Goal: Minimise manual processes

### Pitching GRC Engineering

Option A (traditional):
- Manual evidence collection, screenshots, GRC tools chasing teams

Option B (GRC engineering):
- Use low/no-code or API tools to auto-collect evidence
- Upskills GRC
- Reduces burden on tech teams
- Enables continuous monitoring

---

## Implementation

For main org (SaaS-oriented):
- Use Vanta/Drata for SOC 2/ISO 27001
- Map Trust Services Criteria → Controls → Evidence (via API)

For subsidiaries (non-SaaS or on-prem):
- Gap analysis
- Migrate to main org’s tech stack/tools
- Integrate over time to align GRC + control sets

### Consider flexible options:
- JupiterOne, Backstage
- Policy-as-code
- Open source for control enforcement

---

## Key Concepts

- Automate evidence collection (API, real-time system data)
- Minimise stakeholder fatigue
- Build once, monitor continuously
