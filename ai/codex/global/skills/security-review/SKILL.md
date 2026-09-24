---
name: security-review
description: Use when a change crosses a meaningful trust boundary or handles authentication/authorization, secrets/tokens, sensitive data, payments, webhooks, uploads, untrusted URLs/content, shell execution, dynamic queries, or network exposure. Do not use for routine internal code or ordinary database access with no new security boundary.
---

# Security review

Use this skill to identify concrete, actionable security risks in the changed surface. It is not a generic audit checklist to apply to every patch.

## Workflow

1. **Identify assets and trust boundaries.** State what is sensitive/privileged, which inputs are attacker-controlled, and where authority changes.
2. **Trace relevant data/control flow.** Follow untrusted input, identity/permissions, secrets, files, URLs, commands, queries, or sensitive outputs to the actual sink or decision point.
3. **Form concrete abuse cases.** Ask what an attacker with realistic preconditions could read, modify, execute, impersonate, bypass, or exhaust.
4. **Validate controls.** Check authentication, authorization/ownership, input handling, secret exposure, safe external calls, signature verification, file/path handling, query/command construction, and output/logging only where relevant.
5. **Report evidence-based findings.** A finding should include location, preconditions, abuse path, impact, and the smallest practical remediation. Mark uncertainty explicitly.
6. **Define proof.** Add focused negative/authorization/security tests or manual reproduction steps for material findings.

For a deeper review of a security-sensitive change, read `references/security-checklist.md` selectively.

## Severity guidance

Use severity to communicate impact and exploitability, not drama:
- **Critical:** straightforward compromise with severe impact and little mitigation.
- **High:** serious unauthorized access/action or sensitive exposure under realistic conditions.
- **Medium:** meaningful weakness requiring additional conditions or with bounded impact.
- **Low:** defense-in-depth or limited practical impact.

## Guardrails

- Do not invent vulnerabilities from category names alone.
- Do not flag theoretical issues without a plausible path from controllable input or authority to impact.
- Do not duplicate an unrelated full-repository security audit unless explicitly requested.
- Security controls enforced only by an untrusted client are not authorization boundaries.
