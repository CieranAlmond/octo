# 🚀 Security Strategy at a Fast-Growing Startup

## 📘 Scenario

You have just joined a very fast-growing startup as the **only security person**. The company has roughly **100 employees**, and the **CTO** has been making decisions based on functional need — **security has not always been considered**.

You’ve been hired by the CTO for your **security knowledge and unique perspective**.

The company has:
- Built a **custom CRM solution** sold to clients
- Hosted it on **AWS**
- Uses **CI/CD tooling** to make a handful of production changes per day
- Relies on **SaaS** tools for all other services (email, office, etc.)
- Encourages **staff to purchase their own IT** (laptops, accessories) and expense it

---

## 🔍 How Would You Identify and Prioritise Potential Security Problems?

### 🧠 Initial Thoughts / Assumptions

- Small org, **immature functions**, and you're the **first security hire** — solutions must be pragmatic and resource-conscious.
- **AWS architecture** likely lacks security best practices; needs a review.
- **CI/CD** pipelines may lack deployment control, peer review, and security scans.
- **Third-party SaaS** usage should be audited: what data is being shared and how?
- **Laptops & BYOD**: asset management, encryption, VPNs, antivirus, MDM (Azure Intune), etc.
- No apparent **phishing training** in place.

---

## 🧭 Approach

Taking into account:
- Org size, resource limitations
- CRM with **customer PII** — reputation risk during growth phase
- Focus first on **reducing immediate risk** vs. building long-term governance
- Start assuming **limited/no documentation**

### ✍️ Scoping Operation

Scoping covers:
- Review of **AWS**
- Review of **CI/CD & deployment**
- Review of **company assets & third-party SaaS**

---

## 🔩 Review Areas

### 1. AWS Architecture

- Architecture diagrams for CRM?
- How are CRM endpoints exposed?
- How is authentication handled?

#### AWS Account(s)

- IAM roles and permissions: **Who has access and why?**
- **MFA**: Required for AWS? Using SSO via Okta/Ping?
- Network segregation: VPCs, security groups
- **Encryption**: Are S3/RDS encrypted?
- **Logging/Monitoring**: CloudTrail, CloudWatch, GuardDuty?
- Availability: Redundancy? Backups?
- **Secrets management**: How are production secrets handled?

---

### 2. CI/CD Pipelines

- Who can deploy to production?
- Are there **peer reviews** before merging?
- Any **SAST/DAST scanning**?
- Are there separate environments (dev/test/prod)? Are they **mirrored**?

---

### 3. Company Assets / Third Parties

- **BYOD**: Any device controls?
- Is there an **asset inventory**?
- Are laptops:
  - Encrypted?
  - Updated regularly?
  - Running Antivirus / DLP?
- Is an **MDM** solution deployed?
- JML process: Are assets/data retrieved on offboarding?
- SaaS vendor list:
  - What data is shared?
  - How is it shared?
  - Data type/volume?

---

## 🎤 Info Gathering

Conduct interviews with SMEs:
> “Can you walk me through how you do X?”
> “How is Y handled today?”

Lean on:
- Documentation
- Policies / procedures

---

## 📊 Prioritisation: Risk x Likelihood Matrix

### 🔴 High Priority

- Implement **phishing training**
- Encrypt databases with **PII**
- Protect assets with:
  - MDM
  - JML
  - Remote wipes
  - AV/DLP
- Scan repos for **plaintext secrets**
- Enforce **MFA** for all systems

### 🟠 Medium Priority

- Enable logging + alerts for **IOC**
- Company-issued laptops with:
  - Default security image (VPN, AV, DLP)
- Peer review for deployments
- Monthly/quarterly **IAM reviews**
- Build and maintain **asset inventory**

### 🟡 Low Priority

- **Vendor risk** assessments
- Define policies/procedures (JML, governance)
- Diagram AWS architecture
- Build medium/long-term **security roadmap**
- Create **Infosec policy**, guidance (e.g. password best practices)
- Begin **security standard** scoping (e.g. CE, ISO 27001)

---

## 📈 The Company Has Grown

Now:
- 5,000+ employees
- CRM, AWS, CI/CD scaled well (100+ daily deployments)
- Expanded via **global acquisitions**
- Bigger clients now expect **SOC 2 / ISO 27001**
- CTO wants to stay **tech-first**, avoid manual GRC

---

## 🧠 Updated Perspective

Shift from **firefighting** → **governance and structure**

### 🔁 Revisiting Prioritisation

> The old **low priority** items now become high priority

#### ✅ High Priority Now Includes:

- Centralised **policies, procedures, guidelines**
- Documented **controls & control owners**
- **Formal risk register**
- **Subsidiary integration**: Align to parent governance/control set
- Global compliance: GDPR, APRA (AU), DORA (EU)

---

## 🎯 Challenges for ISO 27001 Certification

### 🗂️ Documentation

- Lack of central documentation
- Existing processes operate in silos
- Need to perform **gap analysis**
- Must drive **team buy-in** to fix process weaknesses

### ⚙️ Technical Gaps

- Varying stacks, inconsistent processes
- Need for standard SDLC, patch mgmt
- **Automated playbooks** (e.g. CIS via Ansible) can help

### 🧑‍💻 Resource Constraints

- People wearing multiple hats
- Convince teams to **prioritise security controls**

### ⚖️ Risk Awareness

- ISO requires **risk-based thinking**
- Risk mindset likely missing in fast-growth mode
- Introduce **proactive risk management**

### 👥 Cultural Shift

#### Management Buy-In

- Why implement ISO?
  - Reduce breach risk
  - Improve reputation
  - Unlock enterprise sales
- Use real-world examples as rationale

#### Employee Buy-In

- Frame benefits in their language:
  - DevOps: "Standardised playbooks = time saved"
  - GRC: "Less firefighting"

---

## 🤖 Automating GRC

### Goal: **Minimise Manual Processes**

### 🧠 Pitching GRC Engineering

Option A (Traditional):
> Manual evidence collection, screenshots, GRC tools chasing teams

Option B (GRC Engineering):
> Use low/no-code or API tools to auto-collect evidence

- Upskills GRC
- Reduces burden on tech teams
- Enables **continuous monitoring**

### 🔧 Implementation Path

#### For Main Org (SaaS-oriented)

- Use Vanta/Drata for SOC 2/ISO 27001
- Map Trust Services Criteria → Controls → Evidence (via API)

#### For Subsidiaries (non-SaaS or on-prem)

- Perform **gap analysis**
- Migrate to main org’s tech stack/tools
- Integrate over time to align GRC + control sets

#### Consider Flexible Options

- Tools like **JupiterOne**, **Backstage**
- **Policy-as-code**
- **Open source** solutions for control enforcement

### 🧩 Key Concepts

- Automate evidence collection via:
  - API queries
  - Real-time system data
- Minimise stakeholder fatigue
- Build once, monitor continuously

---

## 🏁 Final Notes

This is **not an exhaustive list** — it’s a structured view of initial and scaled security approaches based on the real-world context of a fast-growing tech company.

- Short-term: reduce risk quickly
- Long-term: build scalable governance and automation

