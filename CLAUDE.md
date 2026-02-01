# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Multi-model query tool for comparing responses from various LLM providers through AWS Bedrock. Sends the same prompt to multiple models in parallel and generates a markdown report comparing responses.

## Commands

```bash
# Run with inline prompt
python multi-model-query.py "Your prompt here"

# Run with prompt from file
python multi-model-query.py --file prompt.txt

# Custom output file
python multi-model-query.py "prompt" --output results.md

# Query specific models only
python multi-model-query.py "prompt" --models "Claude Opus 4.5" "DeepSeek V3.1"

# List available models
python multi-model-query.py --list-models

# Set max tokens (default: 8192)
python multi-model-query.py "prompt" --max-tokens 4096
```

## Architecture

Single-file tool using only Python standard library (no pip dependencies). Uses `concurrent.futures.ThreadPoolExecutor` to query all models in parallel.

**Model regions**: Most models run in `us-east-1`, but Qwen and DeepSeek models require `us-east-2`.

**Response handling**: Supports both direct text responses and reasoning/thinking model outputs (e.g., Kimi K2, MiniMax M2).

## Available Models

- **Anthropic**: Claude Opus 4.5, Sonnet 4.5, Haiku 4.5
- **OpenAI**: GPT OSS 120B
- **Qwen**: Qwen3 235B, Qwen3 Coder 480B (us-east-2)
- **Google**: Gemma 3 27B
- **NVIDIA**: Nemotron Nano 12B
- **Others**: Moonshot Kimi K2, MiniMax M2, DeepSeek V3.1 (us-east-2)

## Output Format

Generates markdown with:
1. Summary table (model, provider, status, time, tokens)
2. Full responses grouped by provider
