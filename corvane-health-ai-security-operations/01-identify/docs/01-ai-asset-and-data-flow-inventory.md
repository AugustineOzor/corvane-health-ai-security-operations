# AI Asset and Data Flow Inventory

<!-- nav -->
[Repository home](../../README.md) › [Part 01: Identify](../README.md) › Document 1 of 3
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-ID-001 |
| **Version** | 1.0 |
| **Owner** | CISO, with system owners |
| **Date** | 2 October 2026 |
| **NIST CSF 2.0** | ID.AM-01 to ID.AM-05; ID.AM-07 |

## 1. Purpose

You cannot protect what you have not listed. This inventory records every component that makes up Corvane Assist and CareLens, what data flows between them, and where those flows cross a trust boundary. The threat models and controls in this repository are built on it.

## 2. Assets

| ID | Asset | System | Type | Data handled | Owner | Criticality |
| --- | --- | --- | --- | --- | --- | --- |
| A-01 | Corvane Assist tenant | Assist | SaaS (third party) | Staff prompts, uploaded documents, outputs | Head of Digital Workplace | Medium |
| A-02 | Policy library index | Assist | Retrieval index | Internal policies (no PHI) | Head of Digital Workplace | Medium |
| A-03 | AI gateway | Both | Proxy (Corvane) | All prompts and responses, redacted copies in logs | CISO | High |
| A-04 | CareLens orchestrator | CareLens | Application (Corvane) | Patient context, prompts, tool calls | Director of Clinical AI Engineering | High |
| A-05 | Large language model endpoint | CareLens | Cloud API under BAA | Prompts containing PHI; outputs | Director of Clinical AI Engineering | High |
| A-06 | FHIR API connector | CareLens | Integration | PHI for the open patient | EHR Integration Lead | High |
| A-07 | Clinical guideline vector index | CareLens | Retrieval index | Approved guidelines (no PHI) | Clinical Content Lead | High |
| A-08 | Drug-interaction service | CareLens | Licensed API | Medication lists (PHI) | Pharmacy Informatics | High |
| A-09 | Tool layer | CareLens | Code (Corvane) | Tool requests and results | Director of Clinical AI Engineering | High |
| A-10 | Output validator | CareLens | Code (Corvane) | Draft outputs | Director of Clinical AI Engineering | High |
| A-11 | Agent trace store | CareLens | Log store | Full traces, PHI masked | CISO | High |
| A-12 | Model and prompt registry | CareLens | Repository | System prompts, model versions, configurations | Director of Clinical AI Engineering | High |
| A-13 | SIEM | Both | Security platform | Security events and alerts | SOC Manager | High |

## 3. Data flows and trust boundaries

| Flow | From | To | Data | Trust boundary crossed | Protection |
| --- | --- | --- | --- | --- | --- |
| F-01 | Staff browser | Assist tenant (via AI gateway) | Prompts, files | Corvane → third-party SaaS | SSO; DLP blocks PHI; gateway logging |
| F-02 | Assist tenant | Policy library | Queries | Third party → Corvane content | Read-only connector |
| F-03 | Clinician in EHR | CareLens orchestrator | Request, patient context | Within Corvane | EHR session context; role checks |
| F-04 | Orchestrator | LLM endpoint | Prompts with PHI | Corvane → cloud provider | Private endpoint; encryption; BAA; no-training terms |
| F-05 | Tool layer | FHIR API | PHI queries | Within Corvane | Scoped token for the open patient only |
| F-06 | Tool layer | Drug-interaction service | Medication list | Corvane → licensed vendor | BAA; minimum fields |
| F-07 | Orchestrator | Guideline index | Search queries | Within Corvane | Read-only; signed index snapshots |
| F-08 | Orchestrator | EHR inbox and order queue | Unsigned drafts and pended orders | Within Corvane | Write limited to draft and pended states |
| F-09 | All components | SIEM and trace store | Logs | Within Corvane | PHI masking; access logging |

**Highest-risk flows:** F-04 (PHI leaving Corvane's environment), F-05 (broad patient data access if scoping fails) and F-08 (the only flow where the agent writes into the clinical record).

## 4. Review

The inventory is updated with every change to models, tools, connectors or vendors, and reviewed by the SOC and system owners every quarter.

<!-- nav -->
---

[← Previous: Part 01: Identify overview](../README.md) &nbsp;|&nbsp; [Part 01: Identify](../README.md) &nbsp;|&nbsp; [Next: Threat Model: Corvane Assist →](02-threat-model-corvane-assist.md)
<!-- /nav -->
