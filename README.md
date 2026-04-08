# Team Claude Code Setup

Get your development environment configured for working with Claude Code.

## 1. Install Ghostty (terminal)

Ghostty is the recommended terminal. It has native support for Shift+Enter (multiline input), desktop notifications when Claude finishes, and built-in shell integration. All of these make a real difference when working with Claude Code.

**macOS (Homebrew):**
```bash
brew install --cask ghostty
```

Or download directly from https://ghostty.org (requires macOS 13+).

**Configure Ghostty:**

Create `~/.config/ghostty/config`:

```
# Font
font-family = "JetBrains Mono"
font-size = 14

# Shell integration (enables notifications, exit status)
shell-integration = true

# Splits for multitasking
keybind = cmd+d=new_split:right
keybind = cmd+shift+d=new_split:down

# Quick config reload
keybind = cmd+shift+comma=reload_config
```

Pick a theme that works for you. Press `Cmd + ,` to open config in your editor, `Cmd + Shift + ,` to reload.

## 2. Install Claude Code

```bash
# macOS / Linux / WSL
curl -fsSL https://claude.ai/install.sh | bash

# Windows PowerShell
irm https://claude.ai/install.ps1 | iex
```

Run `claude` once to authenticate via browser.

## 3. Configure permissions

Create or edit `~/.claude/settings.json`:

```json
{
  "skipDangerousModePermissionPrompt": true,
  "permissions": {
    "defaultMode": "bypassPermissions"
  }
}
```

This lets Claude run all tools (bash, file edits, git, web search) without prompting for each one. Only use this on machines where you're comfortable with that level of access.

## 4. Set up your project CLAUDE.md

This is the important bit. A `CLAUDE.md` file in your project root tells Claude how to work with you. It covers your tech stack, coding standards, communication style, security rules, and anything else that matters to your team.

**Start here:**
1. Copy `CLAUDE.md.project-template` into your project root as `CLAUDE.md`
2. Fill in each section with rules that match how your team actually works
3. Commit it to the repo so everyone on the team gets it automatically

**Need inspiration?** Look at `CLAUDE.md.example` for a filled-in version. Don't copy it wholesale. The value comes from writing rules that reflect your own preferences and standards.

**Tips for writing a good CLAUDE.md:**
- Be specific. "Write clean code" means nothing. "Sort all dropdowns alphabetically" is a real rule
- Include things that have gone wrong before. If Claude kept doing something annoying, add a rule against it
- Update it as you go. Your first version won't be perfect. Refine it over weeks as you learn what works
- Keep it under 200 lines. Claude reads this every session. Long files dilute the important stuff

## 5. Optional: personal global config

You can also create `~/.claude/CLAUDE.md` for preferences that apply across all your projects (not just ones with a project-level file). Good candidates: communication style, general coding habits, tools you always use.

## 6. Useful commands inside Claude Code

| Command | What it does |
|---------|-------------|
| `/help` | Show available commands |
| `/tools` | List available tools |
| `/permissions` | Check active permission rules |
| `/mcp` | Show connected MCP servers |
| `claude doctor` | Diagnose setup issues |

## File and folder structure

Here's how all the config files fit together:

```
~/.config/ghostty/
  config                       <- Ghostty terminal settings

~/.claude/
  settings.json                <- Claude Code permissions and preferences
  CLAUDE.md                    <- your personal global instructions (optional)

~/your-project/
  CLAUDE.md                    <- shared project standards (committed to git)
  src/
    CLAUDE.md                  <- subdirectory overrides (optional, rare)
  .env                         <- NEVER commit this
  .gitignore                   <- must include .env
```

**How CLAUDE.md files merge:** Claude Code reads all levels and combines them. Project-level files are the main way to share team standards. Personal global files are for individual preferences that shouldn't be in git. Subdirectory files are rarely needed but useful if a subfolder has different rules (e.g. a `docs/` folder with different formatting standards).

**Key principle:** anything team-shared goes in the project repo. Anything personal goes in `~/.claude/`. Don't put personal preferences in project files, and don't put project standards only in your personal config.
