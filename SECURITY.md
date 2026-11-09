# Security Policy — DynamicDNSPro Vault (vaultd)

DynamicDNSPro Vault (vaultd) is distributed through this repository as signed binary releases.

## Verifying a download

- macOS builds are Developer-ID signed and notarized by Apple.
- Every release includes `SHA256SUMS.txt` — verify before running.
- vaultd talks to your vault only over HTTPS and only writes secrets to disk when you ask it to (`inject -o`, with 0600 permissions).

## Reporting a vulnerability

Please report security issues privately to
**support@it-systems.es** — do not open a public issue for
vulnerabilities. We aim to acknowledge reports within 48 hours.

## Privacy

See https://vault.dynamicdnspro.com for the product privacy policy. These applications are
designed to run locally; where the product uses an account or cloud
service, only the data required for the feature is transmitted.
