# Claude Code Skills

Project-level skills, automatically loaded by Claude Code in every session on this repository.

| Skill | Purpose | Source | License |
|---|---|---|---|
| `frontend-design` | Distinctive, non-generic UI/visual design: deliberate palette, typography, layout and signature elements instead of templated AI defaults. | [anthropics/skills](https://github.com/anthropics/skills) | Apache 2.0 (see `frontend-design/LICENSE.txt`) |
| `owasp-security` | Secure app development and review: OWASP Top 10:2025, ASVS 5.0, LLM Top 10 (2025), Agentic AI security (2026), plus per-language pitfalls. | [agamm/claude-code-owasp](https://github.com/agamm/claude-code-owasp) | MIT (see `owasp-security/LICENSE.txt`) |
| `token-efficiency` | Minimize token usage: filter before reading, targeted search over full-file reads, quiet command output, summaries instead of dumps. | Authored for this repo | Same as repository |

Skills activate automatically when relevant (e.g. `owasp-security` when writing auth code, `frontend-design` when building UI). They can also be invoked explicitly, e.g. `/frontend-design`.
