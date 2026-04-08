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

> **Troubleshooting Step 1:**
>
> **"How do I open Spotlight?"** Press `Cmd + Space` on your keyboard. A search bar appears. Type "Terminal" and press Enter.
>
> **"I don't know if I have Homebrew."** You probably don't, and that's fine. Use Option B and download from the website.
>
> **Ghostty won't open.** Right-click the app and choose "Open" instead of double-clicking. macOS sometimes blocks apps downloaded from the internet the first time. You may see a warning. Click "Open" to confirm.
>
> **"Your macOS is too old."** You need to update your Mac. Go to System Settings, then General, then Software Update.

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

> **Troubleshooting Step 2:**
>
> **"command not found: curl"** This is very rare on Mac. Try updating your macOS (System Settings, General, Software Update) and try again.
>
> **"command not found: claude"** You need to close Ghostty completely and reopen it after installing. If that doesn't help, paste the install command again and watch for any error messages.
>
> **The browser didn't open.** Try typing `claude` again. If it still doesn't open, look in the terminal for a URL (it will start with https://). Copy that URL and paste it into your browser manually.
>
> **"I don't have a Claude account."** You'll need one. Ask your team lead for an invite, or sign up at https://claude.ai.
>
> **It says I'm already logged in but something seems wrong.** Type `claude /logout` and press Enter, then type `claude` again to log in fresh.

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

> **Troubleshooting Step 3:**
>
> **Nothing happened.** That's correct. This command doesn't show any output when it works. You're good.
>
> **"Permission denied"** Try pasting this first, then run the command above again:
> ```
> mkdir -p ~/.claude
> ```
>
> **I'm not sure it worked.** You can check by pasting this command:
> ```
> cat ~/.claude/settings.json
> ```
> You should see the text that starts with `{` and contains `"bypassPermissions"`. If you do, it worked.
>
> **I only pasted part of it.** You need to paste the entire block from `mkdir` down to and including `EOF`. If you missed some, just paste the whole thing again. It will overwrite the previous attempt.

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

> **Troubleshooting Step 4:**
>
> **The font looks the same after reopening.** Make sure you fully closed Ghostty (Cmd + Q), not just closed the window. Then reopen it.
>
> **The font looks weird or broken.** JetBrains Mono is built into Ghostty, so this shouldn't happen. If it does, open the config file by pressing `Cmd + ,` in Ghostty and change the font-family line to `font-family = "monospace"`.
>
> **I don't want to do this step.** That's fine. Skip it. Ghostty works without any config. You can always come back and do this later.

---

## Step 5: Start using Claude

Open Ghostty, navigate to your project folder, and type `claude` to start a session.

If you're not sure how to navigate to your project folder, paste this (replacing the path with your actual folder):

```
cd ~/Documents/my-project
```

Then type `claude` and press Enter.

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

> **Troubleshooting Step 5:**
>
> **"I don't know what my project folder is."** Ask your team lead. If you're starting a new project from scratch, create a folder first: `mkdir ~/Documents/my-project` then `cd ~/Documents/my-project`.
>
> **Claude seems confused or isn't doing what I want.** Be more specific. Instead of "make it better", say exactly what you want changed and why. The more context you give, the better the result.
>
> **Claude is doing something wrong and won't stop.** Press `Ctrl + C` to interrupt it. Then explain what went wrong and what you'd like instead.
>
> **I accidentally closed Ghostty mid-session.** Just reopen Ghostty, navigate to your project folder, and type `claude` again. Your files are safe. The conversation history is lost, but that's fine. Just tell Claude what you're working on.

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

> **Troubleshooting Step 6:**
>
> **"I don't know what to put in the CLAUDE.md."** Start with just one or two rules. You don't need to fill in every section on day one. Add more rules as you learn what works and what doesn't.
>
> **"I'm not sure Claude is reading my CLAUDE.md."** Make sure the file is named exactly `CLAUDE.md` (capital letters matter) and is in the root of your project folder, not inside a subfolder. When you start a Claude session, it will mention reading the file.
>
> **"How do I open a .md file?"** It's just a text file. Right-click it, choose "Open With", and pick any text editor (TextEdit, VS Code, or even Notes). Or ask Claude to help you edit it inside a session.

---

## Step 7: Add your team's context (optional)

If your team wants to share notes, conventions, or project background with other teams using this repo, there's a `teams/` folder for that.

1. Copy the `teams/_template/` folder
2. Rename it to your team name (e.g. `teams/wealthai/`)
3. Fill in the README and template inside

**Important: do not put sensitive information here.** This repo is public. Anything confidential (financials, investor names, deal details) should go in your private project repo, not here.

> **Troubleshooting Step 7:**
>
> **"I don't know how to copy a folder in GitHub."** You can do it from the terminal. Navigate to this repo's folder and type: `cp -r teams/_template teams/your-team-name` (replace "your-team-name" with your actual team name, no spaces).
>
> **"I don't use GitHub."** That's OK. You can skip this step entirely. The important file is the CLAUDE.md in your own project folder (Step 6). This step is just for sharing context across teams.

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
| Stop Claude mid-task | `Ctrl + C` |
| Exit a Claude session | `Ctrl + D` or type `/exit` |
| Exit the terminal | Type `exit` and press Enter |
