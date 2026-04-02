# FAL Image Generation Setup for OpenClaw

This package is for **agent-assisted setup**.

The goal is to enable OpenClaw image generation with FAL while keeping the API key out of chat.

## What must be true for this to work

Two things are required:

1. OpenClaw config must include:

```json5
{
  agents: {
    defaults: {
      imageGenerationModel: "fal/fal-ai/flux/dev"
    }
  }
}
```

2. The **running OpenClaw process** must have `FAL_KEY` in its environment.

That second part is critical.
It is not enough to write the key to an arbitrary file unless the running OpenClaw process actually loads that file.

## Recommended user prompt

```text
Help me set up FAL image generation for OpenClaw on this machine using this GitHub repo.

First discover where the active OpenClaw config file is stored and how the running OpenClaw process gets environment variables.
Do not ask me to paste my FAL API key into chat.
Instead, tell me the exact local terminal command I should run so I can store the key securely outside chat.
Back up any config before changing it, apply the minimum necessary changes, make sure the running OpenClaw process actually receives FAL_KEY, and then verify the setup.
```

## Local credential step

The agent should pass an explicit destination file path to the credential script.

Example:

```bash
FAL_ENV_FILE=/path/to/runtime/env-file bash scripts/configure-fal-credentials.sh
```

## Important note

This package does **not** assume one universal env file path.
The agent must first discover how this specific OpenClaw deployment is run.

Examples could include:
- shell-based startup
- service-managed startup
- systemd environment files
- other deployment-specific env loading
