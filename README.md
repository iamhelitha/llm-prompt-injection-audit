# llm-prompt-injection-audit

A Claude skill that audits AI chatbots for prompt injection and related risks. It reviews system prompts, LLM API message assembly, tools, RAG and output handling, and reports strengths, weaknesses, fixes and a safe test plan.

Based on the [OWASP LLM Prompt Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html) and the OWASP Top 10 for LLM Applications 2025 (LLM01, LLM02, LLM05, LLM06, LLM07, LLM10).

## What it checks
- System prompt content (secrets, authorization in prompt, leak impact)
- Instruction/data separation and how the API request is built
- Input screening and known evasions (encoding, typoglycemia, multilingual, Best-of-N)
- Indirect injection via RAG, web, files, hidden text, images
- Tool permissions, argument validation, human approval
- Output handling (markdown/HTML rendering, exfiltration links)
- Guardrail models, rate limits, logging

## Install
**Claude Code:** copy `skills/llm-prompt-injection-audit/` into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

**Claude.ai:** zip the `llm-prompt-injection-audit` folder and upload it under Settings → Capabilities → Skills.

## Usage
Share a system prompt, your LLM API code, tool definitions or RAG setup and ask Claude to audit it for prompt injection.

## Disclaimer
Prompt wording is not a security boundary. This skill helps find weaknesses; it does not certify a system as secure.

## License
MIT
