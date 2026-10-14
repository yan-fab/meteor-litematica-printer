# Meteor Litematica Printer (Modernized & Continuous Port)

[![Minecraft 26.2](https://img.shields.io/badge/Minecraft-26.2-blue.svg)](https://minecraft.net/)
[![Meteor Client 26.2](https://img.shields.io/badge/Meteor%20Client-26.2-purple.svg)](https://meteorclient.com/)
[![Java 25](https://img.shields.io/badge/Java-25-orange.svg)](https://adoptium.net/)
[![Fabric Loader](https://img.shields.io/badge/Fabric-0.19.3+-lightgrey.svg)](https://fabricmc.net/)

Continuous port and maintenance of the **Meteor Litematica Printer** addon, updated for modern versions of **Minecraft** and **Meteor Client**.

This addon allows you to automatically and rapidly paste/print Litematica schematics in survival and creative modes using Meteor Client's placement engine and rotation utilities.

---

## 📥 Download & Installation

1. Download the latest `.jar` from the [Releases](https://github.com/yan-fab/meteor-litematica-printer/releases) tab.
2. Ensure you have the following mods in your `.minecraft/mods` folder:
   - **Fabric Loader** (0.19.3 or newer)
   - **Meteor Client** (matching your Minecraft version)
   - **Litematica** (and **MaLiLib**)
3. Place the `meteor-litematica-printer-<version>.jar` file into your `mods/` directory.
4. Launch the game. The **Printer** module will be available in Meteor Client's GUI (default keybind: `Right Shift`).

---

## 📋 Compatibility Table

| Mod Version | Minecraft Version | Meteor Client Version | Java | Status |
|---|---|---|---|---|
| **v1.4.2** | **26.2** | **26.2-SNAPSHOT (#35)** | Java 25 | ✅ Stable |
| **v1.4.1** | 26.1.2 | 26.1.2-SNAPSHOT | Java 25 | ✅ Archived |
| **v1.4.0** | 1.21.x | 0.5.9+ | Java 21 | Legacy |

---

## 🛠️ Developer Guide: How to Update for Future Versions

This repository is configured to easily integrate and compile future Minecraft and Meteor Client releases. Follow the steps below whenever a new version drops:

### 1. Check Available Versions
- **Minecraft:** Check the latest releases in the [Mojang Version Manifest](https://piston-meta.mojang.com/mc/game/version_manifest_v2.json).
- **Meteor Client:** Check the latest artifacts on [Meteor Maven](https://maven.meteordev.org/snapshots/meteordevelopment/meteor-client/maven-metadata.xml) or the official website [meteorclient.com](https://meteorclient.com).

### 2. Update Configuration Files

#### `gradle.properties`
Update the target Minecraft version and Fabric Loader:
```properties
minecraft_version=<NEW_MC_VERSION>     # e.g., 26.3
loader_version=<LOADER_VERSION>        # e.g., 0.19.5
loom_version=1.17-SNAPSHOT             # Or latest loom version
mod_version=<NEXT_MOD_VERSION>         # e.g., 1.4.3
```

#### `build.gradle`
Update the Meteor Client dependency:
```groovy
dependencies {
    minecraft "com.mojang:minecraft:${project.minecraft_version}"
    implementation "net.fabricmc:fabric-loader:${project.loader_version}"

    // Meteor Client
    implementation "meteordevelopment:meteor-client:<NEW_MC_VERSION>-SNAPSHOT"

    implementation fileTree(dir: 'libs', include: '*.jar')
}
```

> **Note on Minecraft 26+ (Unobfuscated):** Starting with the 26.x series, Minecraft is natively distributed without code obfuscation. Do not use legacy `mappings loom.officialMojangMappings()` or the old `fabric-loom` plugin ID. Always use `net.fabricmc.fabric-loom` and standard `implementation` / `compileOnly` scopes.

### 3. Build the Mod
Run the following command in the project directory:
```bash
./gradlew clean build
```
*(Gradle will automatically download and configure the required JDK via the Foojay Toolchain Resolver).*

The compiled binary will be generated in:
`build/libs/meteor-litematica-printer-<version>.jar`

### 4. Publish a New Release on GitHub
After compiling and testing:
```bash
# Stage and push changes
git add .
git commit -m "feat: update mod to minecraft <MC_VERSION> and meteor <MC_VERSION>"
git push origin main

# Create and push git tag
git tag v<MOD_VERSION>-mc<MC_VERSION>
git push origin v<MOD_VERSION>-mc<MC_VERSION>

# Create GitHub release with the compiled JAR attached
gh release create v<MOD_VERSION>-mc<MC_VERSION> build/libs/meteor-litematica-printer-<version>.jar --title "Meteor Litematica Printer for Minecraft <MC_VERSION>" --notes "Updated and tested for Minecraft <MC_VERSION> and Meteor Client <MC_VERSION>."
```

---

## 👥 Credits & Acknowledgments

- **Original Author:** [kkllffaa](https://github.com/kkllffaa/meteor-litematica-printer) / Avast
- **Meteor Client:** [MeteorDevelopment](https://github.com/MeteorDevelopment/meteor-client)
- **Litematica & MaLiLib:** [masa](https://github.com/maruohon) & [sakura-ryoko](https://github.com/sakura-ryoko)
- **Maintenance & Modern Port:** [yan-fab](https://github.com/yan-fab)
