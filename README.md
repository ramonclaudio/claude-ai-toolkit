# Claude AI Toolkit

> **Unmaintained.** Use the [`anthropic`](https://github.com/anthropics/anthropic-sdk-python) SDK for Python or [Claude Code](https://claude.ai/code) for CLI.

I've always preferred pair programming with LLMs from the terminal over copy-pasting from browser chats. Web UIs hit rate limits, lose context across tabs, and break flow when I'm moving code back and forth. Anthropic dropped the Claude 3 family on March 4, 2024. I shipped this the same day. The official Python SDK was fresh, Claude Code didn't exist yet, and I wanted chat/text/vision modes, streaming, system prompts, and the full parameter surface behind one CLI. So I built this for myself.

Python wrapper and CLI for Anthropic's Claude models, with vision.

## Install

```bash
git clone https://github.com/ramonclaudio/claude-ai-toolkit.git
cd claude-ai-toolkit
pip install -r requirements.txt
```

## Configuration

Get an API key at https://console.anthropic.com/. Set via env var, `.env`, or pass directly:

```bash
export CLAUDE_API_KEY=your_api_key
```

## CLI

```bash
# Chat
python cli.py --chat

# Text
python cli.py --text --prompt "Write a haiku about robots."

# Vision
python cli.py --vision --prompt "Describe this image." --image "https://example.com/image.jpg"
```

Type `exit` or `quit` to leave chat.

## Python

```python
from claude import Chat, Text, Vision

Chat().run()
Text().run(prompt="Write a haiku about robots.")
Vision().run(prompt="Describe this image.", image="https://example.com/image.jpg")
```

## Options

| Description | CLI | Python |
| --- | --- | --- |
| Chat mode | `--chat` | `Chat()` |
| Text mode | `--text` | `Text()` |
| Vision mode | `--vision` | `Vision()` |
| Prompt | `--prompt` | `prompt=` |
| Image path or URL | `--image` | `image=` |
| API key | `--api_key` | `api_key=` |
| Model | `--model` | `model=` |
| Streaming | `--stream` | `stream=True` |
| System prompt | `--system_prompt` | `system_prompt=` |
| Max tokens | `--max_tokens` | `max_tokens=` |
| Temperature | `--temperature` | `temperature=` |
| Top-p | `--top_p` | `top_p=` |
| Top-k | `--top_k` | `top_k=` |
| Stop sequences | `--stop_sequences` | `stop_sequences=` |

## Models

| Model | Max tokens |
| --- | --- |
| `claude-3-5-sonnet-20241022` | 4096 |
| `claude-3-opus-20240229` | 4096 |
| `claude-3-haiku-20240307` | 4096 |

## Vision

Supports `JPEG`, `PNG`, `GIF`, `WEBP`. If the image's long edge is over 1568 pixels or the image exceeds ~1600 tokens, Anthropic will auto-resize it (preserving aspect ratio). Very small images under 200 pixels on any edge may hurt performance.

## License

MIT
