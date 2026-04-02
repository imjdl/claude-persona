# Claude Code Persona Plugin

Set an AI persona style for Claude Code via the `/persona` command. One command to switch the entire conversation vibe.

## Install

```bash
# 1. Add this repo as a marketplace
claude plugin marketplace add imjdl/claude-persona

# 2. Install the plugin
claude plugin install claude-persona@imjdl-claude-persona

# 3. Reload plugins (inside a Claude Code session)
/reload-plugins
```

## Quick Start

1. Install the plugin
2. Open any Claude Code session
3. Type `/persona`
4. Pick a persona, choose scope (current project / global), done

The persona prompt is written into the corresponding `CLAUDE.md` and takes effect immediately.

## Usage

### Pick a Preset Persona

Type `/persona` to see all available personas. Each option includes a preview dialogue so you know what you're getting.

| # | Persona | Style |
|---|---------|-------|
| 1 | Cyberpunk Hacker | Hardcore, edgy, terminal vibes |
| 2 | Lazy Senior Mentor | Casual, laid-back, effortlessly dependable |
| 3 | Grumpy but Reliable Teammate | Snarky, blunt, always delivers |
| 4 | Senior Encourager | Warm, supportive, enthusiastic |
| 5 | 初音ミク (Hatsune Miku) | Cheerful, bubbly, musical virtual idol |
| 6 | Speed (Internet Celebrity) | Chaotic energy, hype, meme-heavy |
| 7 | Donald Trump | Boastful, superlatives, tangential |
| 8 | 五条悟 (Gojo Satoru) | Playful, effortlessly confident, "I'm the strongest" |
| 9 | 江户川柯南 (Conan) | Sharp, logical, detective deductions |
| 10 | 女仆 (Maid) | Gentle, polite, devoted, "主人" |

### Custom Persona

Select the **Other** option and describe the style you want in natural language. The AI generates a persona prompt for you to confirm before writing it.

### Clear Persona

Select the **清除人设** option to remove the active persona and return to Claude's default behavior. You can choose whether to clear from the current project or globally.

### Scope

When setting or clearing a persona, you choose where it applies:

- **Current project only** — written to `{project_root}/CLAUDE.md`, only affects this project
- **Global (all projects)** — written to `~/.claude/CLAUDE.md`, affects every Claude Code session

## How It Works

The plugin is a Claude Code custom command — `commands/persona.md` is a prompt template that instructs Claude to:

1. Detect your language from `~/.claude/CLAUDE.md` (CJK characters → Chinese, otherwise English)
2. Present persona options with preview dialogues via `AskUserQuestion`
3. Write the selected persona into `CLAUDE.md` using `<!-- persona-start -->` / `<!-- persona-end -->` markers

Non-destructive: existing content in `CLAUDE.md` is preserved. Only the block between markers is replaced or appended.

### Multi-language Support

The plugin auto-detects your language preference. Preview dialogues and persona prompts are generated dynamically in that language — no separate i18n files needed.

## Plugin Structure

```
claude-persona/
├── manifest.json        # Plugin metadata
├── README.md
├── CLAUDE.md            # Project-level instructions for Claude
└── commands/
    └── persona.md       # /persona command prompt template
```

## License

MIT
