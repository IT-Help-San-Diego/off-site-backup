# Security Intent Exceptions Report

Generated: 2026-03-12T05:38:11.758214

| Status | Total |
|--------|-------|
| Active intents | 6 |
| Code tags found | 6 |
| Errors | 0 |
| Warnings | 0 |

## Active Exceptions

### SECINTENT-001: TLS skip-verify in SMTP transport analyzer

- **Category**: accepted-risk
- **Severity**: medium
- **File**: `go-server/internal/analyzer/smtp_transport.go`
- **Expires**: 2027-01-15
- **Owner**: security-team
- **Justification**: The SMTP transport analyzer intentionally disables TLS certificate verification to probe mail server TLS configuration as a diagnostic tool. Certificate validation is performed independently in verifyCert().

### SECINTENT-002: TLS skip-verify in probe binary

- **Category**: accepted-risk
- **Severity**: medium
- **File**: `go-server/cmd/probe/main.go`
- **Expires**: 2027-01-15
- **Owner**: security-team
- **Justification**: The probe binary is a security diagnostic tool that intentionally connects to arbitrary servers to inspect their TLS configuration. It must bypass certificate verification to test servers with self-signed, expired, or mismatched certificates.

### SECINTENT-003: Hardcoded DNS resolver IPs

- **Category**: intentional-behavior
- **Severity**: info
- **File**: `go-server/internal/dnsclient/**`
- **Expires**: 2027-01-15
- **Owner**: dns-team
- **Justification**: Well-known public DNS resolver IPs (8.8.8.8, 1.1.1.1, 9.9.9.9, etc.) are intentional constants for the multi-resolver consensus architecture. These are documented, stable, public services — not secrets.

### SECINTENT-004: Empty stub bodies for open-core boundary

- **Category**: intentional-behavior
- **Severity**: info
- **File**: `stubs/**`
- **Expires**: 2027-01-15
- **Owner**: architecture-team
- **Justification**: OSS stubs for proprietary intel code intentionally have empty function bodies that return safe defaults. The real implementations live in dns-tool-intel (private repository).

### SECINTENT-005: Math.random for non-crypto UI purposes

- **Category**: accepted-risk
- **Severity**: low
- **File**: `static/js/main.js`
- **Expires**: 2027-01-15
- **Owner**: frontend-team
- **Justification**: Math.random() is used for non-security UI purposes such as animation timing and visual randomization. Not used for cryptographic operations.

### SECINTENT-006: DNS record test fixtures contain verification tokens

- **Category**: test-fixture
- **Severity**: info
- **File**: `.gitleaks.toml`
- **Expires**: 2027-01-15
- **Owner**: testing-team
- **Justification**: Golden fixture JSON files contain real DNS TXT record data including domain verification tokens. These are publicly available DNS records, not secrets. Gitleaks allowlist covers these patterns.

