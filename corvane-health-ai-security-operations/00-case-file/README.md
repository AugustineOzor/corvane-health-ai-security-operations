# Case File: Corvane Health and Its Two AI Systems

<!-- nav -->
[Repository home](../README.md) › Case file
<!-- /nav -->

Corvane Health, its people, systems, patients and figures are **fictional** and were created for portfolio use.

## The organisation

| Item | Detail |
| --- | --- |
| **Name** | Corvane Health |
| **Type** | Non-profit integrated health system, US Midwest |
| **Size** | 4 hospitals, 38 outpatient clinics, about 11,500 staff, about 640,000 patients a year |
| **Clinical systems** | Commercial electronic health record (EHR) with FHIR R4 APIs; licensed drug-interaction database |
| **Research** | Corvane Research Institute takes part in multi-site clinical trials with EU sponsors, so some pseudonymised trial data relates to people in the EU |
| **Regulatory profile** | HIPAA covered entity (Privacy, Security and Breach Notification Rules); applicable state health privacy and breach laws; HHS Section 1557 non-discrimination rule for patient care decision support tools; FDA clinical decision support policy; GDPR for EU trial data |

## The two AI systems

| | **Corvane Assist** | **CareLens** |
| --- | --- | --- |
| **ID** | AI-WP-001 | AI-CL-001 |
| **What it is** | Enterprise generative AI assistant, licensed from a third-party provider and configured by Corvane | In-house **agentic** clinical assistant built on a third-party large language model |
| **Used by** | About 6,000 staff | 220 hospitalists and primary care clinicians (pilot) at two hospitals |
| **Used for** | Drafting, summarising, translation of non-clinical content, and questions about Corvane policies (answers grounded in the policy library) | Summarising a patient's history, drafting visit notes and suggesting guideline-based treatment considerations for the clinician to review |
| **Patient data (PHI)** | **Not permitted.** Blocked by data loss prevention (DLP) controls | **Required**, limited to the patient the clinician is treating (minimum necessary) |
| **Can it act?** | No: text in, text out | Yes, through tools: reads the record, checks drug interactions, writes **unsigned** draft notes and **pended** order suggestions. It cannot sign notes or place orders. |
| **Owner** | Head of Digital Workplace | Director of Clinical AI Engineering |
| **Clinical safety owner** | n/a | Chief Medical Information Officer (CMIO) |
| **Risk tier** | Moderate | **High** (patient safety and PHI at scale) |
| **Stage** | Live for all staff since March 2026 | Pilot since July 2026; wider rollout decision due Q1 2027 |

## How CareLens works

```
Clinician (EHR sidebar)
   │  request: "summarise this admission and suggest next steps"
   ▼
CareLens orchestrator ──► Policy and guardrail layer (input checks, prompt-injection filter)
   │                             │
   │                             ▼
   │                      LLM (third-party, via Corvane's cloud tenant, under a BAA)
   │
   ├──► Tools (allow-listed, least privilege, every call logged)
   │      get_patient_context · search_notes · get_labs · get_medications
   │      check_interactions · search_guidelines · draft_note · propose_order
   │
   ├──► Retrieval: patient record via FHIR (only the open patient);
   │               clinical guideline library (vector index, signed snapshots)
   │
   └──► Output validation (dose ranges, allergy and interaction checks, citation check)
            │
            ▼
   Draft shown to clinician ──► clinician reviews, edits, signs or discards (human in the loop)
```

## Security and governance roles

| Role | Responsibility |
| --- | --- |
| **AI Governance Council** (co-chaired by CMIO and CISO) | Approves AI systems, risk acceptance and rollout decisions |
| **Chief Information Security Officer (CISO)** | AI security programme; owns this playbook |
| **Security Operations Center (SOC)** | 24/7 monitoring, triage and incident coordination |
| **CMIO** | Clinical safety of CareLens; leads patient safety reviews |
| **Privacy Officer** | HIPAA privacy, breach risk assessments and notifications |
| **Director of Clinical AI Engineering** | Builds and runs CareLens |
| **Head of Digital Workplace** | Runs Corvane Assist and its vendor relationship |
| **Patient Safety Officer** | Patient safety event process |
| **Research Compliance** | GDPR obligations for EU trial data |

## Security tooling referenced

SIEM (Microsoft Sentinel), endpoint detection and response, cloud access security broker and web proxy, enterprise DLP, an **AI gateway** that logs and redacts prompts and responses, EHR and FHIR audit logs, and **agent traces** recording every CareLens step and tool call.

## Frameworks used

NIST Cybersecurity Framework (CSF) 2.0 · NIST AI Risk Management Framework and its Generative AI Profile (NIST AI 600-1) · OWASP Top 10 for LLM Applications (2025) · MITRE ATLAS · HIPAA Security Rule

<!-- nav -->
---

[← Repository home](../README.md) &nbsp;|&nbsp; [Next: Part 01: Identify →](../01-identify/README.md)
<!-- /nav -->
