# Nano Image Generate

[简体中文](./README_CN.md)

**The Ultimate Gemini Image Generation Skill for Claude Code & AI Agents.**

Generate high-fidelity assets, logos, and prototypes using **Nano Banana Pro** (Gemini 3 Pro) and **Nano Banana** (Flash). Designed for seamless integration with AI Agents and CLI workflows.

## Features

- **🚀 Dual Model Support**
    - **Pro** (`gemini-3-pro-image-preview`): High quality, detailed text rendering, complex instruction following.
    - **Flash** (`gemini-2.5-flash-image`): Lightning fast, low latency, ideal for rapid prototyping.
- **🎨 Reference Image Support**: Style transfer, character consistency, and multi-image fusion (up to 14 references).
- **🛠️ Agent-Native Design**: Optimized for tool use, with clear error messages and robust path handling.
- **🔑 Flexible Auth**: Pass API Key via CLI argument (secure), Environment Variable, or file config.
- **📂 Smart Output**: Auto-saves to `./generated/` with descriptive filenames if no path is provided.

## Installation

### From GitHub (Recommended)

```bash
claude skill add github:fancyboi999/nano-image-generate
```

### From Local Path

```bash
git clone https://github.com/fancyboi999/nano-image-generate.git
```

Add to your `~/.claude/settings.json`:

```json
{
  "skills": [
    "/absolute/path/to/nano-image-generate"
  ]
}
```

## Setup API Key

You need a Gemini API Key from [Google AI Studio](https://aistudio.google.com/apikey).

**Option 1: CLI Argument (Best for Agents)**
Agents can pass the key directly at runtime:
```bash
python scripts/generate_image.py "prompt" --key "AIzaSy..."
```

**Option 2: Environment Variable (Recommended for Humans)**
```bash
export GEMINI_API_KEY="AIzaSy..."
```

**Option 3: Hardcoded (Not Recommended)**
Edit `scripts/generate_image.py` and replace `YOUR_GEMINI_API_KEY_HERE`.

## Usage

Once installed, simply ask Claude/Agent:

> "Generate a high-quality logo for a tech startup, use the Pro model."
> "Create a quick draft sketch of a cat using the Flash model."
> "Make an image in the same style as this reference."

### CLI Usage

```bash
python scripts/generate_image.py [PROMPT] [OPTIONS]
```

#### Basic (Auto-save to `./generated/`)
```bash
python scripts/generate_image.py "A futuristic city with neon lights"
```

#### Select Model
```bash
# Pro (Default) - Best quality
python scripts/generate_image.py "Detailed portrait" --model pro

# Flash - Best speed
python scripts/generate_image.py "Quick doodle" --model flash
```

#### Style Transfer
```bash
python scripts/generate_image.py "A village in winter" --ref ./style_ref.jpg
```

## Options

| Option | Alias | Description | Default |
|--------|-------|-------------|---------|
| `--output` | `-o` | Output path. If omitted, auto-saves to `./generated/`. | `./generated/<slug>.png` |
| `--model` | `-m` | Model selection: `pro` or `flash`. | `pro` |
| `--key` | `-k` | Gemini API Key. | `None` |
| `--aspect` | `-a` | Aspect ratio (e.g., `16:9`, `4:3`, `1:1`). | `1:1` |
| `--size` | `-s` | Resolution: `1K`, `2K`, `4K`. | `2K` |
| `--ref` | `-r` | Reference image path (max 14). | `None` |

## License

MIT
