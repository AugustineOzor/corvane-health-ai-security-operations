# Playbook PB-03: Unsafe or Incorrect Clinical Suggestion

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 4 of 6
<!-- /nav -->

| | |
| --- | --- |
| **Triggers** | DET-11 (validator blocks), DET-12 (clinician report); pharmacy or patient safety report |
| **Default severity** | SEV-3 (blocked by validator) · SEV-2 (shown to a clinician but not acted on) · SEV-1 (acted on, or patient affected) |
| **Lead** | CMIO, supported by the SOC and Clinical AI Engineering |

This is primarily a **patient safety event**. Security supports; clinical leadership leads.

## Steps

| Phase | Action | Owner |
| --- | --- | --- |
| **Respond** | Identify the patient, clinician, suggestion and whether it was accepted, edited or rejected | CMIO office |
| | If acted on: contact the treating team immediately to review and correct care | Treating clinician; CMIO |
| | File a patient safety event in the safety reporting system | CMIO office |
| | If the same error could recur: disable the specific suggestion type (for example medication dosing) across all sites until fixed | Clinical AI Engineering |
| **Assess** | Root cause: retrieval (wrong or missing data), reasoning (model error), guideline content, validator gap, or workflow (reviewed too quickly) | CMIO; Clinical AI Engineering |
| | Check for a pattern: search traces for similar suggestions in the last 30 days | SOC |
| | Check for bias: did the error affect one patient group more than others? | Health Equity Lead |
| **Recover** | Fix the cause; add the case to the 2,000-case clinical test set; re-run the full set before re-enabling | Clinical AI Engineering |
| **Improve** | Patient safety review with clinical leadership; share learning with all CareLens users | Patient Safety Officer; CMIO |

## Disclosure

Where a patient was affected, follow Corvane's patient disclosure policy. The clinical team leads the conversation with the patient.

## Evidence to keep

Agent trace, draft as shown, clinician actions, safety event record, root-cause analysis, test results after the fix.

<!-- nav -->
---

[← Previous: Playbook PB-02: Prompt Injection or Poisoned Content in CareLens](03-pb02-prompt-injection-carelens.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Playbook PB-04: Abnormal Agent Activity or Unauthorised Data Access →](05-pb04-abnormal-agent-activity.md)
<!-- /nav -->
