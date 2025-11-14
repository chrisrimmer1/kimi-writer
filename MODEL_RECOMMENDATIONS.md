# Model Recommendations for Creative Writing

## Quick Comparison Table

| Model | Speed | Quality | Cost | Context | Best For |
|-------|-------|---------|------|---------|----------|
| `anthropic/claude-3.5-sonnet` | Fast | ⭐⭐⭐⭐⭐ | $$ | 200K | Creative writing, novels |
| `anthropic/claude-3-opus` | Slow | ⭐⭐⭐⭐⭐ | $$$ | 200K | Technical precision |
| `openai/gpt-4-turbo` | Fast | ⭐⭐⭐⭐ | $$ | 128K | All-around, dialogue |
| `openai/gpt-4o` | Very Fast | ⭐⭐⭐⭐ | $$ | 128K | Fast creative writing |
| `google/gemini-pro-1.5` | Fast | ⭐⭐⭐⭐ | $ | 1M | Very long contexts |
| `google/gemini-flash-1.5` | Very Fast | ⭐⭐⭐ | $ | 1M | Quick drafts |
| `qwen/qwen-2.5-72b-instruct` | Fast | ⭐⭐⭐⭐ | $ | 32K | Budget-friendly quality |
| `meta-llama/llama-3.1-70b-instruct` | Medium | ⭐⭐⭐ | $ | 128K | Open source |
| `mistralai/mixtral-8x7b-instruct` | Fast | ⭐⭐⭐ | $ | 32K | Fast, budget-friendly |

**Cost Scale:** $ (cheap) to $$$ (expensive)

## Detailed Recommendations

### 🏆 Best Overall: Claude 3.5 Sonnet
```python
MODEL_NAME = "anthropic/claude-3.5-sonnet"
```

**Pros:**
- Excellent prose quality and creativity
- Great at following complex instructions
- Strong character development
- Natural dialogue
- Good reasoning abilities for plot structure

**Cons:**
- Medium cost ($3-5 per million tokens)
- Occasionally verbose

**Use for:** Novels, short stories, creative fiction, character-driven narratives

---

### 💪 Most Powerful: Claude 3 Opus
```python
MODEL_NAME = "anthropic/claude-3-opus"
```

**Pros:**
- Highest quality output
- Best reasoning and planning
- Excellent for complex narratives
- Superior at maintaining consistency

**Cons:**
- Most expensive option
- Slower than other models

**Use for:** High-quality novels, complex plots, literary fiction

---

### ⚡ Best Speed/Quality: GPT-4 Turbo
```python
MODEL_NAME = "openai/gpt-4-turbo"
```

**Pros:**
- Fast generation
- Strong creative writing
- Excellent dialogue
- Good at various genres

**Cons:**
- Can be repetitive
- Sometimes needs more guidance

**Use for:** Fast drafting, dialogue-heavy stories, genre fiction

---

### 💰 Best Value: Qwen 2.5 72B
```python
MODEL_NAME = "qwen/qwen-2.5-72b-instruct"
```

**Pros:**
- Very affordable
- Surprisingly good quality
- Strong reasoning
- Fast generation

**Cons:**
- Slightly less creative than Claude/GPT-4
- May need more prompt engineering

**Use for:** Budget projects, drafting, experimental writing

---

### 📚 Best for Long Stories: Gemini Pro 1.5
```python
MODEL_NAME = "google/gemini-pro-1.5"
```

**Pros:**
- Massive 1M token context
- Good at maintaining consistency across long narratives
- Affordable
- Fast

**Cons:**
- Sometimes less creative than Claude
- May produce more formulaic writing

**Use for:** Very long novels, epic series, interconnected story collections

---

## By Genre

### Science Fiction
1. **Claude 3.5 Sonnet** - Best worldbuilding and concepts
2. **GPT-4 Turbo** - Great for hard sci-fi technical details
3. **Qwen 2.5 72B** - Good budget option

### Fantasy
1. **Claude 3.5 Sonnet** - Excellent descriptive prose
2. **Claude 3 Opus** - Best for complex magic systems
3. **GPT-4 Turbo** - Good for action sequences

### Romance
1. **Claude 3.5 Sonnet** - Natural character chemistry
2. **GPT-4 Turbo** - Excellent dialogue
3. **Gemini Pro 1.5** - Good for slow-burn narratives

### Mystery/Thriller
1. **Claude 3 Opus** - Best logical consistency
2. **Claude 3.5 Sonnet** - Great at twists
3. **GPT-4 Turbo** - Good pacing

### Literary Fiction
1. **Claude 3 Opus** - Most sophisticated prose
2. **Claude 3.5 Sonnet** - Excellent character depth
3. **GPT-4 Turbo** - Good for experimental styles

### Horror
1. **Claude 3.5 Sonnet** - Best atmosphere building
2. **GPT-4 Turbo** - Good tension pacing
3. **Qwen 2.5 72B** - Surprisingly effective

## By Project Type

### Short Stories (< 10K words)
**Recommended:** Claude 3.5 Sonnet or GPT-4 Turbo
- Quick generation
- High quality
- Good for complete stories in one session

### Novels (50K-100K words)
**Recommended:** Claude 3.5 Sonnet or Gemini Pro 1.5
- Claude for quality
- Gemini for longer context window
- Consider cost for longer projects

### Story Collections
**Recommended:** Qwen 2.5 72B or GPT-4o
- Generate multiple stories efficiently
- Balance quality and cost
- Fast iteration

### Experimental/Practice Writing
**Recommended:** Mistral 8x7B or Llama 3.1 70B
- Very affordable
- Fast feedback
- Good for learning and experimentation

## Cost Estimates

Approximate costs for typical projects (as of Nov 2024):

| Project Type | Tokens | Claude 3.5 | GPT-4 Turbo | Qwen 2.5 |
|--------------|--------|------------|-------------|----------|
| Short story (5K words) | ~50K | $0.15 | $0.10 | $0.02 |
| Novella (30K words) | ~300K | $0.90 | $0.60 | $0.12 |
| Novel (80K words) | ~800K | $2.40 | $1.60 | $0.32 |
| 10 short stories | ~500K | $1.50 | $1.00 | $0.20 |

*Note: Costs include both input and output tokens. Actual costs may vary.*

## How to Switch Models

1. Open your `.env` file
2. Add or change the `MODEL_NAME` line
3. Save and run

Example `.env` file:
```bash
OPENROUTER_API_KEY=sk-or-v1-abc123...
MODEL_NAME=anthropic/claude-3.5-sonnet  # Change this
```

## Testing Different Models

Try the same prompt with different models to compare:

```bash
# Test with Claude
# (Edit MODEL_NAME in .env to "anthropic/claude-3.5-sonnet" first)
python ai-writer.py "Write a 1000-word mystery short story"

# Test with GPT-4
# (Edit MODEL_NAME in .env to "openai/gpt-4-turbo" first)
python ai-writer.py "Write a 1000-word mystery short story"

# Test with Qwen
# (Edit MODEL_NAME in .env to "qwen/qwen-2.5-72b-instruct" first)
python ai-writer.py "Write a 1000-word mystery short story"
```

## Advanced Tips

### Mixing Models
Consider using different models for different stages:
1. **Planning/Outlining**: Use Claude 3 Opus (best reasoning)
2. **First Draft**: Use Qwen 2.5 72B (fast and cheap)
3. **Polish/Editing**: Use Claude 3.5 Sonnet (best prose)

### Token Optimization
- Longer context models (Gemini) can hold more story history
- Shorter context models may need more frequent compression
- Monitor the token counter during generation

### Temperature Settings
The script uses temperature=1.0 by default, which works well for creative writing. You can adjust this in `ai-writer.py` (search for `temperature=1.0`) for:
- More focused/consistent: 0.7-0.9
- More creative/varied: 1.0-1.2

## Need Help Choosing?

**Still not sure?** Start with **Claude 3.5 Sonnet** - it offers the best balance of quality, speed, and cost for most creative writing projects.

**On a budget?** Try **Qwen 2.5 72B** - you'll be surprised by the quality.

**Writing an epic series?** Use **Gemini Pro 1.5** for its massive context window.

## More Information

- Browse all models: https://openrouter.ai/models
- Check current pricing: https://openrouter.ai/models
- OpenRouter documentation: https://openrouter.ai/docs

