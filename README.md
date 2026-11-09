<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">The command line and SSH agent of DynamicDNSPro Vault.<br>Secrets in your scripts, deploys and SSH sessions — never in your code, history or disk.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <strong>🇬🇧 English</strong> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **This repository publishes official binary releases only** — the source code is private.

## Download

| Platform | File | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.zip) | signed with Developer ID and notarized by Apple |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | unzip and add the folder to your PATH |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | extract to /usr/local/bin |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | extract to /usr/local/bin |

## Getting started

Connect this computer. It prints a code and opens Vault in your browser; approve it with your password and choose a mode:

```sh
vaultd login
```

- **Approve each use** — every secret vaultd reads must be approved in Vault, like AI agents.
- **Authorize this device** — vaultd reads without asking until you revoke it in Settings › Developer.

## Usage

```sh
vaultd search github                          # search items (never prints secrets)
vaultd read "GitHub" --field user             # print a field (password by default; also user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # run a command with secrets in environment variables
vaultd inject -i config.tpl -o config.env     # fill a template, e.g. a .env or a config file
vaultd ssh-agent                              # SSH agent with the keys stored in your vault
```

## Security

- Locked items and end-to-end encrypted items are never delivered to vaultd.
- The device token is stored with 0600 permissions; in CI you can pass it with `VAULTD_TOKEN` and nothing is written to disk.
- `inject -o` writes files readable only by you.
- The SSH agent is read-only and keeps private keys only in memory; in approve-each mode every signature is approved in Vault.
- Every read is recorded in the vault activity log.

## Verify a download

Each release includes `SHA256SUMS.txt`:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Language

vaultd speaks English, Spanish, German, French, Italian and Portuguese (from `LANG`, or force it with `VAULTD_LANG=es`).
