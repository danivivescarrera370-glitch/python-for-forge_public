# python-for-forge_public

A Python-based development workspace for building **Minecraft Forge** modifications using Python. This structure leverages a Python-to-Java language provider layer to tap into the Forge API ecosystem without writing native Java.

## Project Structure

```text
python-for-forge_public/
├── src/
│   └── pymod/
│       ├── __init__.py      # Main mod entry point and initialization
│       └── handlers/        # Custom event and command scripts
└── META-INF/
    └── mods.toml            # Forge mod configuration metadata
```

---

## Configuration (`mods.toml`)

Configure your `META-INF/mods.toml` file to point to your Python engine loader:

```toml
modLoader = "pyforge"
loaderVersion = "[1,)"
issueTrackerURL = "https://github.com"

[[mods]]
modId = "python_for_forge"
version = "1.0.0"
displayName = "Python for Forge Public"
description = "A development framework for executing Python modules inside the Forge JVM environment."
```

---

## Code Implementation (`__init__.py`)

Initialize your event structures and mod runtime logic within `src/pymod/__init__.py`:

```python
from pyforge.decorators import Mod, SubscribeEvent
from pyforge.events import PlayerLoggedInEvent
from pyforge.logger import get_logger

logger = get_logger("PythonForgePublic")

@Mod("python_for_forge")
class PythonForgePublic:
    def __init__(self):
        logger.info("Workspace 'python-for-forge_public' successfully loaded!")

    @SubscribeEvent
    def on_player_join(self, event: PlayerLoggedInEvent):
        player = event.get_player()
        logger.info(f"Detected login event for user: {player.get_name().getString()}")
```

---

## Deployment

1. **Prerequisites:** Install [Minecraft Forge](https://minecraftforge.net) along with the required compatibility bridge JAR file in your local environment.
2. **Setup:** Place the contents of the `python-for-forge_public` folder directly into your instance's `/mods` or development runtime subdirectory.
3. **Execution:** Launch the Forge profile. The engine will parse `mods.toml`, discover the script package, and spin up the Python runtime container.
