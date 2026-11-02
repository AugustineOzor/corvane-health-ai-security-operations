# AI Recovery and Rollback Runbook

<!-- nav -->
[Repository home](../../README.md) › [Part 05: Recover](../README.md) › Document 1 of 1
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-RC-001 |
| **Systems** | Corvane Assist; CareLens |
| **Version** | 1.0 |
| **Owner** | Director of Clinical AI Engineering (CareLens); Head of Digital Workplace (Assist) |
| **NIST CSF 2.0** | RC.RP-01 to RC.RP-06; RC.CO-03, RC.CO-04 |

## 1. Purpose

After an incident is contained, AI systems must come back in a known-good state, with proof that the problem is fixed. This runbook sets the recovery actions, who can approve them, and the checks before service resumes.

## 2. Containment switches (CareLens)

| Switch | Effect | Time to apply | Who can trigger |
| --- | --- | --- | --- |
| Disable one tool | That capability stops; others keep working | Under 5 minutes | On-call engineer |
| Disable one suggestion type (for example medication changes) | Summaries continue; that suggestion type is removed | Under 5 minutes | On-call engineer; CMIO |
| Disable one hospital or unit | CareLens unavailable there | Under 10 minutes | On-call engineer |
| **Disable CareLens** | Sidebar shows "temporarily unavailable"; clinicians use normal workflow | Under 10 minutes | On-call engineer; SOC lead; CMIO; CISO |

Clinical care never depends on CareLens: the normal EHR workflow is always available.

## 3. Recovery actions

| ID | Action | When used | Steps | Verification |
| --- | --- | --- | --- | --- |
| R-01 | **Roll back model or prompt version** | Unapproved model change; behaviour regression | Re-point to the last approved version in the registry; redeploy | Clinical test set passes; version matches registry |
| R-02 | **Restore guideline index** | Tampering or bad content | Load last good signed snapshot; verify hashes | Hash check passes; sample queries return expected sources |
| R-03 | **Disable a connector** (FHIR, drug-interaction service) | Scoping error; vendor issue | Revoke client credentials; remove from tool layer | Denied-call test passes |
| R-04 | **Revert workflow** | Workflow change caused unsafe use | Restore previous EHR sidebar configuration | Workflow demonstration with CMIO office |
| R-05 | **Rotate secrets** | Suspected compromise | Rotate API keys, FHIR client secret, signing keys | Old credentials fail; new ones work |
| R-06 | **Quarantine content** | Injection from a record document | Exclude document from retrieval; keep in EHR | Retrieval test excludes it |
| R-07 | **Revoke user access** | Misuse of Assist or CareLens | Remove role; end sessions | Access test fails as expected |

## 4. Patient safety review (CareLens)

Before CareLens returns after any SEV-1 or SEV-2 clinical incident:

1. **Look back:** review all suggestions of the affected type since the problem began.
2. **Contact:** treating teams for any patient who may have been affected.
3. **Record:** patient safety events for each affected case.
4. **Sign-off:** the CMIO confirms the clinical risk is addressed.

## 5. Return to service

| Severity | Approval to restore | Conditions |
| --- | --- | --- |
| SEV-1 | AI Governance Council co-chairs (CMIO and CISO) | Root cause fixed; full clinical test set and red-team suite passed; patient safety review complete; staged rollout |
| SEV-2 | System owner and CISO; CMIO for clinical incidents | Root cause fixed; relevant tests passed |
| SEV-3 | System owner | Fix deployed through normal change process |

**Staged rollout:** one unit for 48 hours, then one hospital for one week, then all sites, with the SOC watching the related detections at each stage.

## 6. Communication

Clinicians and staff are told when a feature is disabled and when it returns, with a short explanation. Where patients were affected, disclosure follows the patient disclosure policy.

<!-- nav -->
---

[← Previous: Part 05: Recover overview](../README.md) &nbsp;|&nbsp; [Part 05: Recover](../README.md) &nbsp;|&nbsp; [Next: Part 06: Improve →](../../06-improve/README.md)
<!-- /nav -->
