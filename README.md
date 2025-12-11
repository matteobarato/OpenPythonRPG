# OpenEscordia

NOTE: Escordia is still a WIP and it is currently on the earliest stages of development. There is still a lot to do until a stable beta. Keep an eye on the project while I keep pushing updates! (⌒_⌒;)

<p align="center">
  <img src="https://github.com/rodmarkun/OpenEscordia/assets/75074498/7980cfc1-d582-4b99-8382-236b2ee5bc7e" width="500" />
</p>

## What is OpenEscordia?

OpenEscordia is a free, modular, open-source RPG building tool with AI integrations. It enables developers to create fully-fledged RPG games with ease and flexibility. The core of OpenEscordia revolves around **Modules**, which represent entire RPG games. The OpenEscordia engine loads these modules and instantly prepares them for gameplay.

### Key Features

- **Modular Design**: Developers define **actions**, **environments**, and **entities** using JSON files. These files are loaded by the engine and drive gameplay.
- **AI Integrations**: Effortlessly create engaging narratives with AI. The repository includes an AI helper script to generate NPC/dialogue content for entities.
- **Plugin System**: Extend functionality with **Plugins**. The sample module demonstrates plugins for inventory, combat, dialogue, gear, shops, spells, and dungeons.
- **Versatile Interfaces**: Choose the best interface for your game. OpenEscordia ships with a console interface and a Discord bot interface. The engine handles the intermediary logic so you can focus on game content.

### Repository layout (high level)

- modules/basic_escordia/ — sample module used by the engine (actions, environments, entities and plugins)
- interfaces/console_interface.py — simple text console interface entrypoint
- interfaces/discord/discord_manager.py — Discord bot implementation (provides a `!start` command)
- ai_generation.py — helper script to generate or update entity prompts/texts using Runpod or OpenAI
- main.py — example console-run entrypoint that boots the engine and runs the console interface

### Getting Started

Prerequisites
- Python 3.8+ (project tested with 3.10)
- Install any required packages (e.g., discord.py, requests, openai) as needed for the interfaces you plan to use.

Run the sample console game
1. From the repository root, run:

   python main.py

   This uses the sample module at `modules/basic_escordia` and starts the console interface.

Run the Discord bot
1. Provide a Discord bot token. The bot code reads the token from the environment variable `DISCORD_TOKEN`:

   - On macOS / Linux: export DISCORD_TOKEN="your-token"
   - On Windows (PowerShell): $env:DISCORD_TOKEN = "your-token"

2. Start the bot by running the Discord manager script:

   python interfaces/discord/discord_manager.py

3. The bot exposes a `!start` command. When a user runs `!start` the bot creates a character for that Discord user and replies with a profile embed and an interactive view.

Notes about the Discord implementation
- The bot is initialized with full intents and sets a custom activity. It stores active characters in the in-memory `CHARACTERS` dict, keyed by Discord username.
- If a user already has a character, `!start` will inform them and show their profile instead of creating a new one.

AI-assisted entity generation (ai_generation.py)

The repository includes `ai_generation.py`, a helper script to generate or populate entity text fields (for example NPC dialogue) using an AI service. Important details:

- The script currently expects API keys / IDs to be provided directly in the file as the constants `RUNPOD_API_KEY`, `SERVERLESS_API_ID`, and `OPENAI_API_KEY`.
- ENTITY_DIR is set to `modules/basic_escordia/config/entities/` by default; the script processes JSON files in that directory.
- Two services are supported by the script: `runpod` (default) and `openai`. Choose the service by setting `service_choice = 'runpod'` or `'openai'` in the script's `__main__` section, or call `main(service='openai')`.

Usage summary:
1. Update the API constants in `ai_generation.py` or modify the script to read keys from environment variables.
2. Ensure entity JSON files in `modules/basic_escordia/config/entities/` contain fields with keys ending in `_prompt` to be processed.
3. Run the script:

   python ai_generation.py

Caveats & safety
- The AI script overwrites entity JSON files in place with the generated content; keep backups or use version control to prevent accidental data loss.
- Replace hard-coded API keys with environment variables or a secrets manager in production.

Contributing
- This project is early-stage. Contributions to plugins, interfaces, module examples, and AI tooling are welcome. Please open issues or PRs to discuss changes.

License
- This project is open source. See LICENSE for details.


OpenEscordia empowers you to create and host your own RPG games with minimal effort, offering a powerful and flexible platform for both beginners and experienced developers.
