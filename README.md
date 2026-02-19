# Simple LLM Chat CLI (`slcc`)

A simple CLI program, `slcc`, to chat with multiple LLM providers 
(e.g., ChatGPT and Claude) through a unified interface.

## Features

- Support for ChatGPT (OpenAI) and Claude (Anthropic)
- Conversation history maintained throughout the session

## Prerequisites

Have an API key for ChatGPT or Claude and that the keys are exported 
as environment variables `OPENAI_API_KEY` or `ANTHROPIC_API_KEYi`. 

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

## Usage

```bash
slcc -p claude
# or below
slcc --provider claude
```

Specify a custom model:
```bash
slcc --provider chatgpt --model gpt-5-mini
slcc --provider claude --model claude-sonnet-4-5
```

Adjust maximum tokens:
```bash
slcc --provider chatgpt --max-tokens 2048
```

### Command-Line Options

```bash
slcc -h
```

Options:
- `-p, --provider` (required): Choose provider (`chatgpt` or `claude`)
- `-m, --model` (optional): Specify model name (uses provider default if not specified)
- `--max-tokens` (optional): Maximum tokens in response (default: 1024)

### During Conversation

- Type your prompts and press Enter to send
- Type `exit` or `quit` to end the conversation
- Press Ctrl+C to interrupt the conversation
