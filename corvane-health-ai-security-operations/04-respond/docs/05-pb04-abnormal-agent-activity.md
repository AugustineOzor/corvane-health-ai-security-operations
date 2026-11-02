# Playbook PB-04: Abnormal Agent Activity or Unauthorised Data Access

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 5 of 6
<!-- /nav -->

| | |
| --- | --- |
| **Triggers** | DET-08 (denied tool call), DET-09 (limits reached), DET-10 (cross-patient access), DET-16 (unexpected outbound connection) |
| **Default severity** | SEV-3 (single denied call) · SEV-2 (repeated denials or loops) · SEV-1 (DET-10 or DET-16 confirmed) |
| **Lead** | SOC lead |

## Steps

| Phase | Action | Owner |
| --- | --- | --- |
| **Respond** | For DET-10 or DET-16: **disable CareLens** service-wide; revoke its service credentials and FHIR client secret | On-call engineer; SOC lead |
| | For DET-08 or DET-09: disable the specific tool if denials repeat; review the triggering requests | Clinical AI Engineering |
| | Preserve traces, FHIR audit logs and network logs | SOC lead |
| **Assess** | Was it a bug (scoping error), manipulation (injection leading to tool misuse), or a compromised component? | SOC lead; Clinical AI Engineering |
| | Which patients' records were accessed, and was any data returned to the clinician or sent out? | SOC lead; Privacy Officer |
| | HIPAA breach risk assessment for any data accessed without a valid reason | Privacy Officer |
| **Recover** | Fix the cause; rotate secrets; add a regression test to the deployment pipeline | Clinical AI Engineering |
| | Re-enable in stages: one unit, then one hospital, then all, with the SOC watching | Clinical AI Engineering; SOC |
| **Improve** | Review the tool permission matrix and limits | Director of Clinical AI Engineering |

## Evidence to keep

Agent traces, FHIR audit logs, network logs, credential rotation records, risk assessment.

<!-- nav -->
---

[← Previous: Playbook PB-03: Unsafe or Incorrect Clinical Suggestion](04-pb03-unsafe-clinical-suggestion.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Playbook PB-05: Model Update or Behaviour Change →](06-pb05-model-behaviour-change.md)
<!-- /nav -->
