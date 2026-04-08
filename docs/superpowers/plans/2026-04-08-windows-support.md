# Windows Support Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a complete Windows onboarding guide and restructure the repo so Mac and Windows users each get a dedicated, self-contained guide.

**Architecture:** Split current README.md into a landing page + two platform guides. Mac guide is the existing content moved to a new file. Windows guide is new content mirroring the same 10-step structure with PowerShell commands, Windows Terminal, and Git for Windows.

**Tech Stack:** Markdown only. No code.

---

### Task 1: Move current Mac guide to README-mac.md

**Files:**
- Create: `README-mac.md`

- [ ] **Step 1: Create README-mac.md with current README.md content**

Copy the full content of the current `README.md` into a new file `README-mac.md`. Change only the title from:

```markdown
# Getting Started with Claude Code
```

to:

```markdown
# Getting Started with Claude Code (Mac)
```

No other changes. The Mac guide stays exactly as it is.

- [ ] **Step 2: Commit**

```bash
git add README-mac.md
git commit -m "Move Mac guide to README-mac.md"
```

---

### Task 2: Replace README.md with landing page

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Replace README.md with landing page content**

Replace the entire content of `README.md` with:

```markdown
# Getting Started with Claude Code

This guide walks you through setting up Claude Code on your machine. No prior experience with terminals or coding tools is needed.

Pick the guide for your operating system:

- **[Mac setup guide](README-mac.md)** — for macOS (13 or newer)
- **[Windows setup guide](README-windows.md)** — for Windows 10 or 11

**Not sure which?** Click the Apple menu at the top-left of your screen. If you see "About This Mac", use the Mac guide. If you see a Windows logo in the bottom-left corner of your screen (or bottom-centre), use the Windows guide.
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "Replace README with landing page linking to platform guides"
```

---

### Task 3: Write README-windows.md — Steps 1-3 (account, terminal, install)

**Files:**
- Create: `README-windows.md`

- [ ] **Step 1: Create README-windows.md with Steps 1-3**

Create `README-windows.md` with the following content. This covers the account setup, Windows Terminal install, and Claude Code install (including Git for Windows prerequisite).

```markdown
# Getting Started with Claude Code (Windows)

This guide walks you through setting up Claude Code on your Windows PC. No prior experience with terminals or coding tools is needed. Follow each step in order.

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

## Step 2: Install Windows Terminal (your terminal app)

A terminal is the app where you'll talk to Claude. We use Windows Terminal because it's modern, clean, and works well with Claude Code.

**If you're on Windows 11:** Windows Terminal is already installed. Search for "Terminal" in the Start menu and open it.

**If you're on Windows 10:** Install it from the Microsoft Store.

1. Open the Microsoft Store (search "Microsoft Store" in the Start menu)
2. Search for "Windows Terminal"
3. Click "Get" or "Install"
4. Once installed, search for "Terminal" in the Start menu and open it

You should see a window with a dark background and a blinking cursor. This is PowerShell running inside Windows Terminal. This is where you'll run all the commands below.

**Alternative:** If you already use VS Code, you can use its built-in terminal instead. Press `Ctrl + ~` (backtick) to open it. Everything in this guide works the same way.

> **Troubleshooting Step 2:**
>
> **"How do I open the Start menu?"** Click the Windows logo in the bottom-left corner of your screen (or bottom-centre on Windows 11). Or press the Windows key on your keyboard.
>
> **"I can't find Windows Terminal in the Microsoft Store."** Make sure you're searching for "Windows Terminal" (two words). If the Store isn't working, you can download it directly from https://aka.ms/terminal.
>
> **"I see Command Prompt instead of PowerShell."** In Windows Terminal, click the small down arrow next to the tab at the top and select "Windows PowerShell". To make PowerShell the default, go to Settings (click the down arrow, then Settings) and set the Default profile to "Windows PowerShell".
>
> **"Which version of Windows do I have?"** Press the Windows key, type "winver" and press Enter. A window will pop up showing your version. You need Windows 10 version 1809 or newer, or any version of Windows 11.

---

## Step 3: Install Git and Claude Code

Claude Code needs Git installed on your machine to work. Install Git first, then Claude Code.

**Step 3a: Install Git for Windows**

Paste this command into Windows Terminal and press Enter:

```
winget install Git.Git
```

When it finishes, close Windows Terminal completely and reopen it (so it picks up the new installation).

If `winget` doesn't work (some older Windows 10 machines don't have it), download Git directly from https://git-scm.com/downloads/win and run the installer. Accept all the default options.

**Step 3b: Install Claude Code**

In Windows Terminal, paste this command and press Enter:

```
irm https://claude.ai/install.ps1 | iex
```

When it finishes, close Windows Terminal and reopen it.

Then type this and press Enter:

```
claude
```

A browser window will open asking you to log in. Sign in with your Claude account. Once you see a confirmation message, go back to Windows Terminal. You're connected.

> **Troubleshooting Step 3:**
>
> **"winget is not recognized"** Your Windows doesn't have winget. Download Git directly from https://git-scm.com/downloads/win instead. Run the installer and accept all default options.
>
> **"irm is not recognized"** You're probably in Command Prompt instead of PowerShell. Close the window and open Windows Terminal again. Make sure you see "PowerShell" in the tab at the top, not "Command Prompt".
>
> **"Running scripts is disabled on this system"** PowerShell's execution policy is blocking the install. Paste this command first, then try the install command again:
> ```
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```
> Type "Y" and press Enter when it asks to confirm.
>
> **"command not found: claude"** Close Windows Terminal completely and reopen it after installing. If that doesn't help, paste the install command again and watch for any error messages.
>
> **The browser didn't open.** Try typing `claude` again. If it still doesn't open, look in the terminal for a URL (it will start with https://). Copy that URL and paste it into your browser manually.
>
> **It says I'm already logged in but something seems wrong.** Type `claude /logout` and press Enter, then type `claude` again to log in fresh.
>
> **Windows Defender or SmartScreen shows a warning.** This can happen with new downloads. Click "More info" and then "Run anyway". The Claude Code installer is safe.
```

- [ ] **Step 2: Commit**

```bash
git add README-windows.md
git commit -m "Add Windows guide: Steps 1-3 (account, terminal, install)"
```

---

### Task 4: Write README-windows.md — Steps 4-6 (permissions, terminal config, project folder)

**Files:**
- Modify: `README-windows.md`

- [ ] **Step 1: Append Steps 4-6 to README-windows.md**

Add the following content to the end of `README-windows.md`:

```markdown

---

## Step 4: Configure permissions

Claude needs permission to run tools on your machine (editing files, searching the web, running commands). We'll set it up so it can work freely, but only inside your Claude folder. It won't be able to read or change files anywhere else on your machine.

Paste this into Windows Terminal and press Enter:

```powershell
New-Item -ItemType Directory -Path "$HOME\.claude" -Force | Out-Null

@'
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
'@ | Set-Content "$HOME\.claude\settings.json" -Encoding UTF8
```

No output means it worked.

**What this does:** Claude can read, edit, and create files inside your `Documents\Claude\` folder (your project folder from Step 6). It cannot access files anywhere else on your machine. Your personal documents, photos, emails, and everything else stays private.

> **Troubleshooting Step 4:**
>
> **Nothing happened.** That's correct. This command doesn't show any output when it works. You're good.
>
> **I'm not sure it worked.** You can check by pasting this command:
> ```
> Get-Content "$HOME\.claude\settings.json"
> ```
> You should see text that includes `"Documents/Claude"` and `"bypassPermissions"`. If you do, it worked.
>
> **I got a red error message.** Make sure you pasted the entire block, from `New-Item` down to the last line. If you missed some, just paste the whole thing again. It will overwrite the previous attempt.
>
> **Claude says it can't read or edit a file.** Make sure the file is inside your `Documents\Claude\` folder. If it's somewhere else on your machine, move it there first.

---

## Step 5: Configure Windows Terminal (optional but recommended)

This makes Windows Terminal nicer to use. You can do this through the Settings UI.

1. Open Windows Terminal
2. Click the small down arrow next to the tab at the top, then click **Settings** (or press `Ctrl + ,`)
3. Under **Profiles**, click **Defaults**
4. Under **Appearance**, set:
   - Font face: `Cascadia Code` (this is already the default and works well)
   - Font size: `14`
5. Click **Save**

**Want split panes?** You can split your terminal window to have Claude in one side and something else in the other:
- `Alt + Shift + D` splits the current pane
- `Alt + Arrow keys` moves between panes

That's it. Windows Terminal works well out of the box.

> **Troubleshooting Step 5:**
>
> **I can't find the Settings.** Click the small down arrow (v) next to the "+" tab button at the top of Windows Terminal. "Settings" is at the bottom of that menu.
>
> **I want a different font.** JetBrains Mono is a popular coding font. To install it: search "JetBrains Mono" in the Microsoft Store, or paste this in the terminal: `winget install JetBrains.JetBrainsMono`. Then set it as the font in Settings.
>
> **I don't want to do this step.** That's fine. Skip it. Windows Terminal works without any config changes. You can always come back and do this later.

---

## Step 6: Set up your Claude folder

All your work with Claude should live in one place: a folder called **Claude** inside your Documents folder. Every project gets its own subfolder inside it.

**First, create the Claude folder.** Paste this into Windows Terminal and press Enter:

```
New-Item -ItemType Directory -Path "$HOME\Documents\Claude" -Force
```

**Then, set up your project inside it.** Your team lead will tell you which applies:

### If you're joining an existing project

Your team lead will give you a GitHub link (looks like `https://github.com/something/something`). Paste this into Windows Terminal, replacing the URL with your actual link:

```
cd "$HOME\Documents\Claude"
git clone https://github.com/your-org/your-project.git
```

### If you're starting a brand new project

```
cd "$HOME\Documents\Claude"
mkdir my-project
cd my-project
git init
```

Replace "my-project" with whatever you want to call it. Use hyphens instead of spaces (e.g. `sales-dashboard`, not `sales dashboard`).

### Your folder structure

This is what your Claude folder should look like over time:

```
C:\Users\YourName\Documents\Claude\
  project-one\                 <- each project gets its own folder
    CLAUDE.md                  <- rules for Claude (you'll set this up in Step 7)
    .env                       <- secrets and keys (NEVER share or commit this)
    .gitignore                 <- tells git which files to ignore
    src\                       <- your source code
    docs\                      <- documentation, notes, specs
    ...
  project-two\
    ...
```

**Important rules:**
- Always open Windows Terminal and go to your project folder inside `Documents\Claude\` before starting Claude
- Never run Claude from your home folder or desktop. Always be inside a project folder
- The `.env` file holds secrets (API keys, passwords). Never share it, never commit it to git

> **Troubleshooting Step 6:**
>
> **"git is not recognized"** You need to install Git first (Step 3a). If you already installed it, close Windows Terminal completely and reopen it.
>
> **"I don't have a GitHub link."** Ask your team lead. They'll either give you a link to clone, or tell you to start a new project.
>
> **"Permission denied" or "Repository not found" when cloning.** You probably don't have access to the repo. Ask your team lead to add you as a collaborator on GitHub. You'll also need to be logged into GitHub from the terminal. Paste this: `gh auth login` and follow the prompts. If that says "gh is not recognized", install it first (see Step 9).
>
> **"What does `cd` mean?"** It stands for "change directory". It's how you move between folders in the terminal. Think of it like double-clicking a folder on your desktop, but in text form.
>
> **"I already have the project somewhere else on my machine."** Move it into your Claude folder. In Windows Terminal, paste: `Move-Item "$HOME\Desktop\project-name" "$HOME\Documents\Claude\"` (adjust the path if it's somewhere other than your Desktop).
```

- [ ] **Step 2: Commit**

```bash
git add README-windows.md
git commit -m "Add Windows guide: Steps 4-6 (permissions, config, project folder)"
```

---

### Task 5: Write README-windows.md — Steps 7-8 (using Claude, CLAUDE.md)

**Files:**
- Modify: `README-windows.md`

- [ ] **Step 1: Append Steps 7-8 to README-windows.md**

Add the following content to the end of `README-windows.md`:

```markdown

---

## Step 7: Start using Claude

Go to your project folder and start Claude:

```
cd "$HOME\Documents\Claude\your-project"
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
> **"I don't know what my project folder is."** Ask your team lead. If you're starting a new project from scratch, create a folder first: `mkdir "$HOME\Documents\Claude\my-project"` then `cd "$HOME\Documents\Claude\my-project"`.
>
> **Claude seems confused or isn't doing what I want.** Be more specific. Instead of "make it better", say exactly what you want changed and why. The more context you give, the better the result.
>
> **Claude is doing something wrong and won't stop.** Press `Ctrl + C` to interrupt it. Then explain what went wrong and what you'd like instead.
>
> **I accidentally closed Windows Terminal mid-session.** Just reopen Windows Terminal, navigate to your project folder, and type `claude` again. Your files are safe. The conversation history is lost, but that's fine. Just tell Claude what you're working on.

---

## Step 8: Teach Claude how you work (CLAUDE.md)

Claude can learn your preferences, your tech stack, how you like things done, and what to avoid. It reads a file called `CLAUDE.md` at the start of every session. You don't need to write this file yourself. Claude will create it for you by asking you a series of questions.

**How to do it:**

1. Make sure you're in your project folder in Windows Terminal
2. Start Claude by typing `claude` and pressing Enter
3. Paste the message below and press Enter

```
I need to set up a CLAUDE.md file for this project. I'd like you to interview me
to understand how I work and what rules you should follow. Ask me one question at
a time. Cover these topics:

- What I'm building and why
- What kind of work I'll ask you to do (building apps, writing documents,
  creating presentations, research, analysis, or a mix of these)
- What tech stack we use (or if I'm not sure, help me figure it out)
- For documents and written content: what format do I want? (HTML pages,
  markdown files, PDFs, slide decks) What tone and style? (formal, casual,
  technical, plain English) Any branding or formatting rules?
- How I'd like you to communicate with me (short answers? detailed explanations?
  do I want you to ask clarifying questions or just go ahead?)
- How I'd like you to handle saving work (should you commit to git regularly?
  ask before committing? save progress at the end of each session?)
- What coding standards matter to me (even if I'm not technical, things like
  "make it look clean" or "keep it simple" count)
- Any design preferences (colours, fonts, layout)
- Security rules (what should you never do?)
- Anything that's gone wrong before that you should avoid
- How I'd like to update these rules over time (should you suggest new rules
  when you notice patterns? should you ask me before changing anything?)

When you've asked enough questions, create a CLAUDE.md file in this project folder
with everything we discussed. Keep it under 200 lines. Use clear, specific rules
rather than vague guidelines.

Also include a section at the end of the CLAUDE.md called "How to update this file"
that reminds me I can say things like "add a rule to CLAUDE.md that says..." or
"update the CLAUDE.md to change..." at any time during a session.

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
> **Claude created the file but it doesn't seem to be working.** Make sure the file is named exactly `CLAUDE.md` (capital letters matter) and is in the root of your project folder, not inside a subfolder. You can check by typing `dir CLAUDE.md` in Windows Terminal while in your project folder. If it shows the file, it's in the right place.
>
> **I want to change something in the CLAUDE.md later.** Just start a Claude session and say "Update the CLAUDE.md to add this rule: [your rule]". Claude will edit the file for you.
>
> **Claude asked a question I don't understand.** Just say "I'm not sure what you mean" or "skip this one". Claude will either rephrase or move on.
>
> **I'm not technical and don't know what tech stack means.** That's fine. When Claude asks, just describe what you're building in plain English. "A website", "a dashboard", "a mobile app". Claude will figure out the technical details or ask follow-up questions.
```

- [ ] **Step 2: Commit**

```bash
git add README-windows.md
git commit -m "Add Windows guide: Steps 7-8 (using Claude, CLAUDE.md setup)"
```

---

### Task 6: Write README-windows.md — Steps 9-10 and quick reference

**Files:**
- Modify: `README-windows.md`

- [ ] **Step 1: Append Steps 9-10 and quick reference to README-windows.md**

Add the following content to the end of `README-windows.md`:

```markdown

---

## Step 9: Set up developer tools (if building apps or publishing)

If you're building apps, websites, or anything that needs to go live, you'll need accounts on a few services. If you're only writing documents or doing research, you can skip this step.

### GitHub (code storage and collaboration) - FREE

GitHub is where your code lives online. It's like a backup that also lets your team collaborate.

**Cost:** Free for everything you need. Private repos, unlimited collaborators.

**Setup:**
1. Go to https://github.com and create an account (use your work email)
2. In Windows Terminal, install the GitHub command line tool:
   ```
   winget install GitHub.cli
   ```
3. Log in from the terminal:
   ```
   gh auth login
   ```
4. Follow the prompts. Choose "GitHub.com", "HTTPS", and "Login with a web browser"

> **Troubleshooting:**
>
> **"winget is not recognized"** Your Windows doesn't have winget. Download the GitHub CLI directly from https://cli.github.com instead. Run the installer.
>
> **"I already have a GitHub account."** Just run `gh auth login` to connect it to your terminal.

---

### Vercel (publishing websites and apps) - FREE to start

Vercel takes your code and puts it on the internet. When you push code to GitHub, Vercel automatically updates your live site.

**Cost:**
| Plan | Cost | What you get |
|------|------|-------------|
| Hobby (free) | $0/month | Personal, non-commercial projects. 100 GB bandwidth |
| Pro | $20/month | Commercial use. 1 TB bandwidth. Custom domains |

Start on the free Hobby plan. Upgrade to Pro when you're ready to go live with something commercial.

**Setup:**
1. Go to https://vercel.com and sign up (use "Continue with GitHub" so they're linked)
2. That's it for now. When you're ready to deploy something, Claude will walk you through connecting your project

> **Troubleshooting:**
>
> **"Should I sign up with GitHub or email?"** Use "Continue with GitHub". It connects the two accounts automatically, which makes deploying much easier.
>
> **"Do I need the Pro plan?"** Not yet. The free plan is fine for building and testing. You only need Pro when you want to use a custom domain or go commercial.

---

### Supabase (database and backend) - FREE to start

Supabase is where your app stores data. User accounts, content, files. Think of it as the backend that powers your app.

**Cost:**
| Plan | Cost | What you get |
|------|------|-------------|
| Free | $0/month | 500 MB database, 1 GB file storage. Pauses after 7 days of inactivity |
| Pro | $25/month | 8 GB database, 250 GB file storage. Never pauses. Daily backups |

Start on the free plan. It's enough for building and testing. Upgrade to Pro when your app has real users or you need it to stay online permanently.

**Setup:**
1. Go to https://supabase.com and sign up (use "Continue with GitHub" so they're linked)
2. Create a new project. Pick a name and set a database password (save this somewhere safe)
3. Choose the region closest to your users (London for UK)
4. That's it for now. Claude will help you connect your app to Supabase when the time comes

> **Troubleshooting:**
>
> **"My Supabase project paused itself."** On the free plan, projects pause after 7 days with no activity. Go to your Supabase dashboard and click "Restore project". To avoid this, upgrade to Pro ($25/month).
>
> **"I forgot my database password."** You can reset it in the Supabase dashboard under Settings, then Database.
>
> **"Do I need all three services?"** Not necessarily. GitHub is useful for everyone (it backs up your code). Vercel and Supabase are only needed if you're building apps or websites. Ask your team lead if you're not sure.

---

### Cost summary

| Service | Free tier | Paid tier | When to upgrade |
|---------|-----------|-----------|-----------------|
| Claude | - | $20-200/month | You need this from day one |
| GitHub | Unlimited | $4/month (rarely needed) | Only if you need advanced branch protection |
| Vercel | Personal projects | $20/month | When going commercial or using custom domains |
| Supabase | 500 MB, auto-pauses | $25/month | When you have real users or need always-on |

**Minimum cost to get started: $20/month** (just Claude Pro). Everything else has a free tier that's fine for building and testing.

---

## Step 10: Add your team's context (optional)

If your team wants to share notes, conventions, or project background with other teams using this repo, there's a `teams/` folder for that.

1. Copy the `teams/_template/` folder
2. Rename it to your team name (e.g. `teams/wealthai/`)
3. Fill in the README and template inside

**From the terminal:**

```
Copy-Item -Recurse teams\_template teams\your-team-name
```

Replace "your-team-name" with your actual team name, no spaces.

**Important: do not put sensitive information here.** This repo is public. Anything confidential (financials, investor names, deal details) should go in your private project repo, not here.

> **Troubleshooting Step 10:**
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
| Split terminal pane | `Alt + Shift + D` |
| Move between panes | `Alt + Arrow keys` |
| Open terminal settings | `Ctrl + ,` |
| Stop Claude mid-task | `Ctrl + C` |
| Exit a Claude session | `Ctrl + D` or type `/exit` |
| Exit the terminal | Type `exit` and press Enter |
```

- [ ] **Step 2: Commit**

```bash
git add README-windows.md
git commit -m "Add Windows guide: Steps 9-10 and quick reference"
```

---

### Task 7: Final review

- [ ] **Step 1: Read through all three files end-to-end**

Read `README.md`, `README-mac.md`, and `README-windows.md` in full. Check for:
- Broken links between files
- Inconsistent step numbering
- Any Mac-specific language that leaked into the Windows guide
- Any Windows-specific language that leaked into the Mac guide
- Matching pricing tables (both guides should show the same costs)
- The CLAUDE.md interview prompt is identical in both guides

- [ ] **Step 2: Fix any issues found and commit**

```bash
git add -A
git commit -m "Final review: fix any inconsistencies across platform guides"
```

(Skip this commit if no issues were found.)
