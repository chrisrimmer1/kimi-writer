# Changelog

## [2.0.0] - OpenRouter Migration

### 🎉 Major Changes

**Renamed script from `kimi-writer.py` to `ai-writer.py`**
- More generic name reflecting multi-model support

**Switched from Moonshot AI to OpenRouter**
- Now supports any AI model available on OpenRouter
- Easy model switching via `.env` file configuration
- No code changes needed to switch models

### ✨ New Features

- **Environment-based model selection**: Set `MODEL_NAME` in `.env` file
- **Automatic fallback**: Defaults to Claude 3.5 Sonnet if `MODEL_NAME` not set
- **Comprehensive documentation**: Added multiple guides for setup and model selection

### 📝 Configuration Changes

**Before:**
```bash
# .env
MOONSHOT_API_KEY=your-key
MOONSHOT_BASE_URL=https://api.moonshot.ai/v1
```

**After:**
```bash
# .env
OPENROUTER_API_KEY=your-key
MODEL_NAME=anthropic/claude-3.5-sonnet
```

### 🔧 Technical Changes

- Removed Moonshot-specific token counting API call
- Simplified token estimation using character-based calculation
- Updated system prompt to be model-agnostic
- Model name now loaded from environment variable

### 📚 New Documentation Files

1. **QUICK_START.md** - 30-second setup guide
2. **OPENROUTER_SETUP.md** - Complete OpenRouter configuration guide
3. **MODEL_RECOMMENDATIONS.md** - Detailed model comparisons by genre/use case
4. **MIGRATION_NOTES.md** - Summary of all changes
5. **env.example** - Example environment file with model options

### ✅ What Stayed the Same

- All core functionality (streaming, context compression, recovery mode)
- Tool implementations (create_project, write_file, compress_context)
- Project structure and output format
- Command-line interface
- Iteration limits and token thresholds

### 🚀 Upgrade Guide

1. Get OpenRouter API key: https://openrouter.ai/keys
2. Update your `.env` file:
   ```bash
   # Replace MOONSHOT_API_KEY with OPENROUTER_API_KEY
   OPENROUTER_API_KEY=your-new-key-here
   
   # Add MODEL_NAME (optional - defaults to Claude 3.5 Sonnet)
   MODEL_NAME=anthropic/claude-3.5-sonnet
   ```
3. Run as normal - no other changes needed!

### 🎯 Benefits

- ✅ **100+ models available** - Claude, GPT-4, Gemini, Llama, and more
- ✅ **One API key** - Access all models with single key
- ✅ **Easy switching** - Change models by editing one line
- ✅ **Cost optimization** - Try different models to find best value
- ✅ **Future-proof** - New models automatically available

### 📊 Recommended Models

**For Creative Writing:**
- `anthropic/claude-3.5-sonnet` (Best quality)
- `openai/gpt-4-turbo` (Strong dialogue)
- `qwen/qwen-2.5-72b-instruct` (Budget-friendly)

**For Long Contexts:**
- `google/gemini-pro-1.5` (1M token context)

**For Experimentation:**
- `meta-llama/llama-3.1-70b-instruct` (Open source)
- `mistralai/mixtral-8x7b-instruct` (Fast and cheap)

See `MODEL_RECOMMENDATIONS.md` for detailed comparisons.

### 🐛 Bug Fixes

- Fixed potential issues with token counting on different APIs
- Improved error messages for missing API keys
- Better handling of model-specific features

### ⚠️ Breaking Changes

**Environment Variables:**
- `MOONSHOT_API_KEY` → `OPENROUTER_API_KEY` (required)
- `MOONSHOT_BASE_URL` → removed (OpenRouter URL hardcoded)
- `MODEL_NAME` → new (optional, defaults to Claude 3.5 Sonnet)

**API Endpoint:**
- Now uses `https://openrouter.ai/api/v1`

### 🔄 Backward Compatibility

- Existing context summaries should work in recovery mode
- Output format unchanged
- All command-line options preserved

### 📖 Documentation Updates

- **README.md** - Updated with OpenRouter instructions
- **QUICK_START.md** - New quick setup guide
- **OPENROUTER_SETUP.md** - Comprehensive setup guide
- **MODEL_RECOMMENDATIONS.md** - Model selection guide
- **MIGRATION_NOTES.md** - Technical migration details
- **env.example** - Updated example environment file

---

## [1.0.0] - Initial Release

- Autonomous creative writing agent
- Powered by Moonshot AI's kimi-k2-thinking model
- Real-time streaming of reasoning and content
- Automatic context compression
- Recovery mode for interrupted sessions
- Tool system for project and file management

