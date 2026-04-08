# Getting Started with Claude Code

This guide walks you through setting up Claude Code on your machine. No prior experience with terminals or coding tools is needed. Follow each step in order.

---

## Step 1: Install Ghostty (your terminal app)

A terminal is the app where you'll talk to Claude. We use Ghostty because it works better with Claude than the default terminal on your Mac.

**Option A: If you have Homebrew installed**

Open your current Terminal app (search "Terminal" in Spotlight) and paste this:

```
brew install --cask ghostty
```

**Option B: If you don't have Homebrew (or aren't sure)**

1. Go to https://ghostty.org
2. Download the Mac app
3. Open the downloaded file and drag Ghostty to your Applications folder

Once installed, open Ghostty. It looks like a terminal with a black background. This is where you'll run all the commands below.

**You need macOS 13 or newer.** To check: click the Apple menu at the top left of your screen, then "About This Mac". If your version number starts with 13 or higher, you're fine.

---

## Step 2: Install Claude Code

In Ghostty, paste this command and press Enter:

```
curl -fsSL https://claude.ai/install.sh | bash
```

When it finishes, close Ghostty and reopen it (so it picks up the new installation).

Then type this and press Enter:

```
claude
```

A browser window will open asking you to log in. Sign in with your Claude account. Once you see a confirmation message, go back to Ghostty. You're connected.

---

## Step 3: Configure permissions

Claude needs permission to run tools on your machine (editing files, searching the web, running commands). We'll set it up so it doesn't ask you for permission every single time.

Paste this entire block into Ghostty and press Enter:

```
mkdir -p ~/.claude && cat > ~/.claude/settings.json << 'EOF'
{
  "skipDangerousModePermissionPrompt": true,
  "permissions": {
    "defaultMode": "bypassPermissions"
  }
}
EOF
```

That's it. No output means it worked.

---

## Step 4: Configure Ghostty (optional but recommended)

This makes Ghostty nicer to use. Paste this into Ghostty and press Enter:

```
mkdir -p ~/.config/ghostty && cat > ~/.config/ghostty/config << 'EOF'
font-family = "JetBrains Mono"
font-size = 14
shell-integration = true
keybind = cmd+d=new_split:right
keybind = cmd+shift+d=new_split:down
keybind = cmd+shift+comma=reload_config
EOF
```

Close and reopen Ghostty to see the changes.

**What this does:**
- Sets a clean, readable font
- Lets you press `Cmd + D` to split the screen (useful for having Claude in one side and something else in the other)
- Enables notifications so you know when Claude has finished a task

---

## Step 5: Start using Claude

Open Ghostty, navigate to your project folder, and type `claude` to start a session.

**But before you ask Claude to build anything, read this section. It will save you a lot of time.**

### The three modes: brainstorm, plan, build

Claude works best when you work through problems in stages rather than jumping straight to "build me X".

**1. Brainstorm first**

Tell Claude what you're trying to achieve and why. Discuss options. Explore the problem. Don't ask for any code yet.

Example: *"I need a dashboard that shows our team's weekly metrics. The audience is our investors. Let's brainstorm how to approach this."*

**2. Then plan**

Once you've agreed on an approach, ask Claude to write a plan. Review it. Ask questions. Poke holes in it.

Example: *"That approach sounds good. Write a plan for how we'd build this step by step."*

**3. Then build**

Now ask Claude to execute the plan. It writes the code, you review what it produces.

Example: *"The plan looks good. Let's build it, starting with step 1."*

**If something changes along the way**, don't just push through. Say *"Let's step back and rethink this part."* Going back to brainstorming is not a waste of time. It prevents wasted effort.

**Start with all three steps.** As you get more comfortable, you'll find your own rhythm. Small fixes might not need brainstorming. That's fine. But learn the full workflow first, then adjust.

---

## Step 6: Teach Claude how your team works (CLAUDE.md)

You can give Claude a set of rules for your project. Things like what tech stack you use, how you want code written, what to avoid. Claude reads these rules at the start of every session.

**How to set this up:**

1. In this repo, find the file called `CLAUDE.md.project-template`
2. Copy it into your project folder and rename it to `CLAUDE.md`
3. Open it in any text editor and fill in each section

The comments inside the file explain what to put in each section. Delete the comments as you fill them in.

**Want to see a completed example?** Look at `CLAUDE.md.example` in this repo. Don't copy it directly. Use it as inspiration and write rules that match how your team actually works.

**Tips:**
- Be specific. "Write good code" is useless. "Sort all dropdowns alphabetically" is a real rule Claude can follow
- Add rules when Claude does something you don't like. Over time your file gets better
- Keep it under 200 lines. Claude reads this every session and long files dilute the important stuff

---

## Step 7: Add your team's context (optional)

If your team wants to share notes, conventions, or project background with other teams using this repo, there's a `teams/` folder for that.

1. Copy the `teams/_template/` folder
2. Rename it to your team name (e.g. `teams/wealthai/`)
3. Fill in the README and template inside

**Important: do not put sensitive information here.** This repo is public. Anything confidential (financials, investor names, deal details) should go in your private project repo, not here.

---

## Quick reference

Once you're set up, here are useful things to know:

| What you want to do | What to type |
|---------------------|-------------|
| Start Claude | `claude` |
| Get help | `/help` (inside a Claude session) |
| See available tools | `/tools` (inside a Claude session) |
| Check if setup is working | `claude doctor` |
| Split Ghostty screen | `Cmd + D` |
| Open Ghostty settings | `Cmd + ,` |

---

## Troubleshooting

**"command not found: claude"**
Close Ghostty and reopen it. If that doesn't work, run the install command from Step 2 again.

**Browser didn't open when I typed `claude`**
Try running `claude` again. If it still doesn't open, copy the URL that appears in the terminal and paste it into your browser manually.

**"Permission denied" errors**
Run the permissions command from Step 3 again. Make sure you paste the whole block, not just part of it.

**Something else not working?**
Run `claude doctor` in Ghostty. It checks your setup and tells you what's wrong.
