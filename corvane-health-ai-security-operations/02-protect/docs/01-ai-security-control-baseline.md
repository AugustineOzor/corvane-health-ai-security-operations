# AI Security Control Baseline

<!-- nav -->
[Repository home](../../README.md) › [Part 02: Protect](../README.md) › Document 1 of 3
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-PR-001 |
| **Systems** | AI-WP-001 Corvane Assist; AI-CL-001 CareLens |
| **Version** | 1.0 |
| **Owner** | CISO |
| **Approved by** | AI Governance Council, 21 October 2026 |
| **NIST CSF 2.0** | PR.AA, PR.DS, PR.PS, PR.AT, PR.IR |

## 1. Purpose

This baseline sets the minimum preventive controls for each system, tied to the threats in the two threat models. Every control has an ID, an owner and a way to verify it.

## 2. Corvane Assist

| ID | Control | Threats addressed | How verified | Owner |
| --- | --- | --- | --- | --- |
| PA-01 | Corvane Assist is the **only approved** general-purpose GenAI tool; enterprise terms prohibit the provider from training on Corvane data | TA-02, TA-07 | Contract review | Head of Digital Workplace |
| PA-02 | Access only through single sign-on with multi-factor authentication; no personal accounts | TA-06 | Identity configuration review | Identity and Access Management |
| PA-03 | All traffic routed through the AI gateway, which logs prompts and responses with PHI masked | TA-01, TA-08 | Gateway configuration check | CISO |
| PA-04 | DLP inspects prompts and uploads; blocks medical record numbers, Social Security numbers, and name-plus-date-of-birth patterns, and warns on other identifiers | TA-01, TA-08 | Monthly DLP test set | CISO |
| PA-05 | Web proxy and cloud access security broker block unapproved public AI sites, with a page that points staff to Assist | TA-02 | Block-list test | CISO |
| PA-06 | Generative AI Acceptable Use Standard (CH-AISEC-PR-003) acknowledged before first use | TA-01, TA-03, TA-08 | Acknowledgement records | Head of Digital Workplace |
| PA-07 | Policy Q&A answers must cite the source policy; answers without a citation show a warning | TA-03 | Monthly answer sampling | Head of Digital Workplace |
| PA-08 | Upload limits: no more than 10 files or 50 MB per session | TA-06 | Configuration check | Head of Digital Workplace |
| PA-09 | Vendor must give 30 days' notice of model or data-processing changes | TA-07 | Contract review | Procurement |

## 3. CareLens

| ID | Control | Threats addressed | How verified | Owner |
| --- | --- | --- | --- | --- |
| PC-01 | **Patient-scoped access:** each request gets a short-lived FHIR token limited to the patient open in the clinician's EHR session | TC-02, TC-10 | Penetration test; token inspection | EHR Integration Lead |
| PC-02 | **Role-based access:** only clinicians with a care relationship and the CareLens role can invoke it | TC-02 | Access review each quarter | Identity and Access Management |
| PC-03 | **Tool allow-list and least privilege** as set out in the tool permission matrix (CH-AISEC-PR-002); no tool can sign, place orders, or send data outside Corvane | TC-03, TC-10 | Automated policy tests in CI pipeline | Director of Clinical AI Engineering |
| PC-04 | **Retrieved content is data, not instructions:** record text and documents are wrapped and labelled; the model is instructed never to follow them | TC-01 | Red-team test suite | Director of Clinical AI Engineering |
| PC-05 | **Prompt-injection filter** on retrieved content and user input; flagged content is excluded and logged | TC-01 | Red-team test suite | Director of Clinical AI Engineering |
| PC-06 | **Output validator:** checks doses against ranges, allergies, interactions and citations before anything is shown; blocks or flags failures | TC-04, TC-11 | Clinical test set (2,000 cases) | CMIO; Pharmacy Informatics |
| PC-07 | **Human in the loop:** outputs are drafts; notes stay unsigned and orders stay pended until a clinician acts; suggestions show their sources | TC-04, TC-05, TC-10 | Workflow demonstration | CMIO |
| PC-08 | **Friction for high-risk suggestions:** medication changes require the clinician to open the cited source before accepting | TC-05 | Workflow demonstration | CMIO |
| PC-09 | **Signed guideline snapshots:** the vector index is rebuilt only from approved, hashed content; hashes checked at load | TC-06 | Integrity check log | Clinical Content Lead |
| PC-10 | **Model pinning:** a specific model version is used; any change goes through the clinical test set and approval | TC-08 | Registry review | Director of Clinical AI Engineering |
| PC-11 | **Rate and step limits:** maximum 12 tool calls and 60 seconds per request | TC-03 | Load and abuse tests | Director of Clinical AI Engineering |
| PC-12 | **Log hygiene:** traces mask PHI; full-fidelity traces kept in a restricted store with access logged | TC-09 | Log review | CISO |
| PC-13 | System prompt holds no secrets; safety rules are enforced in code, not only in the prompt | TC-07 | Code review | Director of Clinical AI Engineering |
| PC-14 | Fairness testing of suggestions across patient groups before rollout and every quarter | TC-11 | Fairness test report | CMIO; Health Equity Lead |
| PC-15 | Clinician training before access, covering limits of CareLens and how to report problems | TC-05 | Training records | CMIO |

## 4. Shared controls

| ID | Control | Owner |
| --- | --- | --- |
| PS-01 | BAAs with the LLM provider, Assist provider and drug-interaction vendor | Privacy Officer |
| PS-02 | Encryption in transit and at rest; keys managed by Corvane | CISO |
| PS-03 | Vulnerability scanning of AI components and dependencies; critical findings fixed within 7 days | CISO |
| PS-04 | AI systems covered by the HIPAA Security Rule risk analysis | Privacy Officer; CISO |

## 5. Controls in other functions

Detection controls are in the detection catalogue (Part 03), response in the playbooks (Part 04) and recovery in the runbook (Part 05).

<!-- nav -->
---

[← Previous: Part 02: Protect overview](../README.md) &nbsp;|&nbsp; [Part 02: Protect](../README.md) &nbsp;|&nbsp; [Next: CareLens Tool Permission Matrix →](02-carelens-tool-permission-matrix.md)
<!-- /nav -->
