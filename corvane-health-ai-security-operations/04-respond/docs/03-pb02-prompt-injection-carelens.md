# Playbook PB-02: Prompt Injection or Poisoned Content in CareLens

<!-- nav -->
[Repository home](../../README.md) › [Part 04: Respond](../README.md) › Document 3 of 6
<!-- /nav -->

| | |
| --- | --- |
| **Triggers** | DET-07 (injection filter on retrieved content), DET-15 (guideline index integrity failure); red-team or clinician report |
| **Default severity** | SEV-3 (blocked, no effect) · SEV-2 (reached the model) · SEV-1 (changed an output shown to a clinician, or index tampering) |
| **Lead** | SOC lead, with the Director of Clinical AI Engineering |

## Steps

| Phase | Action | Owner |
| --- | --- | --- |
| **Respond** | Pull the agent trace: which content was retrieved, what the filter flagged, what the model produced, which tools were called | SOC lead |
| | If the injection came from a **patient record document**: quarantine the document from CareLens retrieval (it stays in the EHR for clinical use) | Clinical AI Engineering |
| | If from the **guideline index** (DET-15): switch CareLens to the last good signed snapshot immediately; treat as SEV-1 | Clinical AI Engineering |
| | If an altered output reached a clinician: contact the clinician; check whether any draft was signed or order accepted | CMIO office |
| **Assess** | Did the output include data the request did not need? If yes, Privacy Officer assesses | Privacy Officer |
| | Where did the content come from (outside letter, patient portal upload, insider)? | SOC lead |
| **Recover** | Add the pattern to the injection filter and the red-team test suite; re-run the suite before re-enabling | Clinical AI Engineering |
| | For index tampering: rebuild the index from approved source, verify hashes, review who had write access | Clinical AI Engineering; CISO |
| **Improve** | Post-incident review within 10 working days; update the threat model (TC-01, TC-06) | CISO |

## Evidence to keep

Agent trace, quarantined content, filter verdicts, index hashes, clinician contact record.

<!-- nav -->
---

[← Previous: Playbook PB-01: PHI Entered into Corvane Assist](02-pb01-phi-in-corvane-assist.md) &nbsp;|&nbsp; [Part 04: Respond](../README.md) &nbsp;|&nbsp; [Next: Playbook PB-03: Unsafe or Incorrect Clinical Suggestion →](04-pb03-unsafe-clinical-suggestion.md)
<!-- /nav -->
