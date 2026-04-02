# Agent playbook for FAL setup

Use this repo when the goal is to enable OpenClaw image generation through FAL.

## Discovery checklist

1. Locate the active OpenClaw config file.
2. Locate how the running OpenClaw process gets environment variables.
3. Back up both config and runtime env sources before editing.
4. Patch only the minimal image generation config needed.
5. Tell the user to run the credential script locally with an explicit env-file path.
6. Ensure that env-file path is actually loaded by the running OpenClaw process.
7. Restart OpenClaw only if needed.
8. Verify that image generation is available.

## Minimum config target

Set:

```json5
{
  agents: {
    defaults: {
      imageGenerationModel: "fal/fal-ai/flux/dev"
    }
  }
}
```

## Critical rule

Do not confuse:
- “a file containing `FAL_KEY`”
with:
- “the running OpenClaw process actually receiving `FAL_KEY` in its environment”

The second condition is what matters.

## Safety rules

- Never ask the user to paste `FAL_KEY` into chat.
- Prefer explicit file paths over guessing.
- Back up config before changing it.
- Apply the smallest possible patch.
- Explain what changed after setup.
