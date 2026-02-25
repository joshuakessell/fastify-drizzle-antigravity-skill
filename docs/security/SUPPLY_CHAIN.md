# Supply Chain Security

## Goals
- Prevent introduction of malicious or high-risk dependencies
- Detect vulnerable dependencies early in PRs
- Produce auditable artifacts (SBOM) for compliance

## CI scanning
- Socket GitHub Actions/CLI integration scans repositories for dependency and supply chain risks. citeturn3view1turn2search1
- Snyk GitHub Actions supports SARIF output upload to GitHub Code Scanning. citeturn2search2turn2search7
- GitHub Dependency Review flags dependency changes per PR.

## SBOM
- Generate and publish a CycloneDX SBOM as a CI artifact (example workflow included).
- Store SBOM in build artifacts (not in git) unless required by policy.

## Hardening recommendations
- Require 2FA for npm org accounts and least-privilege publish rights.
- Pin GitHub Actions by commit SHA where policy requires.
- Block unknown registries; allow only approved registries.
