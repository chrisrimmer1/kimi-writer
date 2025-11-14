# Quick Start Guide

## Setup (First Time Only)

1. **Get API Key**: https://openrouter.ai/keys
2. **Create `.env` file**:
   ```bash
   echo "OPENROUTER_API_KEY=sk-or-v1-..." > .env
   echo "MODEL_NAME=anthropic/claude-3.5-sonnet" >> .env
   ```
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Run the Agent

```bash
python ai-writer.py "Create a sci-fi short story about time travel"
```

## Change Model (Optional)

Edit your `.env` file:

```bash
MODEL_NAME=openai/gpt-4-turbo  # ← Change this
```

### Popular Models

| Model | Use Case | Cost |
|-------|----------|------|
| `anthropic/claude-3.5-sonnet` | Best creative writing | Medium |
| `openai/gpt-4-turbo` | Strong all-around | Medium |
| `google/gemini-pro-1.5` | Long contexts | Low |
| `qwen/qwen-2.5-72b-instruct` | Budget-friendly | Low |
| `meta-llama/llama-3.1-70b-instruct` | Open source | Low |

Browse all models: https://openrouter.ai/models

## That's It!

The agent will:
1. ✅ Create a project folder
2. ✅ Write complete stories/chapters
3. ✅ Save everything to `output/`
4. ✅ Auto-compress context if needed
5. ✅ Stream output in real-time

## Need Help?

- **Full setup guide**: See `OPENROUTER_SETUP.md`
- **Migration info**: See `MIGRATION_NOTES.md`
- **Detailed README**: See `README.md`

