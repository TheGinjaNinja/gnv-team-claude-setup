# Windows Support for Team Claude Code Setup Guide

## Problem

The onboarding guide (`README.md`) is entirely Mac-focused. Windows users get stuck at Step 2 and have no path forward. Users have reported this.

## Solution

Split the single README into three files:

1. **`README.md`** - Landing page that links to the platform-specific guides
2. **`README-mac.md`** - Current Mac guide, moved as-is
3. **`README-windows.md`** - New Windows guide, same 10-step structure with Windows equivalents

## Design Decisions

- **Separate files, not inline toggles.** The audience is non-technical. They should open one guide and follow it top to bottom without switching between platforms.
- **Full mirror, not a supplement.** Windows guide is self-contained. Users never need to cross-reference the Mac guide. Duplication cost is low because shared content (pricing, workflow advice, CLAUDE.md interview prompt) is stable.
- **Windows Terminal as the recommended terminal.** Pre-installed on Windows 11, free from Microsoft Store on Windows 10. Closest parallel to Ghostty for non-technical users. VS Code mentioned as an alternative.
- **PowerShell as the default shell.** All commands written for PowerShell (not CMD, not Git Bash). PowerShell is the default in Windows Terminal and the most accessible for non-technical Windows users.
- **Git for Windows as a prerequisite.** Claude Code requires Git Bash internally. This is the one extra install step Windows users have vs Mac.

## File Details

### README.md (landing page)

- Title: "Getting Started with Claude Code"
- One-line description
- Two links: Mac guide, Windows guide
- "Not sure which?" helper line
- Nothing else. Keep it minimal.

### README-mac.md

- Exact content of the current README.md, no changes
- Only difference: title gets "(Mac)" appended for clarity

### README-windows.md

Same 10-step structure. Step-by-step Windows equivalents:

| Step | Mac | Windows |
|------|-----|---------|
| 1. Claude account | Same | Same (no changes) |
| 2. Terminal | Install Ghostty (Mac-only app) | Install Windows Terminal (Microsoft Store or pre-installed on Win 11). Mention VS Code as alternative |
| 3. Install Claude Code | `curl -fsSL https://claude.ai/install.sh \| bash` | Prerequisite: install Git for Windows from git-scm.com. Then `irm https://claude.ai/install.ps1 \| iex` in PowerShell |
| 4. Permissions | bash heredoc writes `~/.claude/settings.json` | PowerShell commands using `New-Item` and `Set-Content`. Path: `$HOME\Documents\Claude\` with `**` glob patterns |
| 5. Terminal config | Ghostty config file with `cat > ...` | Windows Terminal settings via GUI (Settings > open JSON file). Optional and lighter since WT works well out of the box. Font recommendation: JetBrains Mono (install from nerdfonts.com or `winget`) |
| 6. Project folder | `mkdir -p ~/Documents/Claude` | `New-Item -ItemType Directory -Path "$HOME\Documents\Claude" -Force` |
| 7. Start using Claude | `cd ~/Documents/Claude/your-project && claude` | `cd "$HOME\Documents\Claude\your-project"` then `claude`. Same brainstorm/plan/build workflow advice |
| 8. CLAUDE.md | Same interview prompt | Same interview prompt (no changes needed) |
| 9. Dev tools | `brew install gh`, web signups | `winget install GitHub.cli` (or download from cli.github.com). Vercel and Supabase signup identical |
| 10. Team context | `cp -r teams/_template teams/your-team` | `Copy-Item -Recurse teams\_template teams\your-team` |

### Troubleshooting sections

Each step gets Windows-specific troubleshooting:

- "How do I open PowerShell?" instead of "How do I open Spotlight?"
- `winget` errors instead of `brew` errors
- Windows Defender/SmartScreen warnings instead of macOS Gatekeeper
- "Search in Start menu" instead of "search in Spotlight"
- Git for Windows install issues (common on corporate machines with restricted installs)
- PowerShell execution policy issues (`Set-ExecutionPolicy` may be needed)

### Quick reference table

| Action | Mac | Windows |
|--------|-----|---------|
| Start Claude | `claude` | `claude` |
| Get help | `/help` | `/help` |
| Split terminal | `Cmd + D` (Ghostty) | Right-click tab > Split pane (Windows Terminal) |
| Open terminal settings | `Cmd + ,` (Ghostty) | `Ctrl + ,` (Windows Terminal) |
| Stop Claude mid-task | `Ctrl + C` | `Ctrl + C` |
| Exit Claude session | `Ctrl + D` or `/exit` | `Ctrl + D` or `/exit` |
| Exit terminal | `exit` | `exit` |

## Scope

- Three files: `README.md` (rewrite), `README-mac.md` (move), `README-windows.md` (new)
- No changes to `CLAUDE.md.example`, `CLAUDE.md.project-template`, or `teams/` templates (these are platform-agnostic)

## Out of scope

- Linux support (not requested, can be added later with the same pattern)
- Changing the Mac guide content
- Platform-specific CLAUDE.md templates (not needed, CLAUDE.md content is platform-agnostic)
