# Nano Image Generate

[English](./README.md)

**适用于 Claude Code 与 AI Agent 的终极 Gemini 图像生成技能。**

使用 **Nano Banana Pro** (Gemini 3 Pro) 和 **Nano Banana** (Flash) 生成高保真素材、Logo 和原型。专为 AI Agent 集成和 CLI 工作流设计。

## 功能特点

- **🚀 双模型支持**
    - **Pro** (`gemini-3-pro-image-preview`)：高质量、优秀的文字渲染能力、复杂的指令遵循能力。
    - **Flash** (`gemini-2.5-flash-image`)：极速生成、低延迟，适合快速原型设计。
- **🎨 参考图片支持**：风格迁移、角色一致性保持、多图融合（最多支持 14 张参考图）。
- **🛠️ Agent 原生设计**：针对工具调用进行了优化，提供清晰的错误提示和健壮的路径处理。
- **🔑 灵活的认证方式**：支持通过 CLI 参数传递 API Key（安全）、环境变量或文件配置。
- **📂 智能输出**：如果未提供路径，自动保存到 `./generated/` 目录并生成描述性文件名。

## 安装

### 从 GitHub 安装（推荐）

```bash
claude skill add github:fancyboi999/nano-image-generate
```

### 从本地路径安装

```bash
git clone https://github.com/fancyboi999/nano-image-generate.git
```

添加到你的 `~/.claude/settings.json`：

```json
{
  "skills": [
    "/absolute/path/to/nano-image-generate"
  ]
}
```

## 配置 API Key

你需要从 [Google AI Studio](https://aistudio.google.com/apikey) 获取 Gemini API Key。

**选项 1: CLI 参数 (Agent 最佳实践)**
Agent 可以直接在运行时传递 Key：
```bash
python scripts/generate_image.py "prompt" --key "AIzaSy..."
```

**选项 2: 环境变量 (人类用户推荐)**
```bash
export GEMINI_API_KEY="AIzaSy..."
```

**选项 3: 硬编码 (不推荐)**
编辑 `scripts/generate_image.py` 并替换 `YOUR_GEMINI_API_KEY_HERE`。

## 使用方法

安装后，只需告诉 Claude/Agent：

> "生成一个科技初创公司的 Logo，使用 Pro 模型。"
> "用 Flash 模型快速画一个猫的草图。"
> "参照这张图片的风格生成一张新图。"

### CLI 用法

```bash
python scripts/generate_image.py [提示词] [选项]
```

#### 基础用法 (自动保存到 `./generated/`)
```bash
python scripts/generate_image.py "一个霓虹灯闪烁的未来城市"
```

#### 选择模型
```bash
# Pro (默认) - 最佳画质
python scripts/generate_image.py "精细的人像" --model pro

# Flash - 最佳速度
python scripts/generate_image.py "快速涂鸦" --model flash
```

#### 风格迁移
```bash
python scripts/generate_image.py "冬日的村庄" --ref ./style_ref.jpg
```

## 选项参数

| 选项 | 别名 | 说明 | 默认值 |
|------|------|------|--------|
| `--output` | `-o` | 输出路径。省略时自动保存到 `./generated/`。 | `./generated/<slug>.png` |
| `--model` | `-m` | 模型选择：`pro` 或 `flash`。 | `pro` |
| `--key` | `-k` | Gemini API Key。 | `None` |
| `--aspect` | `-a` | 宽高比 (例如 `16:9`, `4:3`, `1:1`)。 | `1:1` |
| `--size` | `-s` | 分辨率：`1K`, `2K`, `4K`。 | `2K` |
| `--ref` | `-r` | 参考图片路径 (最多 14 张)。 | `None` |

## 许可证

MIT
