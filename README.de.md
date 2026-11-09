<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">Kommandozeile und SSH-Agent von DynamicDNSPro Vault.<br>Geheimnisse in Skripten, Deployments und SSH-Sitzungen – nie im Code, im Verlauf oder auf der Festplatte.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <strong>🇩🇪 Deutsch</strong> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Dieses Repository veröffentlicht nur offizielle Binärversionen** – der Quellcode ist privat.

## Download

| Plattform | Datei | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.zip) | mit Developer ID signiert und von Apple notarisiert |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | entpacken und den Ordner zum PATH hinzufügen |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | nach /usr/local/bin entpacken |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | nach /usr/local/bin entpacken |

## Erste Schritte

Verbinde diesen Computer. Er zeigt einen Code und öffnet Vault im Browser; gib ihn mit deinem Passwort frei und wähle den Modus:

```sh
vaultd login
```

- **Jede Nutzung freigeben** – jedes Geheimnis, das vaultd liest, wird in Vault freigegeben, wie bei KI-Agenten.
- **Dieses Gerät autorisieren** – vaultd liest ohne Nachfrage, bis du es unter Einstellungen › Entwickler widerrufst.

## Verwendung

```sh
vaultd search github                          # Einträge suchen (zeigt nie Geheimnisse)
vaultd read "GitHub" --field user             # ein Feld ausgeben (standardmäßig das Passwort; auch user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # einen Befehl mit Geheimnissen in Umgebungsvariablen ausführen
vaultd inject -i config.tpl -o config.env     # eine Vorlage füllen, z. B. eine .env- oder Konfigurationsdatei
vaultd ssh-agent                              # SSH-Agent mit den Schlüsseln aus deinem Tresor
```

## Sicherheit

- Gesperrte und Ende-zu-Ende-verschlüsselte Einträge werden nie an vaultd übergeben.
- Das Gerätetoken wird mit Rechten 0600 gespeichert; in CI kannst du es per `VAULTD_TOKEN` übergeben, ohne dass etwas auf die Festplatte geschrieben wird.
- `inject -o` schreibt Dateien, die nur du lesen kannst.
- Der SSH-Agent ist schreibgeschützt und hält private Schlüssel nur im Speicher; im Modus „jede Nutzung“ wird jede Signatur in Vault freigegeben.
- Jeder Lesezugriff wird im Aktivitätsprotokoll des Tresors festgehalten.

## Download prüfen

Jede Version enthält `SHA256SUMS.txt`:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Sprache

vaultd spricht Deutsch, Englisch, Spanisch, Französisch, Italienisch und Portugiesisch (über `LANG` oder erzwungen mit `VAULTD_LANG=de`).
