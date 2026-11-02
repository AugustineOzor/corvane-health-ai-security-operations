# AI Security Operations KPI Scorecard

<!-- nav -->
[Repository home](../../README.md) › [Part 06: Improve](../README.md) › Document 2 of 2
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-IM-002 |
| **Version** | 1.0 |
| **Owner** | CISO |
| **Reported to** | AI Governance Council (monthly) |
| **Spreadsheet** | `../files/CH-AISEC-IM-002_AI_SecOps_KPI_Scorecard.xlsx` |
| **NIST CSF 2.0** | GV.OV-03; ID.IM-01; DE.AE-02 |

## 1. Purpose

These measures show whether the AI security operations loop is working: whether prevention holds, detection is timely, response is fast and lessons are applied.

## 2. Measures

| ID | Measure | Target (green) | Amber | Red | October 2026 |
| --- | --- | --- | --- | --- | --- |
| K-01 | PHI submissions reaching Assist after DLP (per 10,000 prompts) | Below 0.5 | 0.5 to 2 | Above 2 | 0.3 |
| K-02 | Visits to blocked AI sites (per 1,000 staff per month) | Below 20 | 20 to 50 | Above 50 | 34 |
| K-03 | Injection attempts blocked by CareLens filter (share of detected attempts) | At least 98% | 95% to 98% | Below 95% | 97.5% |
| K-04 | Denied tool calls per 10,000 CareLens requests | Below 5 | 5 to 15 | Above 15 | 2.1 |
| K-05 | Unsafe suggestions blocked by validator (per 10,000 requests) | Below 10 | 10 to 25 | Above 25 | 6.4 |
| K-06 | Unsafe suggestions shown to clinicians (validator missed) | 0 | n/a | 1 or more | 0 |
| K-07 | Clinician suggestion acceptance rate | 40% to 90% | 30% to 40% or 90% to 95% | Outside amber | 71% |
| K-08 | Mean time to detect a SEV-1 or SEV-2 AI incident (minutes) | Below 15 | 15 to 60 | Above 60 | 11 |
| K-09 | Mean time to contain a SEV-1 or SEV-2 AI incident (minutes) | Below 30 | 30 to 120 | Above 120 | 24 |
| K-10 | Detection use cases tested in the last quarter | 100% | 90% to 100% | Below 90% | 94% |
| K-11 | Improvement actions overdue | 0 | 1 to 2 | Above 2 | 0 |
| K-12 | Staff completing GenAI acceptable use training | At least 95% | 90% to 95% | Below 90% | 96% |

## 3. October 2026 summary

Nine measures green and three amber. **K-02** (visits to blocked AI sites) points to a usability gap: staff still reach for public tools. **K-03** is just below target; the new injection styles from the tabletop exercise (IM-02) are expected to bring it back to green. **K-10** is amber because one new detection use case went live too late in the quarter to be tested.

<!-- nav -->
---

[← Previous: Tabletop Exercise Report: "The Letter That Talked Back"](01-tabletop-exercise-report.md) &nbsp;|&nbsp; [Part 06: Improve](../README.md) &nbsp;|&nbsp; [Finish: back to repository home →](../../README.md)
<!-- /nav -->
