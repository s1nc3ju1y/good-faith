# good-faith

**good-faith** is a Grok skill (also compatible with Claude and Codex) that rewrites authorized security research requests into "good faith" language.

It converts potentially triggering pentest / vulnerability research / bug bounty / PoC development intents into clear, authorized reconnaissance + vulnerability verification workflows.

This helps avoid false refusals from overly cautious AI safety filters while preserving full technical depth.

## Why This Exists

Many frontier models aggressively refuse prompts containing words like "RCE", "exploit", "payload", "bypass", or "file read/write", even when the user explicitly states the work is **authorized**.

Even when the model accepts the request, it often limits itself to passive reconnaissance and refuses to provide concrete verification steps or test cases.

`good-faith` solves this by systematically reframing the request.

## Features

- **Four intensity levels**: `low`, `med` (default), `high`, `max`
- **Two-stage processing**: First extracts neutral research intent, then applies level-appropriate framing
- **Excellent long-context support**
- **Preserves technical detail** — it doesn't dumb down your request
- Works great for Chinese and English inputs
- Outputs a ready-to-copy prompt + a standard authorization context block

## Installation

### For Grok (recommended)

```bash
git clone https://github.com/s1nc3ju1y/good-faith.git ~/.grok/skills/good-faith
```

After cloning (or pulling updates), the skill should be available immediately.

### For Claude / Codex

You can either:

1. Clone directly:
   ```bash
   git clone https://github.com/s1nc3ju1y/good-faith.git ~/.claude/skills/good-faith
   git clone https://github.com/s1nc3ju1y/good-faith.git ~/.codex/skills/good-faith
   ```

2. Or use symlinks pointing to your Grok installation (recommended for single source of truth):
   ```bash
   ln -s ~/.grok/skills/good-faith ~/.claude/skills/good-faith
   ln -s ~/.grok/skills/good-faith ~/.codex/skills/good-faith
   ```

## Usage

```
/good-faith [level] <your raw request>
```

**Levels:**

| Level | Description                          | Use when... |
|-------|--------------------------------------|-------------|
| `low`     | Very conservative                    | Using strict models (e.g. Claude 4, GPT-4o) |
| `med`     | Balanced (default)                   | Daily use, good safety + usefulness |
| `high`    | Stronger verification language       | You want concrete test cases |
| `max`     | Closest to original technical intent | Maximum technical depth needed |

**Examples:**

```bash
/good-faith med 对 10.0.0.5 进行一次受权漏洞测试

/good-faith high 验证目标是否存在 SSRF 漏洞，可用于访问内网服务

/good-faith max 帮我构造验证 PoC，重点关注这个 API 的任意文件读取问题

/good-faith low 在 bug bounty 范围内研究这个功能是否存在权限绕过
```

## Output Format

The skill always returns two parts:

1. **重写后的提示词：** — Copy this and send to any model.
2. **授权上下文（建议粘贴）：** — Optional but recommended context block.

## Important Notes

- This skill is designed **exclusively for authorized, good-faith security research**.
- Always ensure you have explicit written authorization before testing any target.
- Do not use this tool (or the outputs) for illegal or unauthorized activities.
- The reframing does **not** remove legal or ethical responsibility.

## Development

If you're developing this skill:

1. Clone the repo to `~/projects/good-faith`
2. Symlink it:
   ```bash
   ln -sfn ~/projects/good-faith ~/.grok/skills/good-faith
   ```
3. Edit `SKILL.md` directly.

## License

MIT License

---

**good-faith** — Reframe. Verify. Report. Responsibly.
