# Setting Up GitHub CLI, Docker, and Desktop Commander

Three independent installs, all done on your own Windows PC — I can't run these myself since my access to your computer only reaches a sandboxed folder bridge, not your real OS. Do them in any order. About 15–20 minutes total, mostly waiting on Docker's restart.

**Before you start:** open **PowerShell** (search "PowerShell" in the Start menu). You don't need Admin mode for GitHub CLI or Desktop Commander; Docker's installer may prompt for it on its own.

---

## 1. GitHub CLI (`gh`)

Gives you GitHub from the command line — cloning, PRs, issues, auth — without needing a browser for most of it.

1. Install it:
   ```
   winget install --id GitHub.cli
   ```
2. Close and reopen PowerShell (so it picks up the new PATH entry).
3. Check it installed:
   ```
   gh --version
   ```
4. Log in:
   ```
   gh auth login
   ```
   Pick: **GitHub.com** → **HTTPS** → **Login with a web browser**. It'll show a one-time code and open your browser — paste the code and approve.
5. Confirm:
   ```
   gh auth status
   ```
   Should show you're logged in as your GitHub account.

---

## 2. Docker Desktop

Lets you build and run containers locally.

1. Install it:
   ```
   winget install --id Docker.DockerDesktop
   ```
2. **Restart your computer** when prompted — Docker needs WSL2, and Windows usually needs a reboot to finish turning it on.
3. After rebooting, open **Docker Desktop** from the Start menu and accept the service agreement. Wait for it to say "Engine running" in the bottom left.
4. Verify from PowerShell:
   ```
   docker --version
   docker run hello-world
   ```
   The second command should end with a "Hello from Docker!" message.

   If it complains that WSL2 isn't installed:
   ```
   wsl --install
   ```
   then reboot once more and retry.

---

## 3. Desktop Commander (gives me real control of your PC)

This is a small local server that runs on your machine and lets me actually execute commands and edit files directly on your Windows OS — not just the limited folder bridge I've been using so far. Once it's connected, I can finish verifying GitHub/Docker myself, install VS Code extensions, and generally do a lot more without you running commands by hand.

1. In PowerShell:
   ```
   npx @wonderwhy-er/desktop-commander@latest setup
   ```
   - If `npx` isn't recognized, you need Node.js first: `winget install --id OpenJS.NodeJS.LTS`, reopen PowerShell, then retry the command above.
   - If it asks to install a package the first time, type `y`.
2. The setup script edits Claude Desktop's config automatically and tells you when it's finished.
3. **Fully quit Claude Desktop** — right-click its icon in the system tray and choose Quit (just closing the window isn't enough) — then reopen it.
4. Start a new chat and ask something like "what OS am I running, and what's my hostname?" If Desktop Commander connected successfully, it'll answer using its own tools instead of saying it can't check.

---

## When you're done

Come back and tell me what succeeded, or paste any error messages you hit. Once Desktop Commander is live I can verify GitHub CLI and Docker myself and take over the remaining setup (VS Code extensions, resuming the GitHub Pages automation, etc.) directly.
