# Simple LLM Chat CLI (`slcc`)

A simple CLI program, `slcc`, to chat with multiple LLM providers 
(e.g., ChatGPT and Claude) through a unified interface.

## Features

- Support for ChatGPT (OpenAI) and Claude (Anthropic)
- Conversation history maintained throughout the session

## Prerequisites

Have an API key for ChatGPT or Claude and that the keys are exported 
as environment variables `OPENAI_API_KEY` or `ANTHROPIC_API_KEYi`. 
For example, you can have 
`~/.api_key_openai_1`, and have below lines in your `~/.zshrc` or `~/.bashrc`.

```bash
# chatgpt
export OPENAI_API_KEY="$(cat $HOME/.api_key_openai_1 2>/dev/null || echo '')"

# claude
export ANTHROPIC_API_KEY="$(cat $HOME/.api_key_anthropic_1 2>/dev/null || echo '')"
```

## Installation

### Install with pipx

1. Install `pipx` if you don't have it. For more info, refer 
to [its documentation](https://pipx.pypa.io/stable/)

2. Install directly from GitHub:
```bash
pipx install git+https://github.com/quietlyecho/simple-llm-chat-cli.git
```

3. The `slcc` command is now available globally:
```bash
slcc --provider claude
```

### Updating and Uninstalling

To update:
```bash
pipx upgrade slcc
```

To uninstall:
```bash
pipx uninstall slcc
```

## Usage

```bash
slcc -p claude
# or below
slcc --provider claude
```

Specify a custom model:
```bash
slcc --provider chatgpt --model gpt-4o
slcc --provider claude --model claude-sonnet-4
```

Adjust maximum tokens:
```bash
slcc --provider chatgpt --max-tokens 2048
```

Adjust temperature (randomness):
```bash
slcc --provider chatgpt --temperature 0.7
slcc --provider claude --temperature 0.2  # More deterministic
slcc --provider chatgpt --temperature 1.0  # More creative
```

### Command-Line Options

```bash
slcc -h
```

Options:
- `-p, --provider` (required): Choose provider (`chatgpt` or `claude`)
- `-m, --model` (optional): Specify model name (uses provider default if not specified)
- `--max-tokens` (optional): Maximum tokens in response (default: 1024)
- `--temperature` (optional): Sampling temperature 0.0-1.0, higher is more random (default: 0.5)

### During Conversation

- Type your prompts and press Enter to send
- Type `exit` or `quit` to end the conversation
- Press Ctrl+C to interrupt the conversation

## Extending the System

To add a new LLM provider:

1. Create a new provider class in `src/providers/` that inherits from `LLMProvider`
2. Implement the required abstract methods: `send_message()` and `get_provider_name()`
3. Register the provider in `src/config.py` in the `ProviderFactory.PROVIDERS` dictionary
