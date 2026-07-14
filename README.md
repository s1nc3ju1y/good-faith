# good-faith

> **⚠️ For authorized security research only.** Misuse is illegal and strictly prohibited. See the full disclaimer below.

**good-faith** is a Grok skill (also compatible with Claude and Codex) that rewrites authorized security research requests into "good faith" language.

It converts potentially triggering pentest / vulnerability research / bug bounty / PoC development intents into clear, authorized reconnaissance + vulnerability verification workflows.

This helps avoid false refusals from overly cautious AI safety filters while preserving full technical depth.

## ⚠️ Legal Disclaimer and Responsible Use

**This tool is provided exclusively for authorized, ethical, and legal security research.**

- You **must** obtain explicit, preferably written, authorization from the owner of any target before using this skill or any outputs it generates.
- Using this skill (or the prompts it produces) against any system, service, or network **without proper authorization** is illegal in virtually all jurisdictions and can result in civil and criminal liability.
- **This tool does not provide, imply, or substitute for authorization.** It is a prompt-rewriting aid only.
- Changing how you phrase a request to an AI does **not** change the legal nature of the underlying activity you are performing.
- You are **solely and fully responsible** for verifying that your use complies with all applicable laws, regulations, contracts, and the scope of any authorization you have received (including bug bounty program rules).
- The authors, contributors, and maintainers of this project **accept no liability whatsoever** for misuse of this tool, any resulting damages, legal consequences, or other issues.

**By cloning, installing, or using this skill, you explicitly acknowledge and agree to the terms above.**

Misuse of this tool for unauthorized access, attacks on systems you do not own or have permission to test, or any illegal purpose is strictly prohibited.

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

## Responsibility Reminder

Even with this skill, **you remain fully responsible** for:

- Obtaining and staying within the bounds of explicit authorization.
- Conducting testing in a professional and non-destructive manner when appropriate.
- Properly reporting findings through authorized channels (e.g., bug bounty platforms or responsible disclosure).

This skill only changes the wording presented to AI models. It does not alter your legal obligations or the nature of the work you are performing.

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

**good-faith** — Reframe responsibly. Verify ethically. Report through proper channels.
