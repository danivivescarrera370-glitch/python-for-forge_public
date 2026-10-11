# python-for-forge_public

An unofficial **NeoForge** port of [Fabric Language Python](https://github.com/hellojaviergarcia/fabric-language-python_public/tree/main). This project delivers a high-performance language adapter pipeline, allowing developers to write fully-featured modifications for (Neo)Forge environments using native Python 3 syntax instead of traditional Java.

## Features

- **Multi-Loader Support:** Fully bridges the Python scripting layer across modern **Forge** and **NeoForge** ecosystems.
- **GraalVM Driven:** Powered by an embedded GraalVM container, removing any requirement for players to install Python natively on their local machines.
- **Full Engine Mapping:** Mirrors the original adapter's capacity to handle items, blocks, engine events, and native Mixins directly from Python scripts.

---

## Project Structure

```text
python-for-forge_public/
├── src/
│   └── pymod/
│       ├── __init__.py      # Main script entry point and hook registry
│       └── mixins/          # Mixin injection classes written in Python
└── META-INF/
    └── neoforge.mods.toml   # Forge/NeoForge mod metadata configuration
```

---

## Configuration (`neoforge.mods.toml`)

This `META-INF/neoforge.mods.toml` maps your Python scripts to the modern (Neo)Forge FML ecosystem:

```toml
modLoader = "javafml"
loaderVersion = "[1,)"
license = "MIT"
issueTrackerURL = "https://github.com"

[[mods]]
modId = "python_for_forge"
version = "1.0.0"
displayName = "Python for Forge"
description = "An unofficial NeoForge language provider port of Fabric Language Python. Write mods entirely using clean Python syntax."

[[dependencies.python_for_forge]]
modId = "minecraft"
type = "required"
versionRange = "[26.2,26.3)"
ordering = "NONE"
side = "BOTH"

[[dependencies.python_for_forge]]
modId = "neoforge"
type = "required"
versionRange = "*"
ordering = "NONE"
side = "BOTH"
```

---

## Quick Start Template (`__init__.py`)

This boilerplate registers components and listens to lifecycle hooks inside your Python environment:

```python
from pyforge.decorators import Mod, SubscribeEvent, Mixin
from pyforge.events import PlayerLoggedInEvent
from pyforge.logger import get_logger

logger = get_logger("PythonForForge")

@Mod("python_for_forge")
class PythonForForgePort:
    def __init__(self):
        logger.info("Python for Forge language adapter initialized.")

    @SubscribeEvent
    def on_player_join(self, event: PlayerLoggedInEvent):
        player_name = event.get_player().get_name().getString()
        logger.info(f"[Python for Forge] Logged user entry: {player_name}")
```

---

## Deployment & Setup

1. **Workspace Sync:** Ensure your codebase matches the root directory name `python-for-forge_public`.
2. **Installation:** Place the built `python-for-forge_public` mod folder directly inside your targeted instance's `.minecraft/mods/` directory.
3. **Execution:** Launch Minecraft through your configured Forge or NeoForge game profile. The engine parses the language adapter metadata and safely runs the script containers.
