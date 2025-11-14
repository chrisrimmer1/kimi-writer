# OpenRouter Setup Guide

This project has been configured to use **OpenRouter**, which gives you access to multiple AI models through a single API.

## Quick Start

### 1. Get an OpenRouter API Key

1. Go to https://openrouter.ai/keys
2. Sign up or log in
3. Create a new API key
4. Copy your API key

### 2. Configure the API Key

Create a `.env` file in the project root:

```bash
echo "OPENROUTER_API_KEY=your-api-key-here" > .env
```

Or create it manually:

```env
# .env file
OPENROUTER_API_KEY=your-actual-api-key-here
```

### 3. Choose Your Model

Add the model name to your `.env` file:

```bash
# .env file
OPENROUTER_API_KEY=your-actual-api-key-here
MODEL_NAME=anthropic/claude-3.5-sonnet
```

**Popular options:**
```bash
# Claude models (excellent for creative writing)
MODEL_NAME=anthropic/claude-3.5-sonnet
MODEL_NAME=anthropic/claude-3-opus

# OpenAI models (strong all-around)
MODEL_NAME=openai/gpt-4-turbo
MODEL_NAME=openai/gpt-4o

# Google models
MODEL_NAME=google/gemini-pro-1.5
MODEL_NAME=google/gemini-flash-1.5

# Open source models (cheaper)
MODEL_NAME=meta-llama/llama-3.1-70b-instruct
MODEL_NAME=qwen/qwen-2.5-72b-instruct
MODEL_NAME=mistralai/mixtral-8x7b-instruct
```

**Note:** If you don't set `MODEL_NAME`, it defaults to `anthropic/claude-3.5-sonnet`

### 4. Run the Agent

```bash
python ai-writer.py "Create a sci-fi short story about AI"
```

## Switching Models

To change models, simply:

1. Open your `.env` file
2. Change the `MODEL_NAME` value
3. Save and run

**Example `.env` file:**
```bash
OPENROUTER_API_KEY=sk-or-v1-abc123...
MODEL_NAME=openai/gpt-4-turbo
```

**That's it!** No code changes needed.

## Finding Models

Browse all available models at: https://openrouter.ai/models

You can filter by:
- **Price** (some models are free!)
- **Context window** (how much text they can process)
- **Capabilities** (vision, function calling, etc.)

## Model Recommendations

### For Creative Writing
- **Best:** `anthropic/claude-3.5-sonnet` - Excellent prose, follows instructions well
- **Alternative:** `openai/gpt-4-turbo` - Very creative, good at dialogue
- **Budget:** `qwen/qwen-2.5-72b-instruct` - Strong performance, lower cost

### For Technical Writing
- **Best:** `anthropic/claude-3-opus` - Most accurate
- **Alternative:** `openai/gpt-4o` - Fast and accurate
- **Budget:** `meta-llama/llama-3.1-70b-instruct` - Open source

### For Experimentation
- **Fast:** `google/gemini-flash-1.5` - Very quick responses
- **Long context:** `google/gemini-pro-1.5` - Handles very long stories
- **Free tier:** Check OpenRouter for free models

## Costs

OpenRouter charges per-token based on the model you choose. Check pricing at:
https://openrouter.ai/models

Most models cost $0.50-$5 per million tokens. A typical 10-chapter novel might cost $0.50-$2.00.

## Troubleshooting

### "OPENROUTER_API_KEY environment variable not set"
- Make sure you created the `.env` file in the project root
- Check that the variable name is exactly `OPENROUTER_API_KEY`
- No quotes needed around the key in the `.env` file

### "401 Unauthorized"
- Verify your API key is correct
- Make sure you have credits on your OpenRouter account
- Check that your key hasn't expired

### Model-specific errors
- Some models may not support all features (like streaming or function calling)
- Try a different model if you encounter issues
- Check the model's documentation on OpenRouter

## Benefits of OpenRouter

1. **One API key** for all models
2. **Easy switching** between models
3. **Automatic fallbacks** if a model is down
4. **Usage tracking** and analytics
5. **Competitive pricing** with bulk discounts

## Original Configuration

This project was originally configured for Moonshot AI's kimi-k2-thinking model. The OpenRouter version maintains all functionality while adding flexibility.

**Key changes:**
- API endpoint changed to `https://openrouter.ai/api/v1`
- Environment variable changed to `OPENROUTER_API_KEY`
- Model name easily configurable at top of `kimi-writer.py`
- Token estimation simplified (no API-specific endpoint needed)

