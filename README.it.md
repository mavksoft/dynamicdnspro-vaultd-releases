<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">La riga di comando e l’agente SSH di DynamicDNSPro Vault.<br>Segreti nei tuoi script, deploy e sessioni SSH — mai nel codice, nella cronologia o su disco.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <strong>🇮🇹 Italiano</strong> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Questo repository pubblica solo le versioni binarie ufficiali** — il codice sorgente è privato.

## Download

| Piattaforma | File | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.dmg](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.dmg) | firmato con Developer ID, notarizzato e graffato da Apple: aprilo e trascina vaultd su bin |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | decomprimi e aggiungi la cartella al PATH |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | estrai in /usr/local/bin |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | estrai in /usr/local/bin |

## Primi passi

Collega questo computer. Mostra un codice e apre Vault nel browser; approvalo con la tua password e scegli la modalità:

```sh
vaultd login
```

- **Approva ogni uso** — ogni segreto letto da vaultd si approva in Vault, come per gli agenti IA.
- **Autorizza questo dispositivo** — vaultd legge senza chiedere finché non lo revochi in Impostazioni › Sviluppatore.

## Uso

```sh
vaultd search github                          # cerca elementi (non mostra mai segreti)
vaultd read "GitHub" --field user             # mostra un campo (di default la password; anche user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # esegue un comando con segreti nelle variabili d’ambiente
vaultd inject -i config.tpl -o config.env     # compila un modello, per esempio un .env o un file di configurazione
vaultd ssh-agent                              # agente SSH con le chiavi salvate nella tua cassaforte
```

## Sicurezza

- Gli elementi bloccati e quelli cifrati end-to-end non vengono mai consegnati a vaultd.
- Il token del dispositivo è salvato con permessi 0600; in CI puoi passarlo con `VAULTD_TOKEN` e non viene scritto nulla su disco.
- `inject -o` scrive file leggibili solo da te.
- L’agente SSH è di sola lettura e tiene le chiavi private solo in memoria; in modalità “ogni uso” ogni firma si approva in Vault.
- Ogni lettura resta nel registro attività della cassaforte.

## Verificare un download

Ogni versione include `SHA256SUMS.txt`:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Lingua

vaultd parla italiano, inglese, spagnolo, tedesco, francese e portoghese (da `LANG`, o forzalo con `VAULTD_LANG=it`).
