# Migration to OpenRouter

## Summary of Changes

This document summarizes the changes made to switch from Moonshot AI to OpenRouter.

## Files Modified

### 1. `ai-writer.py` (formerly `kimi-writer.py`)
**Changes:**
- Updated API configuration to use OpenRouter
- Changed environment variable from `MOONSHOT_API_KEY` to `OPENROUTER_API_KEY`
- Base URL changed to `https://openrouter.ai/api/v1`
- Model name moved to easily configurable constant with examples
- Removed Moonshot-specific token estimation API call
- Simplified token estimation using character-based approximation
- Updated display messages to show selected model name

**Key changes:**
- Model name now read from environment variable
- Defaults to `anthropic/claude-3.5-sonnet` if not set
- Set via `.env` file for easy switching

### 2. `utils.py`
**Changes:**
- Updated system prompt to be model-agnostic (removed "Moonshot AI" references)
- Kept all tool definitions intact
- No changes to tool implementations

### 3. `README.md`
**Changes:**
- Updated title and description to mention OpenRouter
- Added section on model selection and configuration
- Updated API key setup instructions
- Added "Supported Models" section with popular examples
- Updated troubleshooting section
- Updated credits and technical details

### 4. New Files Created

#### `OPENROUTER_SETUP.md`
Complete setup guide including:
- Step-by-step OpenRouter configuration
- Model recommendations by use case
- Pricing information
- Troubleshooting guide
- Benefits of OpenRouter

#### `MIGRATION_NOTES.md` (this file)
Summary of all changes for reference

## How to Use

### Switch Models in 3 Steps:

1. **Get OpenRouter API key**: https://openrouter.ai/keys
2. **Create `.env` file**:
   ```bash
   OPENROUTER_API_KEY=your-key-here
   MODEL_NAME=anthropic/claude-3.5-sonnet
   ```
3. **Change model anytime**:
   Just edit `MODEL_NAME` in your `.env` file!

That's it! Run the script normally.

## What Stayed the Same

- All tool implementations (create_project, write_file, compress_context)
- Project structure and output format
- Recovery mode functionality
- Streaming interface
- Context compression logic
- Maximum iterations and token limits
- Command-line interface

## Backward Compatibility

The core functionality is identical. If you have existing context summaries from the Moonshot version, they should work fine in recovery mode.

## Testing Recommendations

1. Test with a simple prompt first:
   ```bash
   python kimi-writer.py "Write a 500-word short story about a robot"
   ```

2. Try different models to compare:
   - Claude 3.5 Sonnet (creative, follows instructions well)
   - GPT-4 Turbo (strong all-around)
   - Qwen 2.5 72B (open source alternative)

3. Check that files are created properly in `output/` directory

4. Test recovery mode with an existing context file

## Benefits of This Change

1. **Flexibility**: Easy to switch between any AI model
2. **Cost Optimization**: Try different models to find best price/performance
3. **Availability**: Automatic fallbacks if one model is down
4. **Single API Key**: Access to all models with one key
5. **Future-Proof**: New models automatically available

## Notes

- Token estimation is now approximate (character-based) since OpenRouter doesn't have a dedicated token counting endpoint
- Some models may not support all features (check OpenRouter docs)
- Pricing varies by model - check https://openrouter.ai/models
- The reasoning_content streaming feature was specific to kimi-k2-thinking and won't appear with other models (but won't cause errors)

## Questions?

See `OPENROUTER_SETUP.md` for detailed setup instructions and model recommendations.

