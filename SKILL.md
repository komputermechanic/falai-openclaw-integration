---
name: openclaw-image-generation-setup
description: Install or manage image generation for OpenClaw. Use this when the user wants to set up image generation (OpenAI or fal.ai), switch their current fal.ai model, or uninstall image generation. The installer script handles API key collection, openclaw.json configuration, fal_image skill creation, and gateway restart.
---

# OpenClaw Image Generation Setup

Created by **Komputer Mechanic**
Website: <https://komputermechanic.com/>

## What this does

This skill installs, updates, or removes image generation support in OpenClaw via a single interactive script: `install-image-generation.sh`

---

## When to use this skill

Use this skill when the user says things like:
- "set up image generation"
- "I want to generate images with OpenClaw"
- "configure fal.ai for OpenClaw"
- "switch my fal.ai model"
- "uninstall image generation"
- "remove my image gen setup"

---

## How to help the user

Tell the user to run the installer script. Give them the cautious path:

```bash
wget -O install-image-generation.sh https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh
bash install-image-generation.sh
```

Or the fast path if they prefer:

```bash
curl -fsSL https://raw.githubusercontent.com/komputermechanic/openclaw-image-generation/main/install-image-generation.sh | bash
```

---

## What the script will ask the user

1. Whether to proceed (disclaimer shown first)
2. Which action: fresh setup, switch model, or uninstall
3. For fresh setup: which provider(s) — OpenAI, fal.ai, or both
4. For fal.ai: which model (7 options shown in the script)
5. API key(s) — entered securely, stored in `~/.openclaw/.env`
6. If both providers: which is primary and which is fallback

---

## Supported providers and models

**OpenAI**
- `gpt-image-1` — ~$0.17/image, generation only

**fal.ai — Generate only**
- FLUX.1 Dev (`fal-ai/flux/dev`) — ~$0.025/image
- FLUX.1 Schnell (`fal-ai/flux/schnell`) — cheapest, ultra fast
- FLUX.1.1 Pro (`fal-ai/flux-pro/v1.1`) — enhanced quality
- FLUX.2 Flex (`fal-ai/flux-2-flex`) — fine control, typography

**fal.ai — Generate + Edit**
- FLUX.2 Pro (`fal-ai/flux-2-pro`) — best photorealism, ~$0.03/image
- Nano Banana 2 (`fal-ai/nano-banana-2`) — Google, fast + edit
- Nano Banana Pro (`fal-ai/nano-banana-pro`) — Google, highest quality

---

## After setup

When setup completes, the script outputs a message for the user to send to their agent. The message tells the agent to:
1. Read the updated `fal_image` skill at `~/.openclaw/skills/fal-image/SKILL.md`
2. Confirm understanding
3. Run a smoke test (generate a test image)
4. Return the image URL

If the user pastes that message to you, follow those instructions exactly.

---

## Notes

- OpenClaw must already be installed before running this script
- The script checks for `~/.openclaw/openclaw.json` and exits if not found
- The `fal_image` skill is created automatically when fal.ai is selected
- Models 5–7 (FLUX.2 Pro, Nano Banana 2, Nano Banana Pro) support both generation and editing
- Models 1–4 support generation only

