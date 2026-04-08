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

## 4. How to work with Claude: brainstorm, plan, build

Claude Code works best when you follow a deliberate workflow. Don't just jump straight to "build me X". The quality of what you get out depends on how you work with it.

**The three modes:**

1. **Brainstorm** - Explore the problem space. Tell Claude what you're trying to achieve and why. Discuss options, trade-offs, and approaches. Don't write any code yet. This is where you align on what to build.

2. **Plan** - Once you've agreed on an approach, ask Claude to write a plan. This is a step-by-step implementation outline. Review it, poke holes in it, refine it. The plan becomes your shared roadmap.

3. **Build** - Now execute the plan. Claude writes the code, you review. If something comes up that changes the approach, go back to brainstorming or update the plan. Don't just push through a plan that no longer fits.

**In practice:**
- Start a new feature with "Let's brainstorm how to approach X"
- When aligned, say "Write a plan for this"
- When the plan looks good, say "Let's build it" or "Execute step 1"
- If something unexpected comes up, say "Let's step back and rethink this part"

**This is the default.** We recommend everyone starts this way. As you get more comfortable with Claude, you'll develop your own rhythm. Some people skip brainstorming for small tasks. Some go straight to building for bug fixes. That's fine. But start with the full workflow and adjust from experience, not assumption.

## 5. Set up your project CLAUDE.md

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

## 6. Adding project context for your team

If your team needs shared context that Claude should know about (product background, key decisions, domain terminology), put it in your project's `CLAUDE.md` or in a `docs/` folder that Claude can read.

**Do not put sensitive information in this setup repo.** Investor names, financial figures, deal status, and similar details belong in the project repo itself (private), not here. This repo is for setup guidance and templates.

Each team should own their own project context. The `teams/` folder in this repo has a template for adding team-specific notes that aren't sensitive:

```
teams/
  your-team-name/
    README.md                  <- team-specific setup notes, tools, conventions
    CLAUDE.md.template         <- customised CLAUDE.md template for your projects
```

To add your team: copy `teams/_template/` to `teams/your-team-name/` and fill it in.

## 7. Optional: personal global config

You can also create `~/.claude/CLAUDE.md` for preferences that apply across all your projects (not just ones with a project-level file). Good candidates: communication style, general coding habits, tools you always use.

## 8. Useful commands inside Claude Code

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
