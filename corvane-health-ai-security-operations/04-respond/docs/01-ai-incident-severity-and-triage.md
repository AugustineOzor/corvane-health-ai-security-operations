# AI Incident Severity and Triage Guide

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 1 of 6
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-RS-001 |
| **Version** | 1.0 |
| **Owner** | SOC Manager, with the CMIO for clinical incidents |
| **NIST CSF 2.0** | RS.MA-01 to RS.MA-05; RS.AN-03; RS.CO-02, RS.CO-03 |

## 1. Purpose

AI incidents can be security incidents, privacy incidents, patient safety events, or all three at once. This guide makes sure the right people are involved from the first hour.

## 2. Severity

| Severity | Definition | Examples | Response start | Who is paged |
| --- | --- | --- | --- | --- |
| **SEV-1** | Confirmed or likely patient harm, PHI exposure at scale, or compromise of an AI system | Cross-patient data exposure; unsafe suggestion acted on; tampered guideline index | 15 minutes, 24/7 | SOC lead, CISO, CMIO, Privacy Officer, system owner |
| **SEV-2** | Control failure with potential for harm, or limited PHI exposure | Injection that reached the model; PHI uploaded to Assist; unapproved model version live | 1 hour | SOC lead, system owner, Privacy Officer; CMIO if clinical |
| **SEV-3** | Blocked attempt or minor policy breach | Blocked injection; single DLP warning; jailbreak attempts | Next business day | SOC analyst; system owner informed |
| **SEV-4** | Informational | Tuning findings; isolated feedback | Weekly review | SOC analyst |

**Rule of thumb:** if a patient could have been affected, start at SEV-2 or higher and involve the CMIO.

## 3. First 30 minutes

1. **Confirm** the alert is real, using the agent trace or gateway log.
2. **Classify** the severity and open an incident record.
3. **Decide on containment** using the playbook's first step. For CareLens, the on-call engineer can disable a single tool, a single hospital or the whole service.
4. **Preserve evidence:** snapshot traces, logs and the model and configuration version.
5. **Notify** the people in the severity table.

## 4. Three questions for every AI incident

| Question | Why it matters |
| --- | --- |
| **Was PHI exposed, and to whom?** | Triggers HIPAA breach risk assessment by the Privacy Officer |
| **Could a patient have been harmed?** | Triggers a patient safety event and clinical review |
| **Is the AI system still behaving this way?** | Decides whether to contain the feature, tool or whole service |

## 5. Playbooks

| Playbook | Scenario |
| --- | --- |
| [PB-01](02-pb01-phi-in-corvane-assist.md) | PHI entered into Corvane Assist |
| [PB-02](03-pb02-prompt-injection-carelens.md) | Prompt injection or poisoned content in CareLens |
| [PB-03](04-pb03-unsafe-clinical-suggestion.md) | Unsafe or incorrect clinical suggestion |
| [PB-04](05-pb04-abnormal-agent-activity.md) | Abnormal agent activity or unauthorised data access |
| [PB-05](06-pb05-model-behaviour-change.md) | Model update or behaviour change |

## 6. Notification obligations (summary)

| Regime | When | Timing (summary) | Owner |
| --- | --- | --- | --- |
| HIPAA Breach Notification Rule | Unsecured PHI breach, after risk assessment | Individuals without unreasonable delay and no later than 60 days after discovery; HHS and, for over 500 residents of a state, the media | Privacy Officer |
| State breach and health privacy laws | As defined by each state | Varies; some states are shorter than HIPAA | Privacy Officer; Legal |
| GDPR (EU research data) | Personal data breach involving EU trial participants | Supervisory authority within 72 hours where required | Research Compliance; Privacy Officer |
| Vendor contracts and BAAs | Incident involving a vendor | As set in each agreement | Procurement; Privacy Officer |

These are summaries. Legal confirms obligations for each incident.

<!-- nav -->
---

[← Previous: Part 04: Respond overview](../README.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Playbook PB-01: PHI Entered into Corvane Assist →](02-pb01-phi-in-corvane-assist.md)
<!-- /nav -->
