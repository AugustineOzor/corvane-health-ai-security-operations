# AI Detection Use Case Catalogue

<!-- nav -->
[Repository home](../../README.md) › [Part 03: Detect](../README.md) › Document 1 of 1
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-DE-001 |
| **Systems** | Corvane Assist; CareLens |
| **Version** | 1.0 |
| **Owner** | SOC Manager |
| **Spreadsheet** | `../files/CH-AISEC-DE-001_AI_Detection_Use_Cases.xlsx` |
| **NIST CSF 2.0** | DE.CM-01, DE.CM-03, DE.CM-09; DE.AE-02 to DE.AE-08 |

## 1. Purpose

Preventive controls fail sometimes. This catalogue defines what the SOC watches for in Corvane's AI systems, where the signal comes from, how severe it is and which playbook to run. Each use case maps to a threat in the threat models.

## 2. Log sources

| Source | What it records |
| --- | --- |
| AI gateway | Every prompt and response (PHI masked), user, timestamp, DLP verdict |
| DLP and web proxy | Blocked uploads, PHI pattern hits, visits to unapproved AI sites |
| Agent traces | Every CareLens step: retrieved content IDs, injection-filter verdicts, tool calls and results, validator verdicts, model version |
| FHIR and EHR audit logs | Which patient records were accessed, by whom and through which application |
| Clinician feedback | Accept, edit, reject and "report a problem" actions on CareLens drafts |
| Model registry | Model, prompt and configuration versions in production |

## 3. Use cases

| ID | Detection | System | Source | Severity | Threat | Playbook |
| --- | --- | --- | --- | --- | --- | --- |
| DET-01 | PHI pattern in a prompt or upload (blocked or warned) | Assist | DLP; AI gateway | Medium (High if bulk) | TA-01 | PB-01 |
| DET-02 | Upload of a file containing more than 20 PHI records | Assist | DLP | **High** | TA-01 | PB-01 |
| DET-03 | Repeated visits to blocked AI sites by the same user | Both | Web proxy | Low | TA-02 | Coaching |
| DET-04 | Repeated jailbreak patterns from one user (5 in 24 hours) | Assist | AI gateway | Low | TA-04 | Coaching |
| DET-05 | Unusual Assist volume: over 3× the user's normal, or out of hours | Assist | AI gateway | Medium | TA-06 | Account review |
| DET-06 | Policy answers reported wrong by users | Assist | User feedback | Low | TA-03 | Content fix |
| DET-07 | **Injection filter fires on retrieved record content** | CareLens | Agent traces | **High** | TC-01 | PB-02 |
| DET-08 | **Tool call denied by the permission layer** | CareLens | Agent traces | **High** | TC-03, TC-10 | PB-04 |
| DET-09 | Step or rate limit reached (possible loop) | CareLens | Agent traces | Medium | TC-03 | PB-04 |
| DET-10 | FHIR access to a patient other than the one open in the session | CareLens | FHIR audit | **Critical** | TC-02 | PB-04 |
| DET-11 | Output validator blocks an unsafe suggestion (dose, allergy, interaction) | CareLens | Agent traces | Medium (High if 3 or more in a day) | TC-04 | PB-03 |
| DET-12 | Clinician reports a harmful or incorrect suggestion | CareLens | Clinician feedback | **High** | TC-04, TC-11 | PB-03 |
| DET-13 | Acceptance rate of suggestions outside the expected band (below 40% or above 90% weekly) | CareLens | Clinician feedback | Medium | TC-05, TC-08 | PB-05 |
| DET-14 | Model version in production differs from the approved registry entry | CareLens | Model registry; traces | **High** | TC-08 | PB-05 |
| DET-15 | Guideline index hash does not match the signed snapshot | CareLens | Integrity check | **Critical** | TC-06 | PB-02 |
| DET-16 | Unexpected outbound connection from CareLens components | CareLens | Network logs | **Critical** | TC-02, TC-09 | PB-04 |

## 4. Example detection logic

Detection rules are written for the SIEM. Two simplified examples, in KQL-style pseudocode:

**DET-10: cross-patient access through CareLens**

```kql
FhirAudit
| where ClientApp == "CareLens"
| join kind=inner (AgentTraces | project RequestId, SessionPatientHash) on RequestId
| where hash_sha256(PatientId) != SessionPatientHash
| project TimeGenerated, RequestId, UserId, ResourceType
```

**DET-13: clinician acceptance rate out of band**

```kql
ClinicianFeedback
| where TimeGenerated > ago(7d) and Action in ("accept","edit","reject")
| summarize AcceptRate = countif(Action == "accept") * 1.0 / count() by Hospital
| where AcceptRate < 0.40 or AcceptRate > 0.90
```

## 5. Tuning and testing

- Every use case is tested against a seeded event before it goes live, and every quarter after.
- False-positive rates are reviewed monthly; any use case above 30% false positives is tuned.
- New threats or incidents add new use cases (see Part 06).

<!-- nav -->
---

[← Previous: Part 03: Detect overview](../README.md) &nbsp;|&nbsp; [Part 03: Detect](../README.md) &nbsp;|&nbsp; [Next: Part 04: Respond →](../../04-respond/README.md)
<!-- /nav -->
