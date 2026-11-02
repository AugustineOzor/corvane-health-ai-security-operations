# Threat Model: Corvane Assist

<!-- nav -->
[Repository home](../../README.md) › [Part 01: Identify](../README.md) › Document 2 of 3
<!-- /nav -->

| Document control | |
| --- | --- |
| **Document ID** | CH-AISEC-ID-002 |
| **System** | AI-WP-001 Corvane Assist |
| **Version** | 1.0 |
| **Method** | Data-flow-based threat modelling, mapped to OWASP Top 10 for LLM Applications (2025) and MITRE ATLAS |
| **Participants** | Security Architecture, SOC, Digital Workplace, Privacy Office |
| **Date** | 6 October 2026 |

## 1. Scope

Staff use of Corvane Assist through the AI gateway (flows F-01 and F-02), including uploads and the policy Q&A feature. The provider's own infrastructure is covered by vendor due diligence, not this model.

## 2. Threats

| ID | Threat | OWASP LLM | MITRE ATLAS | Likelihood | Impact | Rating |
| --- | --- | --- | --- | --- | --- | --- |
| TA-01 | Staff paste or upload PHI into prompts | LLM02 Sensitive Information Disclosure | AML.T0057 LLM Data Leakage | High | High | **Critical** |
| TA-02 | Staff use unapproved public AI tools instead ("shadow AI") | n/a (governance) | n/a | High | High | **Critical** |
| TA-03 | Policy Q&A gives a confident but wrong answer, and staff act on it | LLM09 Misinformation | n/a | Medium | Medium | Medium |
| TA-04 | Jailbreak attempts to bypass usage restrictions | LLM01 Prompt Injection | AML.T0054 LLM Jailbreak | Medium | Low | Low |
| TA-05 | Malicious instructions hidden in an uploaded document change the output | LLM01 Prompt Injection (indirect) | AML.T0051 LLM Prompt Injection | Low | Medium | Low |
| TA-06 | Compromised staff account used to pull large volumes of internal content | LLM02 | n/a | Low | Medium | Low |
| TA-07 | Provider changes model or data terms without notice | LLM03 Supply Chain | n/a | Medium | Medium | Medium |
| TA-08 | Confidential business information disclosed in prompts (contracts, security details) | LLM02 | AML.T0057 | Medium | Medium | Medium |

## 3. Key insight

The main risk is not an attacker; it is **well-meaning staff putting patient data where it does not belong**. Controls focus on making the safe path easy (an approved tool that works) and the unsafe path hard (DLP and blocking of unapproved tools).

## 4. Controls

Controls for each threat are set out in the control baseline (CH-AISEC-PR-001) and the full matrix (`../files/CH-AISEC-ID-004_AI_Threat_and_Control_Matrix.xlsx`).

<!-- nav -->
---

[← Previous: AI Asset and Data Flow Inventory](01-ai-asset-and-data-flow-inventory.md) &nbsp;|&nbsp; [Part 01: Identify](../README.md) &nbsp;|&nbsp; [Next: Threat Model: CareLens →](03-threat-model-carelens.md)
<!-- /nav -->
