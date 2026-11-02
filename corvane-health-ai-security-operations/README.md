<img width="2560" height="840" alt="corvane-health-banner" src="https://github.com/user-attachments/assets/1076b1c5-f7af-4d0c-9814-5b5ed104c7f6" />


# Corvane Health: AI Security Operations Playbook

A fictional, end-to-end **AI security operations** programme for a US health system running two very different AI systems:

- **Corvane Assist**: an enterprise generative AI assistant for about 6,000 staff, where the main risk is people putting patient data in the wrong place.
- **CareLens**: an in-house **agentic** clinical assistant that reads patient records, calls tools and drafts notes and order suggestions, where the risks are PHI exposure *and* patient safety.

Each system is taken through the full loop (**Identify → Protect → Detect → Respond → Recover → Improve**), organised around **NIST CSF 2.0** and the **NIST AI RMF**, and mapped to the **OWASP Top 10 for LLM Applications (2025)**, **MITRE ATLAS** and the **HIPAA Security Rule**.

## The story in one minute

1. **Identify:** 13 assets and 9 data flows are mapped; 19 threats are modelled, including indirect prompt injection through a scanned letter and plausible-but-wrong treatment suggestions.
2. **Protect:** CareLens gets patient-scoped access, a tool allow-list with no power to sign or order, an output validator and genuine human review. Assist gets DLP, blocking of unapproved AI tools and a plain-language acceptable use standard.
3. **Detect:** 16 detection use cases feed the SOC, from PHI in prompts to cross-patient access and unapproved model versions.
4. **Respond and Recover:** five playbooks and a rollback runbook cover PHI exposure, prompt injection, unsafe suggestions, abnormal agent activity and model changes, each with a patient safety review where needed.
5. **Improve:** a tabletop exercise shows layered defences stopping a dangerous dose suggestion, but exposes a data-minimisation gap and unclear incident leadership, both now being fixed.

**[Start reading: Case file →](00-case-file/README.md)**

## Parts

| Part | NIST CSF 2.0 | Contents |
| --- | --- | --- |
| [00 Case file](00-case-file/README.md) | | Organisation, both AI systems, CareLens architecture, roles, tooling |
| [01 Identify](01-identify/README.md) | ID | Asset and data flow inventory; threat models for both systems; threat and control matrix |
| [02 Protect](02-protect/README.md) | PR | Control baseline; CareLens tool permission matrix; GenAI acceptable use standard |
| [03 Detect](03-detect/README.md) | DE | 16 AI detection use cases with example SIEM logic |
| [04 Respond](04-respond/README.md) | RS | Severity and triage guide; five incident playbooks |
| [05 Recover](05-recover/README.md) | RC | Recovery and rollback runbook; return-to-service rules |
| [06 Improve](06-improve/README.md) | ID.IM | Tabletop exercise report; KPI scorecard |

Every document is in Markdown, with a Word version in each part's `files` folder. Four Excel workbooks (threat and control matrix, tool permission matrix, detection use cases and KPI scorecard) use drop-down lists, conditional formatting and live summary formulas.

## Disclaimer

Corvane Health, Corvane Assist, CareLens and all people, figures and events are fictional and were created for portfolio use. This repository is not legal, clinical or regulatory advice. Regulatory references are summaries: always verify them against the official texts.
