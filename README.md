# Meteor Litematica Printer (Port Modernizado & Contínuo)

[![Minecraft 26.2](https://img.shields.io/badge/Minecraft-26.2-blue.svg)](https://minecraft.net/)
[![Meteor Client 26.2](https://img.shields.io/badge/Meteor%20Client-26.2-purple.svg)](https://meteorclient.com/)
[![Java 25](https://img.shields.io/badge/Java-25-orange.svg)](https://adoptium.net/)
[![Fabric Loader](https://img.shields.io/badge/Fabric-0.19.3+-lightgrey.svg)](https://fabricmc.net/)

Port e manutenção contínua do addon **Meteor Litematica Printer**, atualizado para as versões modernas do **Minecraft** e **Meteor Client**. 

O addon permite posicionar esquemáticas do Litematica de forma automatizada e ultra-rápida utilizando as funcionalidades e utilitários do Meteor Client.

---

## 📥 Download & Instalação

1. Baixe o arquivo `.jar` mais recente na aba de [Releases](https://github.com/yan-fab/meteor-litematica-printer/releases).
2. Certifique-se de ter os seguintes mods na sua pasta `.minecraft/mods`:
   - **Fabric Loader** (0.19.3 ou superior)
   - **Meteor Client** (versão compatível com a sua versão do jogo)
   - **Litematica** (e **MaLiLib**)
3. Coloque o `.jar` do `meteor-litematica-printer` dentro da sua pasta `mods/`.
4. Inicie o jogo. O módulo **Printer** estará disponível no menu do Meteor (pressione a tecla do GUI do Meteor, padrão `Right Shift`).

---

## 📋 Tabela de Compatibilidade

| Versão do Mod | Versão do Minecraft | Versão do Meteor Client | Java | Status |
|---|---|---|---|---|
| **v1.4.2** | **26.2** | **26.2-SNAPSHOT (#35)** | Java 25 | ✅ Estável |
| **v1.4.1** | 26.1.2 | 26.1.2-SNAPSHOT | Java 25 | ✅ Arquivado |
| **v1.4.0** | 1.21.x | 0.5.9+ | Java 21 | Legado |

---

## 🛠️ Guia do Desenvolvedor: Como Atualizar para Novas Versões

Este repositório foi estruturado para permitir que novas versões do Minecraft e do Meteor Client sejam integradas com facilidade. Siga os passos abaixo sempre que uma nova versão sair:

### 1. Verificar as versões disponíveis
- **Minecraft:** Verifique a versão mais recente em [Mojang Version Manifest](https://piston-meta.mojang.com/mc/game/version_manifest_v2.json).
- **Meteor Client:** Verifique a versão mais recente publicada no [Maven do Meteor](https://maven.meteordev.org/snapshots/meteordevelopment/meteor-client/maven-metadata.xml) ou no site oficial [meteorclient.com](https://meteorclient.com).

### 2. Atualizar os arquivos de configuração

#### `gradle.properties`
Altere a versão do Minecraft e do Fabric Loader:
```properties
minecraft_version=<NOVA_VERSAO_MC>     # Exemplo: 26.3
loader_version=<VERSAO_LOADER>          # Exemplo: 0.19.5
loom_version=1.17-SNAPSHOT              # Ou versão mais recente do loom
mod_version=<PROXIMA_VERSAO>           # Exemplo: 1.4.3
```

#### `build.gradle`
Atualize a dependência do Meteor Client:
```groovy
dependencies {
    minecraft "com.mojang:minecraft:${project.minecraft_version}"
    implementation "net.fabricmc:fabric-loader:${project.loader_version}"

    // Meteor Client
    implementation "meteordevelopment:meteor-client:<NOVA_VERSAO_MC>-SNAPSHOT"

    implementation fileTree(dir: 'libs', include: '*.jar')
}
```

> **Nota sobre o Minecraft 26+ (Não-Ofuscado):** A partir da série 26.x, o Minecraft é distribuído nativamente sem ofuscação de código. Não utilize `mappings loom.officialMojangMappings()` nem o plugin legado `fabric-loom`. Use sempre `net.fabricmc.fabric-loom` e dependências com escopo padrão `implementation`.

### 3. Compilar o Mod
Execute no terminal da pasta do projeto:
```bash
./gradlew clean build
```
*(O Gradle baixará automaticamente o JDK correspondente via Foojay Toolchain Resolver).*

O arquivo compilado estará disponível na pasta:
`build/libs/meteor-litematica-printer-<versão>.jar`

### 4. Publicar nova Release no GitHub
Após compilar e testar:
```bash
# Salvar as alterações
git add .
git commit -m "feat: update mod to minecraft <VERSAO> and meteor <VERSAO>"
git push origin main

# Criar nova tag
git tag v<MOD_VERSION>-mc<MC_VERSION>
git push origin v<MOD_VERSION>-mc<MC_VERSION>

# Criar release via GitHub CLI com o binário
gh release create v<MOD_VERSION>-mc<MC_VERSION> build/libs/meteor-litematica-printer-<versao>.jar --title "Meteor Litematica Printer para <MC_VERSION>" --notes "Atualização para Minecraft <MC_VERSION> e Meteor Client <MC_VERSION>."
```

---

## 👥 Créditos & Agradecimentos

- **Autor Original:** [kkllffaa](https://github.com/kkllffaa/meteor-litematica-printer) / Avast
- **Meteor Client:** [MeteorDevelopment](https://github.com/MeteorDevelopment/meteor-client)
- **Litematica & MaLiLib:** [masa](https://github.com/maruohon) & [sakura-ryoko](https://github.com/sakura-ryoko)
- **Manutenção & Port Moderno:** [yan-fab](https://github.com/yan-fab)
