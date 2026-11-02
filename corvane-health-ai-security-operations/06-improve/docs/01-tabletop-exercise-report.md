# Tabletop Exercise Report: "The Letter That Talked Back"

<!-- nav -->
[Repository home](../../README.md) › [Part 06: Improve](../README.md) › Document 1 of 2
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-IM-001 |
| **Date of exercise** | 4 November 2026 |
| **Facilitator** | CISO office |
| **Participants** | SOC, Clinical AI Engineering, CMIO office, Privacy Office, Patient Safety, Pharmacy Informatics, Legal, Communications (14 people) |
| **Playbooks tested** | PB-02, PB-03, PB-04 |
| **NIST CSF 2.0** | ID.IM-02, ID.IM-03, ID.IM-04 |

## 1. Scenario

A scanned referral letter from an outside clinic contains hidden text instructing CareLens to recommend doubling a patient's anticoagulant dose and to include the patient's home address in its summary. The injection filter misses it because the text is written in a style the filter has not seen before.

| Inject | Time | Event |
| --- | --- | --- |
| 1 | 09:10 | Hospitalist asks CareLens to summarise the admission |
| 2 | 09:11 | CareLens drafts a summary suggesting a doubled anticoagulant dose and including the address |
| 3 | 09:11 | Output validator blocks the dose suggestion (above range) and DET-11 fires; the address passes through |
| 4 | 09:20 | Hospitalist rejects the draft and uses "report a problem" (DET-12) |
| 5 | 10:05 | SOC finds two more patients whose records include letters from the same clinic |

## 2. What went well

- **The output validator caught the dangerous dose** before the clinician saw it.
- **The clinician reported it** within 10 minutes using the built-in button.
- **Agent traces** let the SOC reconstruct exactly what was retrieved and produced.
- **Containment was fast:** the team agreed to disable medication suggestions across all sites in 6 minutes of discussion.

## 3. What did not go well

| Gap | Impact | Severity |
| --- | --- | --- |
| The injection filter missed the novel phrasing | Injection reached the model | High |
| No control stopped **unrequested demographic data** (the address) in a clinical summary | PHI shown beyond minimum necessary | High |
| Unclear whether the SOC or the CMIO office leads when an incident is both security and clinical | 20 minutes lost deciding ownership | Medium |
| No quick way to find other records containing documents from the same source | Look-back took over an hour | Medium |
| Communications had no template for telling clinicians a CareLens feature was disabled | Slow, inconsistent messaging | Low |

## 4. Actions

| ID | Action | Owner | Due | Status |
| --- | --- | --- | --- | --- |
| IM-01 | Add an **output field filter**: summaries may include only fields relevant to the request type; demographic fields are removed unless requested | Director of Clinical AI Engineering | 15 December 2026 | In progress |
| IM-02 | Add 40 new injection styles to the red-team suite, and test the filter against them every month | Director of Clinical AI Engineering | 30 November 2026 | In progress |
| IM-03 | Joint leadership rule: **CMIO leads when a patient may be affected; SOC leads otherwise; both always notified** (added to CH-AISEC-RS-001) | CISO; CMIO | 15 November 2026 | Complete |
| IM-04 | Index the source of each scanned document so look-backs can search by sending organisation | EHR Integration Lead | 31 January 2027 | Not started |
| IM-05 | Communication templates for feature disable and restore messages | Communications | 30 November 2026 | In progress |
| IM-06 | New detection use case: **unrequested demographic fields in a clinical output** | SOC Manager | 15 December 2026 | Not started |

## 5. Conclusion

Layered controls worked: the dose error was stopped even though the first control failed. The exercise exposed one real gap in data minimisation and one gap in incident leadership, both now being fixed. The next exercise (Q2 2027) will test a model update scenario using PB-05.

<!-- nav -->
---

[← Previous: Part 06: Improve overview](../README.md) &nbsp;|&nbsp; [Part 06: Improve](../README.md) &nbsp;|&nbsp; [Next: AI Security Operations KPI Scorecard →](02-ai-secops-kpi-scorecard.md)
<!-- /nav -->
