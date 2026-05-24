# GRC Automation & SOC 2 Type 2 Evidence Framework

> **Role context:** Built and operated as GRC lead at a fintech. Reporting to CFO. No prior GRC infrastructure existed. Everything below was designed, implemented, and operationalized from scratch.

---

## Overview

This repository documents the GRC (Governance, Risk & Compliance) program I designed and led, encompassing:

- A **19-document policy library** anchored to SOC 2 CC controls, NIST CSF, and OWASP Top 10
- A **~40-control SOC 2 Type 2 evidence framework** covering operational proof requirements across the full audit period
- Incident response architecture, vendor risk workflows, and change management enforcement
- A **Python-based permissions automation design** for ERP role and access lifecycle management (architecture and design documented; implementation in progress)

The program was built to satisfy a SOC 2 Type 2 audit while simultaneously closing material operating effectiveness gaps discovered during a live security incident.

---

## Background & Problem Statement

Upon joining, the GRC function consisted of a legacy policy wiki with stale, unenforced documents. No operational evidence collection existed. Engineering and Product had no awareness that change management policies applied to their workflows — a critical operating effectiveness gap for SOC 2 Type 2, which requires proof of *consistent operation over time*, not just the existence of controls.

A production security incident surfaced this gap directly: an affected release had bypassed change management review entirely. The post-incident audit finding became the forcing function for a full GRC reboot.

---

## Policy Library (19 Documents)

All policies are versioned in a document management system (source of truth) and cross-referenced to SOC 2 CC controls and NIST CSF functions.

| # | Policy | Primary Controls |
|---|--------|-----------------|
| 1 | Information Security Policy | CC1.1, CC5.3 |
| 2 | Acceptable Use Policy | CC1.4, CC6.1 |
| 3 | Access Control Policy | CC6.1–CC6.5 |
| 4 | Change Management Policy | CC8.1 |
| 5 | Incident Response Policy | CC7.3–CC7.5 |
| 6 | Vulnerability Management Policy | CC7.1 |
| 7 | Data Classification & Handling Policy | C1.1, CC6.7 |
| 8 | Encryption Policy | CC6.7 |
| 9 | Business Continuity & DR Policy | A1.2–A1.3 |
| 10 | Vendor / Third-Party Risk Policy | CC9.2 |
| 11 | Secure Software Development Policy | CC8.1, CC6.6 |
| 12 | Risk Assessment Policy | CC3.1–CC3.4 |
| 13 | Logging & Monitoring Policy | CC4.1, CC7.2 |
| 14 | Physical Security Policy | CC6.4 |
| 15 | Privacy Policy (external) | CC2.2, C1.1 |
| 16 | Data Retention & Disposal Policy | C1.2 |
| 17 | Human Resources Security Policy | CC1.4, CC6.3 |
| 18 | Network Security Policy | CC6.6, CC6.7 |
| 19 | Security Awareness & Training Policy | CC1.4 |

---

## SOC 2 Type 2 Evidence Framework

SOC 2 Type 2 differs fundamentally from Type 1: it requires proof that controls operated *consistently and effectively over the audit period* (typically 6–12 months). Point-in-time screenshots are insufficient. Evidence must demonstrate cadence, ownership, and exception handling.

The framework below covers ~40 controls across the five Trust Service Criteria. Each control entry specifies: evidence type, collection frequency, system of record, responsible owner, and audit artifact format.

### Common Criteria (CC)

#### CC1 — Control Environment

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC1.1 — COSO principles documented | Policy acknowledgment log | Annual + onboarding | GRC | Signed acknowledgment CSV |
| CC1.2 — Board/mgmt oversight | Board meeting minutes (security agenda items) | Quarterly | CLO/CFO | Redacted minutes PDF |
| CC1.3 — Organizational structure | Org chart + RACI matrix | On change | GRC | Versioned diagram |
| CC1.4 — Commitment to competence | Security training completion records | Annual | GRC/HR | LMS export |
| CC1.5 — Accountability enforced | Performance review documentation | Annual | HR | Attestation |

#### CC2 — Communication & Information

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC2.1 — Internal communication of policies | Policy distribution log | Annual + onboarding | GRC | Email/Drive distribution record |
| CC2.2 — External communication (customers/vendors) | Privacy policy version history, vendor notification log | On change | CLO/CCO | Git changelog + email log |
| CC2.3 — Reporting obligations | Incident notification records | Per incident | GRC/CLO | Incident ticket + notification evidence |

#### CC3 — Risk Assessment

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC3.1 — Risk assessment process | Risk register with scoring methodology | Semi-annual | GRC | Risk register XLSX |
| CC3.2 — Fraud risk | Fraud risk assessment | Annual | GRC/CFO | Assessment doc |
| CC3.3 — Change risk | Change management tickets with risk ratings | Per change | Engineering/GRC | Jira/Linear export |
| CC3.4 — Emerging risk | Threat intelligence review log | Quarterly | GRC | Review log |

#### CC4 — Monitoring Controls

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC4.1 — Ongoing monitoring | SIEM alert review log; anomaly reports | Monthly | GRC/SecOps | Alert triage log |
| CC4.2 — Management evaluations | GRC program review meetings | Quarterly | GRC/CFO | Meeting notes + action items |

#### CC5 — Control Activities

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC5.1 — Control selection | Control mapping document (SOC 2 ↔ NIST CSF) | Annual review | GRC | Mapping matrix |
| CC5.2 — Technology controls | System configuration baselines | Quarterly | Engineering/GRC | Config export |
| CC5.3 — Policies deployed | Policy version log; enforcement evidence | On change | GRC | Drive version history |

#### CC6 — Logical & Physical Access

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC6.1 — Access control infrastructure | SSO/IdP config screenshots; MFA enforcement proof | Quarterly | IT/GRC | IdP admin export |
| CC6.2 — Access provisioning | Access request tickets; provisioning log | Per event | IT/GRC | Ticket export + ERP audit CSV |
| CC6.3 — Access removal | Offboarding checklist completions; deprovisioning log | Per event | IT/HR/GRC | Signed checklist + automation log |
| CC6.4 — Physical access | Facility access log (if applicable) | Monthly | Ops | Badge log or N/A attestation |
| CC6.5 — Logical access review | Quarterly access review sign-offs | Quarterly | GRC + system owners | Signed review + remediation evidence |
| CC6.6 — Threat detection | IDS/WAF alert logs; penetration test results | Annual pentest; monthly log review | GRC/Engineering | Pentest report + log export |
| CC6.7 — Data transmission controls | TLS configuration evidence; encryption-at-rest proof | Annual | Engineering | Config + cert export |
| CC6.8 — Malware controls | EDR deployment coverage report | Quarterly | IT | EDR console export |

#### CC7 — System Operations

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC7.1 — Vulnerability management | Scan results + remediation tracking | Monthly scans; quarterly review | GRC/Engineering | Scanner export + tickets |
| CC7.2 — Anomaly detection | SIEM/log alert review; escalation records | Monthly | GRC/SecOps | Alert log |
| CC7.3 — Incident response | Incident tickets with timeline and RCA | Per incident | GRC | IRP-formatted incident report |
| CC7.4 — Incident resolution | Post-incident review docs; control updates | Per incident | GRC | After-action report |
| CC7.5 — Disclosure obligations | Breach notification records (if applicable) | Per incident | CLO/GRC | Notification log |

#### CC8 — Change Management

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC8.1 — Change authorization | Change tickets with approval workflow | Per change | Engineering/GRC | Ticket export showing approvals |
| CC8.1 — Testing prior to production | QA/staging sign-off records | Per change | Engineering | PR review + deploy log |
| CC8.1 — Emergency change process | Emergency change log with post-hoc approval | Per event | Engineering/GRC | Emergency change tickets |

#### CC9 — Risk Mitigation

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| CC9.1 — Risk mitigation activities | Risk register treatment tracking | Quarterly | GRC | Risk register delta |
| CC9.2 — Vendor/third-party risk | Vendor risk assessments; SOC 2 report collection | Annual + onboarding | GRC | Vendor assessment tracker |

### Availability (A)

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| A1.1 — Availability commitments | SLA documentation; uptime monitoring | Monthly | Engineering/GRC | Uptime report |
| A1.2 — Environmental threats | BCP/DR plan; backup test results | Annual | Engineering/GRC | DR test report |
| A1.3 — Recovery testing | Tabletop or live DR exercise | Annual | Engineering/GRC | Exercise report + RTO/RPO validation |

### Confidentiality (C)

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| C1.1 — Confidential data identification | Data classification policy + inventory | Annual | GRC/CLO | Data map |
| C1.2 — Confidential data disposal | Media disposal/data deletion records | Per event | IT/GRC | Disposal log |

### Processing Integrity (PI)

| Control | Evidence Type | Frequency | Owner | Artifact |
|---------|--------------|-----------|-------|----------|
| PI1.1 — Complete and accurate processing | Input/output validation testing evidence | Per release | Engineering | Test report |
| PI1.2 — Processing commitments | SLA/contractual commitments documentation | Annual | CLO/GRC | Contract excerpts |

---

## Incident Response: Case Study

**Production Security Incident — Access Control Vulnerability**

A production release introduced an authorization vulnerability that allowed authenticated users to access data under specific conditions. Root cause involved a broken access control pattern — a class of vulnerability well-documented in the OWASP API Security Top 10.

**GRC response actions:**
- Activated IRP within hours of detection
- Assembled cross-functional incident team (Engineering, Product, Legal, GRC)
- Scoped impact via log analysis; identified affected records
- Initiated customer notification workflow per CC7.5
- Conducted full after-action review; identified change management bypass as a contributing factor
- Launched structured 8-week Secure Software Development Transformation program in response

**SOC 2 operating effectiveness implication:** The incident revealed that Engineering and Product had no awareness that change management policies applied to their release workflows. This is an operating effectiveness gap — the policy existed, but consistent operation could not be demonstrated. The remediation program and evidence collection framework above were designed directly to close this gap for the Type 2 audit period.

---

## Monitoring & Logging Architecture

Evidence-quality logging requires more than "logs exist." For SOC 2 Type 2, auditors look for:

1. **Log completeness** — all relevant systems emit structured logs
2. **Tamper evidence** — logs are shipped to an immutable sink before local rotation
3. **Alert coverage** — anomalies generate tickets, tickets have owners and resolution SLAs
4. **Review cadence** — log review is documented and dated, not just automated

### Stack

| Layer | Tooling | Evidence Output |
|-------|---------|----------------|
| Application logs | Structured JSON → log aggregator | Searchable audit trail |
| Infrastructure | Cloud-native logging (AWS CloudTrail / GCP Audit Logs) | API call history |
| Identity/Access | IdP System Log | Authentication + provisioning events |
| Endpoint | EDR console | Threat detection + coverage |
| SIEM/Alerting | Log aggregation platform | Alert triage log for CC4.1, CC7.2 |
| Secrets | Vault audit log | Secrets access trail |

### Monthly Review Artifact (template)

```
Log Review — [Month YYYY]
Reviewer: [Name, Title]
Date: [ISO date]
Systems reviewed: [list]
Alerts triaged: [N]
Escalations: [N] — ticket refs: [links]
Anomalies requiring follow-up: [describe or "none"]
Signature: ________________
```

This signed log review document is the evidence artifact for CC4.1 and CC7.2.

---

## Vendor Risk: Adversarial Assessment Case Study

The framework was stress-tested against a high-stakes vendor assessment involving a critical financial services partner. Over multiple consecutive disclosure requests, the vendor returned incomplete or evasive responses regarding their own SOC 2 posture, subprocessor chain, and incident history.

GRC actions taken:
- Maintained structured disclosure gap log across all interactions
- Escalated to Legal with formal notice framework
- Documented vendor risk rating escalation in risk register
- Proposed contractual remediation requirements and audit rights clause

This case study illustrates how a mature vendor risk program operates under adversarial conditions — not just checkbox collection.

---

## ERP Permissions Automation: Architecture Design

> **Note:** This section documents the design architecture for a Python-based permissions automation system. The design was completed and the implementation was initiated; full production deployment was in progress at the time of this writing.

### Problem

The ERP/GL system had accumulated permission drift over time: former employees retained access roles, role assignments were undocumented, and there was no automated lifecycle process tied to HR onboarding/offboarding. For SOC 2 Type 2, this creates evidence risk — auditors require proof of periodic access reviews *and* timely revocation.

### Designed Solution: Two-Phase Python Automation

**Phase 1 — Discovery & Audit**

```python
# Connects to ERP API and exports full role/user matrix
# Produces a structured CSV for access review sign-off
# Flags: inactive users, orphaned roles, privilege outliers

python erp_audit.py \
  --export-roles \
  --flag-inactive-days 30 \
  --output access_review_$(date +%Y%m).csv
```

- Authenticates via ERP XML API (session-based, credential-vaulted)
- Pulls all user records, assigned roles, last-login timestamps, and department mappings
- Cross-references against HR system roster (CSV or API feed)
- Outputs a structured access review artifact ready for manager sign-off and auditor submission

**Phase 2 — Remediation & Lifecycle Enforcement**

```python
# Applies approved changes from signed access review
# Deprovisions flagged users, reassigns roles per least-privilege model
# Generates a timestamped change log for SOC 2 evidence

python erp_remediate.py \
  --input approved_review_$(date +%Y%m).csv \
  --dry-run          # validate before applying
  --apply            # execute with audit log output
  --evidence-output ./evidence/CC6.2/
```

- Idempotent: safe to re-run; only applies delta changes
- All actions written to a tamper-evident JSONL change log
- Evidence output folder maps directly to SOC 2 control CC6.2 (Logical Access)
- Dry-run mode allows engineering review before any production changes

### Control Mapping

| Phase | SOC 2 CC | NIST CSF |
|-------|----------|----------|
| Discovery/Audit | CC6.2, CC6.3 | PR.AC-1, PR.AC-4 |
| Remediation | CC6.2, CC6.6 | PR.AC-1, RS.RP-1 |
| Evidence output | CC4.1, CC7.2 | DE.CM-3 |

---

## Skills Demonstrated

| Domain | Specifics |
|--------|-----------|
| GRC Program Design | Built from zero: policy library, risk framework, control mapping, evidence program |
| SOC 2 Type 2 | Operational evidence design, auditor-ready artifact production, external auditor engagement |
| Python Automation | ERP API integration design, access lifecycle automation, audit-trail generation |
| Incident Response | Live IR leadership, access control root cause analysis, after-action → program change |
| Vendor Risk | Multi-cycle assessments, legal escalation, custodial risk management |
| Cross-functional Leadership | Engineering, Product, Legal, Finance, HR alignment across all workstreams |
| Regulatory Frameworks | SOC 2 CC/A/C/PI, NIST CSF, OWASP Top 10, fintech data privacy obligations |

---

## Contact

**James Pierson**
GRC & Security Executive | Open to opportunities
[LinkedIn: linkedin.com/in/jpierson] · [jpierson@seanet.com]

> *This repository is a sanitized portfolio representation. Proprietary data, customer information, and production credentials have been removed. Control frameworks and automation patterns are original work.*
