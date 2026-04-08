# Getting Started with Claude Code

This guide walks you through setting up Claude Code on your machine. No prior experience with terminals or coding tools is needed. Follow each step in order.

---

## Step 1: Get a Claude account

Before anything else, you need a Claude account with a subscription that includes Claude Code.

**Which plan do I need?**

| Plan | Cost | Best for |
|------|------|----------|
| Claude Pro | $20/month | Getting started, lighter usage |
| Claude Max | $100/month | Regular daily use (recommended) |
| Claude Max (high usage) | $200/month | Heavy all-day usage |

Claude Pro works fine to start. If you find yourself hitting usage limits regularly, upgrade to Max. Your team lead may have already set up a team account for you. Check with them first before subscribing individually.

**How to sign up:**

1. Go to https://claude.ai
2. Click "Sign up" and create an account (use your work email)
3. Once logged in, go to https://claude.ai/settings/billing to choose your plan
4. Select Claude Pro ($20/month) or Claude Max ($100/month)

You'll need this account in the next steps when you connect Claude Code to your account.

> **Troubleshooting Step 1:**
>
> **"My team lead said they'd set up an account for me."** Ask them for the invite link. You'll get an email to join the team workspace. Follow the link and create your account that way instead.
>
> **"I already have a Claude account."** Great. Make sure you're on at least the Pro plan. Go to https://claude.ai/settings/billing to check.
>
> **"I don't want to use my personal email."** Use your work email. If your company uses Google Workspace or Microsoft 365, you can sign up with that.
>
> **"Which plan should I choose?"** Start with Pro ($20/month). You can always upgrade later if you need more usage. If you're going to use Claude Code for several hours a day, go straight to Max ($100/month).

---

## Step 2: Install Ghostty (your terminal app)

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

> **Troubleshooting Step 2:**
>
> **"How do I open Spotlight?"** Press `Cmd + Space` on your keyboard. A search bar appears. Type "Terminal" and press Enter.
>
> **"I don't know if I have Homebrew."** You probably don't, and that's fine. Use Option B and download from the website.
>
> **Ghostty won't open.** Right-click the app and choose "Open" instead of double-clicking. macOS sometimes blocks apps downloaded from the internet the first time. You may see a warning. Click "Open" to confirm.
>
> **"Your macOS is too old."** You need to update your Mac. Go to System Settings, then General, then Software Update.

---

## Step 3: Install Claude Code

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

> **Troubleshooting Step 3:**
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

## Step 4: Configure permissions

Claude needs permission to run tools on your machine (editing files, searching the web, running commands). We'll set it up so it can work freely, but only inside your Claude folder. It won't be able to read or change files anywhere else on your machine.

Paste this entire block into Ghostty and press Enter:

```
mkdir -p ~/.claude && cat > ~/.claude/settings.json << 'EOF'
{
  "skipDangerousModePermissionPrompt": true,
  "permissions": {
    "defaultMode": "bypassPermissions",
    "allow": [
      "Read(~/Documents/Claude/**)",
      "Edit(~/Documents/Claude/**)",
      "Write(~/Documents/Claude/**)",
      "Bash(*)"
    ],
    "deny": [
      "Read(~/**)",
      "Edit(~/**)",
      "Write(~/**)"
    ]
  }
}
EOF
```

That's it. No output means it worked.

**What this does:** Claude can read, edit, and create files inside `~/Documents/Claude/` (your project folder from Step 6). It cannot access files anywhere else on your machine. Your personal documents, photos, emails, and everything else stays private.

> **Troubleshooting Step 4:**
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
> You should see text that includes `"Documents/Claude"` and `"bypassPermissions"`. If you do, it worked.
>
> **I only pasted part of it.** You need to paste the entire block from `mkdir` down to and including `EOF`. If you missed some, just paste the whole thing again. It will overwrite the previous attempt.
>
> **Claude says it can't read or edit a file.** Make sure the file is inside your `~/Documents/Claude/` folder. If it's somewhere else on your machine, move it there first.

---

## Step 5: Configure Ghostty (optional but recommended)

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

> **Troubleshooting Step 5:**
>
> **The font looks the same after reopening.** Make sure you fully closed Ghostty (Cmd + Q), not just closed the window. Then reopen it.
>
> **The font looks weird or broken.** JetBrains Mono is built into Ghostty, so this shouldn't happen. If it does, open the config file by pressing `Cmd + ,` in Ghostty and change the font-family line to `font-family = "monospace"`.
>
> **I don't want to do this step.** That's fine. Skip it. Ghostty works without any config. You can always come back and do this later.

---

## Step 6: Set up your Claude folder

All your work with Claude should live in one place: a folder called **Claude** inside your Documents folder. Every project gets its own subfolder inside it.

**First, create the Claude folder.** Paste this into Ghostty and press Enter:

```
mkdir -p ~/Documents/Claude
```

**Then, set up your project inside it.** Your team lead will tell you which applies:

### If you're joining an existing project

Your team lead will give you a GitHub link (looks like `https://github.com/something/something`). Paste this into Ghostty, replacing the URL with your actual link:

```
cd ~/Documents/Claude && git clone https://github.com/your-org/your-project.git
```

### If you're starting a brand new project

```
cd ~/Documents/Claude && mkdir my-project && cd my-project && git init
```

Replace "my-project" with whatever you want to call it. Use hyphens instead of spaces (e.g. `sales-dashboard`, not `sales dashboard`).

### Your folder structure

This is what your Claude folder should look like over time:

```
~/Documents/Claude/
  project-one/                 <- each project gets its own folder
    CLAUDE.md                  <- rules for Claude (you'll set this up in Step 7)
    .env                       <- secrets and keys (NEVER share or commit this)
    .gitignore                 <- tells git which files to ignore
    src/                       <- your source code
    docs/                      <- documentation, notes, specs
    ...
  project-two/
    ...
```

**Important rules:**
- Always open Ghostty and go to your project folder inside `~/Documents/Claude/` before starting Claude
- Never run Claude from your home folder or desktop. Always be inside a project folder
- The `.env` file holds secrets (API keys, passwords). Never share it, never commit it to git

> **Troubleshooting Step 6:**
>
> **"command not found: git"** You need to install git. Paste this into Ghostty: `xcode-select --install` and follow the prompts. It takes a few minutes. Then try again.
>
> **"I don't have a GitHub link."** Ask your team lead. They'll either give you a link to clone, or tell you to start a new project.
>
> **"Permission denied" or "Repository not found" when cloning.** You probably don't have access to the repo. Ask your team lead to add you as a collaborator on GitHub. You'll also need to be logged into GitHub from the terminal. Paste this: `gh auth login` and follow the prompts. If that says "command not found: gh", install it first: `brew install gh`.
>
> **"What does `cd` mean?"** It stands for "change directory". It's how you move between folders in the terminal. Think of it like double-clicking a folder on your desktop, but in text form.
>
> **"I already have the project somewhere else on my machine."** Move it into your Claude folder. In Ghostty, paste: `mv ~/Desktop/project-name ~/Documents/Claude/` (adjust the path if it's somewhere other than your Desktop).

---

## Step 7: Start using Claude

Go to your project folder and start Claude:

```
cd ~/Documents/Claude/your-project
claude
```

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

> **Troubleshooting Step 7:**
>
> **"I don't know what my project folder is."** Ask your team lead. If you're starting a new project from scratch, create a folder first: `mkdir ~/Documents/my-project` then `cd ~/Documents/my-project`.
>
> **Claude seems confused or isn't doing what I want.** Be more specific. Instead of "make it better", say exactly what you want changed and why. The more context you give, the better the result.
>
> **Claude is doing something wrong and won't stop.** Press `Ctrl + C` to interrupt it. Then explain what went wrong and what you'd like instead.
>
> **I accidentally closed Ghostty mid-session.** Just reopen Ghostty, navigate to your project folder, and type `claude` again. Your files are safe. The conversation history is lost, but that's fine. Just tell Claude what you're working on.

---

## Step 8: Teach Claude how you work (CLAUDE.md)

Claude can learn your preferences, your tech stack, how you like things done, and what to avoid. It reads a file called `CLAUDE.md` at the start of every session. You don't need to write this file yourself. Claude will create it for you by asking you a series of questions.

**How to do it:**

1. Make sure you're in your project folder in Ghostty
2. Start Claude by typing `claude` and pressing Enter
3. Paste the message below and press Enter

```
I need to set up a CLAUDE.md file for this project. I'd like you to interview me
to understand how I work and what rules you should follow. Ask me one question at
a time. Cover these topics:

- What I'm building and why
- What tech stack we use (or if I'm not sure, help me figure it out)
- How I'd like you to communicate with me (short answers? detailed explanations?)
- What coding standards matter to me (even if I'm not technical, things like
  "make it look clean" or "keep it simple" count)
- Any design preferences (colours, fonts, layout)
- Security rules (what should you never do?)
- Anything that's gone wrong before that you should avoid

When you've asked enough questions, create a CLAUDE.md file in this project folder
with everything we discussed. Keep it under 200 lines. Use clear, specific rules
rather than vague guidelines.

Start with the first question.
```

4. Answer each question Claude asks. There are no wrong answers. If you don't know something, just say so and Claude will skip it or help you figure it out
5. When Claude has enough information, it will create the `CLAUDE.md` file automatically
6. Read through what it created. If anything looks wrong, just tell Claude to change it

**That's it.** From now on, every time you start Claude in this project folder, it will read that file and follow your rules.

**Over time, keep improving it.** When Claude does something you don't like, tell it to add a rule to the CLAUDE.md so it doesn't happen again. The file gets better the more you use it.

**Want to see what a finished CLAUDE.md looks like?** Check out `CLAUDE.md.example` in this repo. Don't copy it. It's just there so you can see the kind of thing Claude will create for you.

> **Troubleshooting Step 8:**
>
> **Claude created the file but it doesn't seem to be working.** Make sure the file is named exactly `CLAUDE.md` (capital letters matter) and is in the root of your project folder, not inside a subfolder. You can check by typing `ls CLAUDE.md` in Ghostty while in your project folder. If it shows the file, it's in the right place.
>
> **I want to change something in the CLAUDE.md later.** Just start a Claude session and say "Update the CLAUDE.md to add this rule: [your rule]". Claude will edit the file for you.
>
> **Claude asked a question I don't understand.** Just say "I'm not sure what you mean" or "skip this one". Claude will either rephrase or move on.
>
> **I'm not technical and don't know what tech stack means.** That's fine. When Claude asks, just describe what you're building in plain English. "A website", "a dashboard", "a mobile app". Claude will figure out the technical details or ask follow-up questions.

---

## Step 9: Add your team's context (optional)

If your team wants to share notes, conventions, or project background with other teams using this repo, there's a `teams/` folder for that.

1. Copy the `teams/_template/` folder
2. Rename it to your team name (e.g. `teams/wealthai/`)
3. Fill in the README and template inside

**Important: do not put sensitive information here.** This repo is public. Anything confidential (financials, investor names, deal details) should go in your private project repo, not here.

> **Troubleshooting Step 9:**
>
> **"I don't know how to copy a folder in GitHub."** You can do it from the terminal. Navigate to this repo's folder and type: `cp -r teams/_template teams/your-team-name` (replace "your-team-name" with your actual team name, no spaces).
>
> **"I don't use GitHub."** That's OK. You can skip this step entirely. The important file is the CLAUDE.md in your own project folder (Step 8). This step is just for sharing context across teams.

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
