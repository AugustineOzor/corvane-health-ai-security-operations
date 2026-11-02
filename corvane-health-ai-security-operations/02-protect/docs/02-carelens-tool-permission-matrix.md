# CareLens Tool Permission Matrix

<!-- nav -->
[Repository home](../../README.md) › [Part 02: Protect](../README.md) › Document 2 of 3
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-PR-002 |
| **System** | AI-CL-001 CareLens |
| **Version** | 1.0 |
| **Owner** | Director of Clinical AI Engineering |
| **Approved by** | AI Governance Council, 21 October 2026 |
| **Spreadsheet** | `../files/CH-AISEC-PR-002_CareLens_Tool_Permission_Matrix.xlsx` |

## 1. Purpose

An AI agent is only as safe as what it is allowed to do. This matrix lists every tool CareLens can call, what it may read or write, under which limits, and what needs a human. Anything not listed is denied by default.

## 2. Permission levels

- **Read:** retrieves data; changes nothing
- **Draft:** creates content in a pending state that has no effect until a clinician acts
- **Act:** changes the record or triggers something in the real world. **CareLens has no Act permissions.**

## 3. Matrix

| Tool | Purpose | Level | Data scope | Limits | Human step required | Logged |
| --- | --- | --- | --- | --- | --- | --- |
| get_patient_context | Problems, allergies, recent encounters | Read | Open patient only | 1 call per request | No | Yes |
| search_notes | Find relevant clinical notes | Read | Open patient; last 24 months | 5 calls; 20 notes max | No | Yes |
| get_labs | Lab results | Read | Open patient; last 24 months | 3 calls | No | Yes |
| get_medications | Active and recent medications | Read | Open patient | 1 call | No | Yes |
| check_interactions | Drug-interaction and allergy check | Read | Medication list only (minimum fields) | 3 calls | No | Yes |
| search_guidelines | Approved clinical guidelines | Read | Signed guideline index | 5 calls | No | Yes |
| draft_note | Write a draft note to the clinician's inbox | Draft | Open patient's chart; unsigned | 1 per request | **Clinician must review and sign** | Yes |
| propose_order | Suggest an order for the clinician | Draft | Open patient; pended state only; formulary items only | 3 per request | **Clinician must review and sign** | Yes |

## 4. Denied by design

| Capability | Why denied |
| --- | --- |
| Sign notes or orders | Clinical accountability stays with the clinician |
| Access any patient other than the open one | Minimum necessary; prevents cross-patient leakage |
| Send email, messages or data outside Corvane | Prevents exfiltration through tools |
| Browse the web | Untrusted content and data leakage |
| Change its own configuration, prompts or tool list | Prevents self-escalation |
| Write to the guideline index | Prevents poisoning |

## 5. Enforcement

Permissions are enforced in the tool layer, not just described in the prompt. Automated tests in the deployment pipeline try every denied capability and every limit; a release fails if any test passes that should not. Every tool call is recorded in the agent trace with the request ID, patient context hash, arguments (PHI masked) and result status.

<!-- nav -->
---

[← Previous: AI Security Control Baseline](01-ai-security-control-baseline.md) &nbsp;|&nbsp; [Part 02: Protect](../README.md) &nbsp;|&nbsp; [Next: Generative AI Acceptable Use Standard →](03-genai-acceptable-use-standard.md)
<!-- /nav -->
