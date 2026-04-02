---
name: fal-image-generation-setup
description: Set up FAL image generation for OpenClaw in an agent-assisted way. Use when the user wants to enable the built-in image_generate tool with fal, configure imageGenerationModel, locate the active OpenClaw config and runtime environment source, and keep the FAL API key out of chat by storing it through a local terminal step.
---

# FAL Image Generation Setup

Created by **Komputer Mechanic**  
Website: <https://komputermechanic.com/>

Use this package when a user wants to enable FAL-based image generation in OpenClaw.

## Core workflow

1. Discover the active OpenClaw config file.
2. Discover how the running OpenClaw process receives environment variables.
3. Back up files before editing.
4. Patch the minimum OpenClaw config needed to set `imageGenerationModel` to `fal/fal-ai/flux/dev`.
5. Tell the user to run the credential script locally in the terminal with an explicit destination path.
6. Ensure the runtime environment source used by OpenClaw actually provides `FAL_KEY` to the running process.
7. Restart OpenClaw if required.
8. Verify that image generation is available.

## Critical requirement

Writing `FAL_KEY` to a file is not enough by itself.
The running OpenClaw process must actually load that value into its environment.

## Safety rules

- Never ask the user to paste `FAL_KEY` into chat.
- Prefer explicit file paths over guessing.
- Back up config before changing it.
- Apply the smallest possible patch.
- Explain what changed after setup.

## References

- Read `references/agent-playbook.md` for the agent setup flow.
