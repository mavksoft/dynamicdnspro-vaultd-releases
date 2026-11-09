<p align="center">
  <img src="https://vault.dynamicdnspro.com/assets/brand/logo-128.png" alt="DynamicDNSPro Vault" width="96">
</p>

<h1 align="center">vaultd</h1>

<p align="center">A linha de comandos e o agente SSH do DynamicDNSPro Vault.<br>Segredos nos teus scripts, deploys e sessões SSH — nunca no código, no histórico ou no disco.</p>

<p align="center">
  <a href="https://vault.dynamicdnspro.com"><img src="https://img.shields.io/badge/website-vault.dynamicdnspro.com-1f6feb" alt="website"></a>
  <a href="https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dynamicdnspro-vaultd-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20%C2%B7%20Windows%20%C2%B7%20Linux-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <strong>🇵🇹 Português</strong></p>

> **Este repositório publica apenas as versões binárias oficiais** — o código-fonte é privado.

## Download

| Plataforma | Ficheiro | |
|---|---|---|
| **macOS** (Intel · Apple Silicon) | [vaultd-macos-universal.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-macos-universal.zip) | assinado com Developer ID e notarizado pela Apple |
| **Windows** x64 | [vaultd-windows-amd64.zip](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-windows-amd64.zip) | descomprime e adiciona a pasta ao PATH |
| **Linux** x64 | [vaultd-linux-amd64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-amd64.tar.gz) | extrai para /usr/local/bin |
| **Linux** ARM64 | [vaultd-linux-arm64.tar.gz](https://github.com/mavksoft/dynamicdnspro-vaultd-releases/releases/latest/download/vaultd-linux-arm64.tar.gz) | extrai para /usr/local/bin |

## Primeiros passos

Liga este computador. Mostra um código e abre o Vault no navegador; aprova-o com a tua palavra-passe e escolhe o modo:

```sh
vaultd login
```

- **Aprovar cada uso** — cada segredo que o vaultd ler é aprovado no Vault, como os agentes de IA.
- **Autorizar este equipamento** — o vaultd lê sem perguntar até o revogares em Definições › Programador.

## Utilização

```sh
vaultd search github                          # procura itens (nunca mostra segredos)
vaultd read "GitHub" --field user             # mostra um campo (por omissão a palavra-passe; também user, otp, url, notes…)
vaultd run --env DB_PASS=vault://123/pass -- ./deploy.sh   # executa um comando com segredos em variáveis de ambiente
vaultd inject -i config.tpl -o config.env     # preenche um modelo, por exemplo um .env ou um ficheiro de configuração
vaultd ssh-agent                              # agente SSH com as chaves guardadas no teu cofre
```

## Segurança

- Os itens bloqueados e os cifrados ponta a ponta nunca são entregues ao vaultd.
- O token do equipamento é guardado com permissões 0600; em CI podes passá-lo com `VAULTD_TOKEN` e nada é escrito no disco.
- `inject -o` escreve ficheiros que só tu podes ler.
- O agente SSH é só de leitura e mantém as chaves privadas apenas em memória; no modo cada uso, cada assinatura é aprovada no Vault.
- Cada leitura fica no registo de atividade do cofre.

## Verificar um download

Cada versão inclui `SHA256SUMS.txt`:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## Idioma

O vaultd fala português, inglês, espanhol, alemão, francês e italiano (a partir de `LANG`, ou força com `VAULTD_LANG=pt`).
