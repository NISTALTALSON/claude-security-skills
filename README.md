# Defensive Claude security skills bundle

This bundle was selected for authorized defensive work on websites and codebases: security audits, OWASP-aligned secure coding, vulnerability triage, scoped patches, regression proof, and post-patch validation.

## Recommended order

1. **Cloudflare `security-audit`** — use for a full, multi-phase audit with coverage tracking, independent finding validation, machine-readable findings, and reports. Requires a coding agent with parallel subagents and Node.js. Keep target-controlled code in an OS-enforced sandbox.
2. **OWASP `owasp-security`** — use during secure implementation and review. Covers OWASP Top 10:2025, ASVS 5.0, LLM/agent risks, and language-specific secure/unsafe patterns.
3. **Trail of Bits plugins** — use selectively:
   - `audit-context-building`, `static-analysis`, `variant-analysis`, `differential-review`, `insecure-defaults`, `sharp-edges`, `supply-chain-risk-auditor`, `fp-check` for finding and triaging issues.
   - `patching-bugs`, `post-patch-validation`, `code-improver` for reproducing, patching, proving, and regression-checking fixes.
4. **Anthropic official reference** — Claude Code already provides `/security-review`; the files in `official-reference/` are the official command/GitHub Action reference. Anthropic says automated review complements rather than replaces manual review.

## Installation on Windows Claude Code

From the extracted bundle root, copy the two primary skill folders into your user skills directory:

```powershell
New-Item -ItemType Directory -Force "$HOME\\.claude\\skills" | Out-Null
Copy-Item -Recurse -Force .\\skills\\cloudflare-security-audit "$HOME\\.claude\\skills\\cloudflare-security-audit"
Copy-Item -Recurse -Force .\\skills\\owasp-security "$HOME\\.claude\\skills\\owasp-security"
```

For Trail of Bits, the safest supported route is to add the upstream marketplace in Claude Code and install only the named plugins:

```text
/plugin marketplace add trailofbits/skills
/plugin install static-analysis@trailofbits
/plugin install differential-review@trailofbits
/plugin install patching-bugs@trailofbits
/plugin install post-patch-validation@trailofbits
```

The full selected plugin source is included for review; do not run its test/evaluation scripts as part of installation.

## Safety

Use only on systems you own or have written authorization to assess. Review `SKILL.md` and scripts before enabling them, keep Claude Code permissions in Manual mode for sensitive repositories, and use a sandbox/dev container for target-controlled code. Do not use outside-mode probing against an unauthorized URL.

## Provenance

- Cloudflare security-audit: https://github.com/cloudflare/security-audit-skill
- OWASP skill: https://github.com/agamm/claude-code-owasp
- Trail of Bits skills: https://github.com/trailofbits/skills
- Anthropic security review: https://github.com/anthropics/claude-code-security-review
