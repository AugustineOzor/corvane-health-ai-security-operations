# Playbook PB-01: PHI Entered into Corvane Assist

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 2 of 6
<!-- /nav -->

| | |
| --- | --- |
| **Triggers** | DET-01, DET-02; staff self-report |
| **Default severity** | SEV-3 (single warning) · SEV-2 (PHI submitted, or a file with PHI) · SEV-1 (bulk PHI or repeated deliberate use) |
| **Lead** | SOC analyst, with the Privacy Officer |

## Steps

| Phase | Action | Owner |
| --- | --- | --- |
| **Respond** | Confirm what was submitted from the gateway log (masked view); identify the user, time and volume | SOC analyst |
| | If DLP blocked it before submission: close as SEV-3, send coaching message | SOC analyst |
| | If submitted: suspend the session; ask the vendor to delete the conversation under the BAA and confirm in writing | Head of Digital Workplace |
| | Contact the user: understand why, and whether other tools were used | SOC analyst; line manager |
| **Assess** | Privacy Officer runs a HIPAA breach risk assessment (nature of PHI, who received it, whether it was actually viewed or retained, mitigation) | Privacy Officer |
| **Recover** | Remove the user's access temporarily if the use was deliberate; restore after retraining | Identity and Access Management |
| | Add the pattern that slipped through to the DLP rules | CISO |
| **Improve** | Record lessons; check whether the user needed a feature that only CareLens offers, and whether that need is common | Head of Digital Workplace |

## Evidence to keep

Gateway log entry, DLP verdict, vendor deletion confirmation, risk assessment, user communication.

## Decision point

If the user was a clinician trying to do patient-specific work, raise it with the CMIO: the real fix may be giving them CareLens access.

<!-- nav -->
---

[← Previous: AI Incident Severity and Triage Guide](01-ai-incident-severity-and-triage.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Playbook PB-02: Prompt Injection or Poisoned Content in CareLens →](03-pb02-prompt-injection-carelens.md)
<!-- /nav -->
