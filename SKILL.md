---
name: openclaw-image-generation-setup
description: Set up OpenClaw image generation through a single interactive installer script. Use when the user wants to configure OpenAI image generation, fal.ai image generation, both with primary and fallback, switch fal.ai models later, or uninstall image generation settings. The installer can also create a custom fal_image skill for supported fal.ai workflows.
---

# OpenClaw Image Generation Setup

Created by **Komputer Mechanic**  
Website: <https://komputermechanic.com/>

Use the single installer script in this repo:

- `install-image-generation.sh`

## What the installer handles

The script supports:
- fresh setup
- model switching for fal.ai
- uninstall

It can:
- collect API keys
- update `.env`
- update `openclaw.json`
- create or update the `fal_image` skill
- restart OpenClaw Gateway

## fal.ai model support

The installer currently supports multiple fal.ai models, including generation-only models and generation+edit models.

## Important note

If fal.ai is selected, the script intentionally creates a custom `fal_image` skill under:

- `~/.openclaw/skills/fal-image/`
