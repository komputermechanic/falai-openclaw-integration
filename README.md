# OpenClaw Image Generation Setup

Created by **Komputer Mechanic**
Website: <https://komputermechanic.com/>

This repo contains a single interactive installer script for adding image generation to OpenClaw:

- `install-image-generation.sh`

---

## What the script does

The script walks you through three possible actions:

| Option | Description |
|--------|-------------|
| **1) Fresh setup** | Configure image generation from scratch |
| **2) Switch model** | Change your current fal.ai model |
| **3) Uninstall** | Remove image generation from OpenClaw |

---

## Supported providers

### OpenAI
- Model: `gpt-image-1`
- Pricing: ~$0.17 / image
- Capability: generation only

### fal.ai
Choose from 7 models during setup:

**Generate only:**
| # | Model | Model ID | Notes |
|---|-------|----------|-------|
| 1 | FLUX.1 Dev | `fal-ai/flux/dev` | General use, ~$0.025/image |
| 2 | FLUX.1 Schnell | `fal-ai/flux/schnell` | Ultra fast, cheapest |
| 3 | FLUX.1.1 Pro | `fal-ai/flux-pro/v1.1` | Enhanced quality |
| 4 | FLUX.2 Flex | `fal-ai/flux-2-flex` | Fine control, typography |

**Generate + Edit:**
| # | Model | Model ID | Notes |
|---|-------|----------|-------|
| 5 | FLUX.2 Pro | `fal-ai/flux-2-pro` | Best photorealism, ~$0.03/image |
| 6 | Nano Banana 2 | `fal-ai/nano-banana-2` | Google, fast + edit |
| 7 | Nano Banana Pro | `fal-ai/nano-banana-pro` | Google, highest quality |

---

## What the script configures

Depending on the path chosen, the script will:

- Verify that OpenClaw is installed (`~/.openclaw/openclaw.json` must exist)
- Ensure `~/.openclaw/.env` exists
- Collect and save `OPENAI_API_KEY` (if OpenAI is selected)
- Collect and save `FAL_KEY` (if fal.ai is selected)
- Update `imageGenerationModel` in `~/.openclaw/openclaw.json`
- Create or update the `fal_image` skill at `~/.openclaw/skills/fal-image/SKILL.md`
- Restart OpenClaw Gateway

---

## Fresh setup flow

1. Choose provider: OpenAI only, fal.ai only, or both
2. If fal.ai: choose a model from the list above
3. If using an existing key: optionally replace it
4. If both providers: choose which is primary and which is fallback
5. Script updates `openclaw.json` and creates the `fal_image` skill
6. Gateway restarts automatically

---

## Switch model flow

1. Script shows your current model
2. Choose a new fal.ai model
3. `openclaw.json` is updated
4. `fal_image` skill is rebuilt for the new model
5. Gateway restarts automatically

---

## Uninstall flow

1. Removes `imageGenerationModel` from `openclaw.json`
2. Deletes `~/.openclaw/skills/fal-image/`
3. Optionally removes `FAL_KEY` from `.env`
4. Optionally removes `OPENAI_API_KEY` from `.env`
5. Gateway restarts automatically

---

## The fal_image skill

When fal.ai is configured, the script creates a `fal_image` skill your OpenClaw agent can use directly.

- **Generate-only models** (options 1–4): the skill supports image generation via a single curl POST to `https://queue.fal.run/{model-id}`
- **Generate + Edit models** (options 5–7): the skill supports both generation and editing via a second endpoint at `https://queue.fal.run/{model-id}/edit`

The skill instructs the agent to extract the image URL from the JSON response and return it to the user.

---

## How to run

### Cautious path (recommended)

```bash
wget -O install-image-generation.sh https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh
bash install-image-generation.sh
```

### Fast path

```bash
curl -fsSL https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh | bash
```

---

## OpenClaw agent prompt

After setup completes, the script gives you a message to send to your agent. Example for fresh setup:

```
Hey! I just configured a new image generation skill for you called fal_image.
The skill file is located at ~/.openclaw/skills/fal-image/SKILL.md

Please do the following:
1. Read the skill file at that location
2. Confirm you understand how to use it
3. Run a smoke test by generating this image:
   A futuristic African city skyline at sunset, cinematic lighting
4. Return the image URL to confirm everything is working
```

---

## Notes

- This repo is intentionally built around a single installer script
- The script checks for `openclaw.json` before proceeding — OpenClaw must be installed first
- Some fal.ai models support **generation only**; others support **generation and editing**
- If you already have API keys saved, the script will ask before replacing them

