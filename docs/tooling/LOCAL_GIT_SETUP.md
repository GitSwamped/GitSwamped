# Local Git Setup — Global‑first (Beginner Friendly)

This guide walks you through setting up the **commit message template** for your machine.  
Use a **global setup** so it just works in every repo you use.

> I also include an *advanced per‑repo* option at the end. Skip it on your first run.

---

## Prereqs
- **Git** installed → check with: `git --version`
- **VS Code** installed (recommended)

Open a terminal:
- **Windows:** PowerShell
- **macOS/Linux:** Terminal

> All commands below assume you start **in the root of the GitSwamped repo** you cloned (`cd` into it first).

---

## Step 1 — Copy the provided files to your home folder

### Windows (PowerShell)
```powershell
Copy-Item .github\commit-template.txt $env:USERPROFILE\.commit-template
Copy-Item docs\tooling\gitconfig.example $env:USERPROFILE\.gitconfig
```

### macOS / Linux (Terminal)
```bash
cp .github/commit-template.txt ~/.commit-template
cp docs/tooling/gitconfig.example ~/.gitconfig
```
Note the above commands set the name of the local file to be different than the name of the file you are copying from the repo. 

Be sure to open the file once copied, and update your unique [user] information.

### Optional Alternative 
```bash
#    Review our example Git config
#    Open your global Git config in an editor and copy any pieces you want
#    from docs/tooling/gitconfig.example (e.g., core.editor, user.name/email).
git config --global -e
```

> **Note:** In `docs/tooling/gitconfig.example`, the line `editor = code --wait` tells Git to open VS Code for commit messages. Keep it if you want VS Code to be the editor you create your commit messages in; remove it if you prefer another editor.

---

## Step 2 — Tell Git to use the template (global)

### Windows (PowerShell)
```powershell
git config --global commit.template "$env:USERPROFILE\.commit-template"
```

### macOS / Linux
```bash
git config --global commit.template ~/.commit-template
```

Verify it’s set:
```bash
git config --show-origin --get commit.template
# should print: (global file path)  ~/.commit-template
```

---

## Step 3 — Use the template

In any Git repo on your machine:
```bash
git commit
```
Git opens your editor with the template. Fill it out, save, close → commit completes.

---

## Troubleshooting

- **Template didn’t appear?** Re‑run Step 2 and check the verify command.
- **Windows path issues?** Quote the path: `"$env:USERPROFILE\.commit-template"`.
- **Commit opens in the wrong editor?** Open `gitconfig.example` and copy the `core.editor = code --wait` line into your global config (`git config --global -e`).
- **Can't find .gitconfig on your local machine?** Enable show hidden items in your file viewer.

---

## Advanced (optional) — Per-repo commit template

Use this only if you want a **specific repo** to have its own template (overriding your global one). Git will use the value stored in **that repo’s** `.git/config` when you run commands inside it.

### A) If the repo already has a template file
Check the path and then set it (relative paths are portable):

- **Windows (PowerShell)**
```powershell
Get-Item .github\commit-template-file  # or any path in this repo
git config --local commit.template .github/commit-template-file
git config --show-origin --get commit.template  # should show .git/config
```
- **macOS / Linux**
```bash
ls .github/commit-template-file        # or any path in this repo
git config --local commit.template .github/commit-template-file
git config --show-origin --get commit.template  # should show .git/config
```
You can use any path inside the repo (e.g., commit-template.txt at the root or docs/commit-template.txt). .github/ is just a convention.

### B) Use a file outside the repo (not portable, but valid)
If you insist on a home-folder template for a particular repo, add your own `commit-template-file` to your local home directory. Then, from the root of the repo you want it applied to:

Windows
```powershell
git config --local commit.template "$env:USERPROFILE\commit-template-file"
```
macOS / Linux
```bash
Copy code
git config --local commit.template ~/commit-template-file
```

### D) One-off (just for a single commit)
```
git commit -t path/to/template
```

Verify / Undo
```bash
git config --show-origin --get commit.template   # see the exact file and where it’s set
git config --local --unset commit.template       # remove per-repo override
```

Precedence: local (repo) overrides global.

> How Git decides where to store settings: when you run `git config` **inside a repo**, it writes to that repo’s `.git/config` (local). With `--global`, it writes to your `~/.gitconfig`. **Local overrides global.**

---

## Tip

- Not using `gitconfig.example`? Set your identity:

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.edu"
```
