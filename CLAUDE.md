# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kimi Writing Agent is an autonomous agent for creative writing tasks powered by OpenRouter (supporting multiple AI models). The agent operates in an agentic loop with up to 300 iterations, using real-time streaming for reasoning, content generation, and tool execution.

## Development Commands

### Running the Agent

```bash
# Fresh start with inline prompt
uv run ai-writer.py "Create a collection of 5 sci-fi short stories about AI"
# or: python ai-writer.py "Create a collection of 5 sci-fi short stories about AI"

# Interactive mode
uv run ai-writer.py
# or: python ai-writer.py

# Recovery mode (continue from saved context)
uv run ai-writer.py --recover output/my_project/.context_summary_20250107_143022.md
# or: python ai-writer.py --recover output/my_project/.context_summary_20250107_143022.md
```

### Setup

```bash
# Install dependencies using uv (recommended)
uv pip install -r requirements.txt

# Or using pip
pip install -r requirements.txt

# Configure API key and model
cp env.example .env
# Edit .env and add:
# OPENROUTER_API_KEY=your-api-key-here
# MODEL_NAME=anthropic/claude-3.5-sonnet
```

## Architecture

### Core Components

**ai-writer.py** (main agent loop):
- Manages the agentic iteration loop (max 300 iterations)
- Handles streaming responses with separate streams for reasoning_content, content, and tool_calls
- Implements automatic context compression at 180K tokens (90% of 200K limit)
- Creates periodic backups every 50 iterations
- Supports recovery mode from context summaries
- Real-time token monitoring using character-based estimation (~4 chars per token)

**utils.py**:
- `estimate_token_count()`: Legacy function (no longer used with OpenRouter)
- `get_tool_definitions()`: Returns OpenAI-compatible tool definitions
- `get_tool_map()`: Maps tool names to implementation functions
- `get_system_prompt()`: Returns the agent's system prompt with writing guidelines

**tools/** (agent tools):
- `project.py`: Manages project folder creation in `output/` directory. Maintains global state for active project folder.
- `writer.py`: Writes markdown files with three modes: create (fail if exists), append, overwrite
- `compression.py`: Compresses conversation history by summarizing older messages, saves timestamped summaries

### Key Architecture Patterns

**Streaming Response Handling** (ai-writer.py:306-380):
- Accumulates chunks from three separate streams: reasoning_content, content, and tool_calls
- Shows real-time progress indicators for large tool arguments (every 500 chars)
- Reconstructs message object after streaming completes
- Must preserve reasoning_content in message history for proper context

**Message Conversion** (ai-writer.py:119-168):
- Converts between OpenAI message objects and dictionaries
- Critical: Must preserve `reasoning_content` field when converting messages
- Handles tool_calls, tool_call_id, and name fields appropriately

**Token Management**:
- Context limit: 200,000 tokens
- Auto-compression threshold: 180,000 tokens (90%)
- Uses character-based estimation (~4 chars per token)
- Messages must be serialized properly (utils.py:26-49) for token counting

**Context Compression Strategy** (compression.py:48-159):
- Keeps system message and N most recent messages intact (default 10)
- Summarizes middle messages using the configured AI model
- Saves summaries to `.context_summary_TIMESTAMP.md` files in project folder
- Injects summary as a user message with special formatting

**Global State Management**:
- Active project folder stored in `tools/project.py:_active_project_folder`
- Set by `create_project_impl()`, used by `write_file_impl()`
- Agent must call `create_project` before `write_file`

### Model Configuration

- API: OpenRouter (`https://openrouter.ai/api/v1`)
- Model: Configurable via `MODEL_NAME` env var (defaults to `anthropic/claude-3.5-sonnet`)
- Temperature: 1.0
- Max tokens per call: 65,536 (64K)
- Supports 100+ models via OpenRouter

### Tool Design Philosophy

The agent has minimal tools to encourage autonomous behavior:
1. `create_project`: Initializes workspace (one project at a time)
2. `write_file`: Creates/modifies files with explicit modes
3. `compress_context`: Internal tool, auto-called by system (agent shouldn't manually invoke)

The system prompt (utils.py:154-192) emphasizes writing complete, substantial content (short stories: 3000-10000 words, chapters: 2000-5000 words minimum).

### Output Structure

All generated projects go in `output/` directory:
```
output/
├── project_name/
│   ├── chapter_01.md           # Agent-written content
│   ├── chapter_02.md
│   └── .context_summary_*.md   # Auto-saved context summaries
```

## Error Handling

**Graceful Interruption** (ai-writer.py:486-502):
- `Ctrl+C` triggers context save before exit
- Displays recovery command for resuming work

**Iteration Limit** (ai-writer.py:510-529):
- Saves final context when hitting MAX_ITERATIONS (300)
- Provides recovery instructions

**API Errors**:
- Token estimation failures are non-fatal (ai-writer.py:260-262)
- Per-iteration errors logged but loop continues (ai-writer.py:504-507)

## Important Implementation Details

### Message History Format

Messages must maintain this structure:
```python
{
    "role": "assistant",
    "content": "...",           # Optional
    "reasoning_content": "...", # Optional (some models like o1 provide this)
    "tool_calls": [...]         # Optional
}
```

### Tool Call Structure

When streaming tool calls (ai-writer.py:343-380):
- Tool calls arrive incrementally by index
- Must accumulate arguments string across chunks
- Progress indicators show every 500 characters to avoid spam
- Final structure matches OpenAI format with id, type, function.name, function.arguments

### Recovery Mode

When `--recover` is used:
- Context loaded from summary file
- Wrapped in `[RECOVERED CONTEXT]` markers
- Injected as user message with instruction to continue

## Dependencies

- `openai>=1.0.0`: Client for API calls (OpenAI-compatible, works with OpenRouter)
- `httpx>=0.24.0`: For direct token estimation API calls
- `python-dotenv>=1.0.0`: Environment variable management
