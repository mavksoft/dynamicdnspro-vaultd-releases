<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">La ligne de commande et l’agent SSH de DynamicDNSPro Vault.<br>Des secrets dans vos scripts, déploiements et sessions SSH — jamais dans le code, l’historique ou le disque.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <strong>🇫🇷 Français</strong> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Ce dépôt publie uniquement les versions binaires officielles** — le code source est privé.

## Téléchargement

| Plateforme | Fichier | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.dmg](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.dmg) | signé Developer ID, notarisé et agrafé par Apple — ouvrez-le et double-cliquez sur « Instalar vaultd » (mot de passe du Mac demandé) |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | décompressez et ajoutez le dossier au PATH |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | extrayez dans /usr/local/bin |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | extrayez dans /usr/local/bin |

## Premiers pas

Connectez cet ordinateur. Il affiche un code et ouvre Vault dans le navigateur ; approuvez-le avec votre mot de passe et choisissez le mode :

```sh
vaultd login
```

- **Approuver chaque usage** — chaque secret lu par vaultd est approuvé dans Vault, comme pour les agents d’IA.
- **Autoriser cet appareil** — vaultd lit sans demander jusqu’à ce que vous le révoquiez dans Réglages › Développeur.

## Utilisation

```sh
vaultd search github                          # rechercher des éléments (n’affiche jamais de secrets)
vaultd read "GitHub" --field user             # afficher un champ (le mot de passe par défaut ; aussi user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # lancer une commande avec des secrets dans les variables d’environnement
vaultd inject -i config.tpl -o config.env     # remplir un modèle, par exemple un .env ou un fichier de configuration
vaultd ssh-agent                              # agent SSH avec les clés stockées dans votre coffre
```

## Sécurité

- Les éléments verrouillés et chiffrés de bout en bout ne sont jamais remis à vaultd.
- Le jeton de l’appareil est stocké avec les droits 0600 ; en CI, passez-le avec `VAULTD_TOKEN` et rien n’est écrit sur le disque.
- `inject -o` écrit des fichiers lisibles par vous seul.
- L’agent SSH est en lecture seule et garde les clés privées uniquement en mémoire ; en mode « chaque usage », chaque signature est approuvée dans Vault.
- Chaque lecture est consignée dans le journal d’activité du coffre.

## Vérifier un téléchargement

Chaque version inclut `SHA256SUMS.txt` :

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Langue

vaultd parle français, anglais, espagnol, allemand, italien et portugais (selon `LANG`, ou forcez-le avec `VAULTD_LANG=fr`).
