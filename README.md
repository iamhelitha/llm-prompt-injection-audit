<div align="center">

<img src="assets/cover.svg" alt="LLM Prompt Injection Audit: find the holes in your chatbot before attackers do" width="100%">

# LLM Prompt Injection Audit

**A Claude skill that audits AI chatbots and agents for prompt injection, leakage and excessive agency, then hands you a prioritized fix list and a safe test plan.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-d97757.svg)](https://docs.claude.com)
[![OWASP LLM Top 10 2025](https://img.shields.io/badge/OWASP-LLM%20Top%2010%202025-blue.svg)](https://genai.owasp.org/llm-top-10/)
[![Claude Code](https://img.shields.io/badge/Works%20with-Claude%20Code-8b5cf6.svg)](https://claude.com/claude-code)

[Install](#install) · [Usage](#usage) · [What it checks](#what-it-checks) · [What you get](#what-you-get) · [Disclaimer](#disclaimer)

</div>

---

## Why this exists

LLMs read instructions and data in the same channel, so there is no enforced boundary between them. A system that is only safe because the model *obeys its prompt* is not safe. This skill reviews your whole LLM pipeline, not just the prompt text, and points to the controls that actually hold: authorization, tool permissions, argument validation, approval gates, output encoding and rate limits.

> **Prompt wording is not a security boundary.** Assume your system prompt will leak, and judge the design by what happens when it does.

## What it checks

| Area | OWASP | Looks for |
|---|---|---|
| **System prompt** | LLM07 | Secrets, authorization rules and abusable business logic inside the prompt; leak impact; canary markers |
| **Message assembly** | LLM01 | String concatenation, user text in the system role, forged history, templated user fields |
| **Input screening** | LLM01 | Coverage of encodings, typoglycemia, multilingual tricks, Best-of-N spam, multi-turn escalation |
| **Indirect injection** | LLM01 | RAG poisoning, web/file/email content, hidden text, instructions inside images |
| **Tools and agency** | LLM06 | Over-broad scopes, missing per-user authz, unvalidated arguments, no human approval on side effects |
| **Output handling** | LLM05 | Markdown/HTML rendering, exfiltration links, model output reaching SQL, shell or other agents |
| **Data exposure** | LLM02 | Sensitive data reachable from context or tools |
| **Abuse limits** | LLM10 | Rate limits, token and cost caps, logging and monitoring |

## Install

**Claude Code (plugin marketplace, recommended)**

```text
/plugin marketplace add iamhelitha/llm-prompt-injection-audit
/plugin install llm-prompt-injection-audit@iamhelitha
```

**Claude Code (manual copy)**

```bash
git clone https://github.com/iamhelitha/llm-prompt-injection-audit.git
cp -r llm-prompt-injection-audit/skills/llm-prompt-injection-audit ~/.claude/skills/   # personal
# or: cp -r ... .claude/skills/                                                        # project-only
```

**Claude.ai**

1. Zip the `skills/llm-prompt-injection-audit` folder.
2. Go to **Settings → Capabilities → Skills** and upload the zip.

## Usage

Share any of the following and ask Claude to audit it:

- a system prompt
- the code that builds your LLM API request
- tool or function definitions
- your RAG or agent setup

Example prompts:

```text
Audit this system prompt for prompt injection risks.
Review my chat endpoint and tool definitions. What could an attacker make the model do?
Check my RAG pipeline for indirect injection and suggest fixes.
```

You don't need to say "prompt injection". The skill triggers whenever you ask for a chatbot or agent security review. If you only share part of the system, it audits what it has and lists what it couldn't assess.

## What you get

1. **Attack-surface map**: trusted inputs, untrusted inputs, capabilities and blast radius.
2. **Strengths and weaknesses** per area, with the exact line or code quoted as evidence.
3. **Severity ratings** based on capability × exposure, so a read-only FAQ bot isn't flagged like an email agent.
4. **Concrete fixes**, with controls placed in code rather than in prompt wording.
5. **A safe test plan** you can run against your own system.

## Based on

- [OWASP LLM Prompt Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/): LLM01, LLM02, LLM05, LLM06, LLM07, LLM10

## Repository layout

```text
.
├── .claude-plugin/                          # marketplace + plugin manifests
├── assets/cover.svg                         # README cover image
├── skills/
│   └── llm-prompt-injection-audit/
│       └── SKILL.md                         # the skill
├── LICENSE
└── README.md
```

## Disclaimer

This skill helps find weaknesses. It does not certify a system as secure. Only test systems you own or are authorized to assess.

## License

[MIT](LICENSE)
