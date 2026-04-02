# OpenClaw Image Generation Setup

Created by **Komputer Mechanic**  
Website: <https://komputermechanic.com/>

This repo is built around a single installer script:

- `install-image-generation.sh`

The script is interactive and currently supports three main flows:
- **Fresh setup** — configure image generation from scratch
- **Switch model** — change the currently selected fal.ai model
- **Uninstall** — remove image generation settings and optionally remove API keys

## What the script can configure

### Providers
- **OpenAI** using `gpt-image-1`
- **fal.ai** using a selectable fal model
- **Both** with a primary + fallback setup

### fal.ai model options
The script currently offers these fal.ai models:

**Generate only:**
- FLUX.1 Dev (`fal-ai/flux/dev`)
- FLUX.1 Schnell (`fal-ai/flux/schnell`)
- FLUX.1.1 Pro (`fal-ai/flux-pro/v1.1`)
- FLUX.2 Flex (`fal-ai/flux-2-flex`)

**Generate + Edit:**
- FLUX.2 Pro (`fal-ai/flux-2-pro`)
- Nano Banana 2 (`fal-ai/nano-banana-2`)
- Nano Banana Pro (`fal-ai/nano-banana-pro`)

## What the script does

Depending on the path you choose, the script can:
- check that OpenClaw is installed
- ensure `~/.openclaw/.env` exists
- collect and store `OPENAI_API_KEY`
- collect and store `FAL_KEY`
- update `~/.openclaw/openclaw.json`
- create or update the `fal_image` skill at:
  - `~/.openclaw/skills/fal-image/SKILL.md`
- restart OpenClaw Gateway
- remove image generation config during uninstall
- optionally remove API keys during uninstall

## Run it

### Cautious path

```bash
wget -O install-image-generation.sh https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh
bash install-image-generation.sh
```

### Fast path

```bash
curl -fsSL https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh | bash
```

## What users should expect

At the beginning, the script shows a disclaimer and asks whether to continue.

Then it lets the user choose one of these actions:
- fresh setup
- switch model
- uninstall

### Fresh setup
The script can:
- configure OpenAI only
- configure fal.ai only
- configure both with primary + fallback

If fal.ai is selected, it also asks which fal model to use.

### Switch model
The script:
- reads the current image generation model
- lets the user choose a new fal model
- updates `openclaw.json`
- rebuilds the `fal_image` skill
- restarts OpenClaw Gateway

### Uninstall
The script can:
- remove `imageGenerationModel` from `openclaw.json`
- delete the `fal-image` skill folder
- optionally remove `FAL_KEY`
- optionally remove `OPENAI_API_KEY`
- restart OpenClaw Gateway

## OpenClaw agent prompt example

```text
Help me set up image generation for OpenClaw using this GitHub repo:

https://github.com/komputermechanic/openclaw-image-generation

Guide me step by step. If needed, tell me to run the install script from the repo.
```

## Notes

- The repo is intentionally centered on the single installer script.
- If fal.ai is configured, the script intentionally creates a custom `fal_image` skill.
- Some fal.ai models in the script support **generation only**, while others support **generation and editing**.
