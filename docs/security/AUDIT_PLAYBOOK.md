# Audit Playbook (Gen Agent Trust Hub, Socket, Snyk)

## Gen Agent Trust Hub (skill scanning)
Gen provides a free skills scanner intended to analyze agent skills for hidden logic, unauthorized access, and malicious behavior patterns. citeturn0search4turn2search3
- Scan the skill URL before installation.
- Review findings for:
  - Hidden instructions and obfuscated payloads
  - Data exfiltration patterns
  - Unsafe file/system access requirements

## Socket (supply chain and repository scanning)
Socket offers GitHub Actions/CLI integrations to scan repos and dependencies for supply chain risks across alert categories. citeturn3view1turn2search1
- Configure `SOCKET_SECURITY_API_KEY` in GitHub Secrets
- Enable `.github/workflows/socket.yml`

## Snyk (dependency and code scanning)
Snyk provides GitHub Actions and supports SARIF output upload into GitHub Code Scanning. citeturn2search2turn2search7
- Configure `SNYK_TOKEN` in GitHub Secrets
- Enable `.github/workflows/snyk.yml`

## Minimum audit artifacts to retain
- SBOM artifact from `.github/workflows/sbom.yml`
- CodeQL results in GitHub Security tab
- Socket scan results (PR checks / issues comments depending on config)
- Snyk SARIF results (if enabled)

## Common audit failure points
- Missing lockfile
- Secrets committed to git history
- CORS configured as `*` with credentials
- Missing object-level authorization checks (IDOR)
- Retry-unsafe creates (no idempotency + no unique constraints)
