# Playbook PB-05: Model Update or Behaviour Change

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 6 of 6
<!-- /nav -->

| | |
| --- | --- |
| **Triggers** | DET-14 (unapproved model version), DET-13 (acceptance rate out of band); vendor notice; rise in DET-11 blocks |
| **Default severity** | SEV-2 · SEV-1 if unsafe outputs reached clinicians |
| **Lead** | Director of Clinical AI Engineering |

## Steps

| Phase | Action | Owner |
| --- | --- | --- |
| **Respond** | Confirm the model version in production against the registry | Clinical AI Engineering |
| | If unapproved: **roll back** to the pinned version (Recovery Runbook, R-01); if rollback is not possible, disable medication suggestions and keep summaries only | Clinical AI Engineering |
| | Ask the provider what changed and when | Head of Vendor Management |
| **Assess** | Run the 2,000-case clinical test set and the red-team suite against the new behaviour | Clinical AI Engineering |
| | Review suggestions shown since the change for errors | CMIO office |
| **Recover** | Approve the new version only if it passes all tests; otherwise stay on the pinned version | AI Governance Council |
| **Improve** | Tighten contract terms on change notice; check that pinning cannot be overridden by the provider | Procurement; Clinical AI Engineering |

## Evidence to keep

Registry entries, test results before and after, vendor correspondence, review of affected suggestions.

<!-- nav -->
---

[← Previous: Playbook PB-04: Abnormal Agent Activity or Unauthorised Data Access](05-pb04-abnormal-agent-activity.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Part 05: Recover →](../../05-recover/README.md)
<!-- /nav -->
