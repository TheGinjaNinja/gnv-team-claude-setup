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
