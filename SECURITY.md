# Security Policy

## Supported versions
This template is intended for active development branches. For released systems, define supported release branches and patch timelines here.

## Reporting a vulnerability
- Prefer private reporting through your organization’s security intake process.
- Include: affected endpoint(s), reproduction steps, expected vs actual behavior, and impact.

## Secure development requirements
1. **No secrets in git**: never commit tokens, connection strings, or private keys.
2. **Lockfiles required**: commit exactly one lockfile for your package manager.
3. **Mandatory CI checks**:
   - CodeQL (code scanning)
   - Dependency Review (PR dependency diffs)
   - Supply chain scanning (Socket)
   - Optional: Snyk SARIF upload

## Security scanning rationale
- Gen Agent Trust Hub provides automated analysis for agent skills to detect hidden logic, unauthorized access, and other malicious behavior patterns. citeturn0search4turn2search3
- Socket provides dependency and supply chain risk detection across multiple alert categories. citeturn3view1
