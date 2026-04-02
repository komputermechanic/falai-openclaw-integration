# Agent playbook for FAL setup

Use the simple three-step setup flow:

1. Tell the user to replace the placeholder with their real FAL API key and add `FAL_KEY` to `~/.bashrc`
2. Tell the user to patch `/root/.openclaw/openclaw.json`
3. Tell the user to run `openclaw gateway restart`

Target config:

```json
{
  "agents": {
    "defaults": {
      "imageGenerationModel": "fal/fal-ai/flux/dev"
    }
  }
}
```
