# python-for-forge_public

An unofficial (Neo)Forge port of [Fabric Language Kotlin](https://github.com/FabricMC/fabric-language-kotlin), built specifically to seamlessly execute Python scripting configurations and language adapters across modern **Forge** and **NeoForge** environments.

## Features

- **Multi-Loader Compatibility:** Native support for both legacy Forge and modern NeoForge ecosystems.
- **Upstream Alignment:** Ported components mirror the robust language adapter architecture found in [Fabric Language Kotlin](https://github.com/FabricMC/fabric-language-kotlin).
- **Embedded Runtimes:** Shipped with pre-configured language providers to execute non-Java scripting layers seamlessly on the JVM.

---

## Project Structure

```text
python-for-forge_public/
├── src/
│   └── pymod/
│       ├── __init__.py      # Script initialization entry point
│       └── adapters/        # NeoForge / Forge bridging adapters
└── META-INF/
    └── mods.toml            # Mod metadata and platform rules
```

---

## Configuration (`mods.toml`)

Configure `META-INF/mods.toml` to dynamically hook into the modern (Neo)Forge lifecycle layers:

```toml
modLoader = "javafml"        # Or "neoforge" depending on your target version
loaderVersion = "[1,)"
issueTrackerURL = "https://github.com"

[[mods]]
modId = "python_for_forge"
version = "1.0.0"
displayName = "Python for Forge"
description = "An unofficial (Neo)Forge port of Fabric Language Kotlin, delivering robust Python language adapter pipelines to modding workflows."
```

---

## Usage & Implementation

Implement your bootstrapping logic inside `src/pymod/__init__.py`. This lifecycle adapter mirrors upstream behavior while dispatching events correctly within (Neo)Forge environments:

```python
from pyforge.decorators import Mod, SubscribeEvent
from pyforge.events import PlayerLoggedInEvent
from pyforge.logger import get_logger

logger = get_logger("PythonForForge")

@Mod("python_for_forge")
class PythonForForgePort:
    def __init__(self):
        logger.info("Python for Forge Language Port successfully initialized.")

    @SubscribeEvent
    def on_player_join(self, event: PlayerLoggedInEvent):
        player_name = event.get_player().get_name().getString()
        logger.info(f"[Port Event] Handled login sequence for: {player_name}")
```

---

## Deploying

1. **Drop-in Dependency:** Place the compiled `python-for-forge_public` structure directly into your instance's `/mods` directory.
2. **Compatibility Layer:** Ensure your development environment has your chosen compatibility runtime (e.g., [Sinytra Connector](https://github.com/Sinytra/Connector) or similar bridge APIs) if you are cross-compiling or mapping multi-loader dependencies.
