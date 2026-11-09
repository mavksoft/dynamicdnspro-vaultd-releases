<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">La línea de comandos y el agente SSH de DynamicDNSPro Vault.<br>Secretos en tus scripts, despliegues y sesiones SSH, nunca en el código, el historial ni el disco.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <strong>🇪🇸 Español</strong> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Este repositorio solo publica las versiones binarias oficiales**: el código fuente es privado.

## Descarga

| Plataforma | Archivo | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.dmg](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.dmg) | firmado con Developer ID, notarizado y grapado por Apple: ábrelo y arrastra vaultd a bin |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | descomprime y añade la carpeta al PATH |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | extrae en /usr/local/bin |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | extrae en /usr/local/bin |

## Primeros pasos

Conecta este equipo. Muestra un código y abre Vault en el navegador; apruébalo con tu contraseña y elige el modo:

```sh
vaultd login
```

- **Aprobar cada uso**: cada secreto que lea vaultd se aprueba en Vault, como los agentes de IA.
- **Autorizar este equipo**: vaultd lee sin preguntar hasta que lo revoques en Ajustes › Desarrollador.

## Uso

```sh
vaultd search github                          # busca elementos (nunca muestra secretos)
vaultd read "GitHub" --field user             # muestra un campo (la contraseña por defecto; también user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # ejecuta una orden con secretos en variables de entorno
vaultd inject -i config.tpl -o config.env     # rellena una plantilla, por ejemplo un .env o un archivo de configuración
vaultd ssh-agent                              # agente SSH con las claves guardadas en tu vault
```

## Seguridad

- Los elementos bloqueados y los cifrados de extremo a extremo nunca se entregan a vaultd.
- El token del equipo se guarda con permisos 0600; en CI puedes pasarlo con `VAULTD_TOKEN` y no se escribe nada en disco.
- `inject -o` escribe archivos que solo puedes leer tú.
- El agente SSH es de solo lectura y guarda las claves privadas solo en memoria; en el modo cada uso, cada firma se aprueba en Vault.
- Cada lectura queda en el registro de actividad del vault.

## Verificar una descarga

Cada versión incluye `SHA256SUMS.txt`:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Idioma

vaultd habla español, inglés, alemán, francés, italiano y portugués (según `LANG`, o fuérzalo con `VAULTD_LANG=es`).
