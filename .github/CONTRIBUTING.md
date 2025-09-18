# 👥 Contributing Guide – GitSwamped  

Welcome to **GitSwamped**! This is a sandbox repo for practicing Git and GitHub workflows together.  
The purpose here is to **learn by doing** — so don’t stress about perfection.  

---

## 📂 Project Structure

```
docs/        → Guides, screenshots, and resources  
examples/    → Practice files (intros, hello worlds, etc.)  
src/         → Placeholder for project code  
tests/       → Example test files  
.github/     → CODEOWNERS, issue/PR templates, git config/message templates  
```

---

## 🔧 Git Workflow (with quick explanations)

1) **Clone the repo**
   ```bash
   git clone https://github.com/<your-username>/GitSwamped.git
   cd GitSwamped
   ```
   > **What this does:** Downloads the repository and enters the folder.  
   > **Why it matters:** Gives you a local working copy you can edit and commit.

2) **Create a branch**
   ```bash
   git checkout -b your-name-feature
   ```
   > **What this does:** Creates and switches to a new branch.  
   > **Why it matters:** Keeps your work isolated until it’s reviewed/merged.

3) **Make changes**
   - Add a practice file in `examples/`  
   - Or update docs with screenshots/notes  
   > **Tip:** Use the VSCode Source Control pane to stage/commit if you prefer GUI.

4) **Commit your work**
   ```bash
   git add .
   git commit -m "Add intro for <name>"
   ```
   > **What this does:** Adds changes to the next snapshot and records them.  
   > **Why it matters:** Commits are your “save points” with messages explaining intent.

5) **Push your branch**
   ```bash
   git push -u origin your-name-feature
   ```
   > **What this does:** Uploads your branch to GitHub and sets the **upstream**.  
   > **Why it matters:** The `-u` flag tells Git which remote branch to track, so future `git push` / `git pull` work without extra arguments.

6) **Open a Pull Request (PR)**  
   - GitHub → **Compare & pull request**  
   - Assign a reviewer (or self-review in sandbox mode)  
   - Merge into `main` once approved  
   > **What this does:** Starts code review and merges work into the shared branch.  
   > **Why it matters:** PRs keep `main` clean and make collaboration transparent.

---

## 🧠 Commit Messages

- Keep them short but clear:
  ```bash
  git commit -m "Add hello world example in Python"
  ```
- See the optional template below for a structured format.

---

## 📝 Optional: Commit Message Template  

I’ve included a reusable commit message template in `/.github/gitmessage.txt`.  
This helps you structure commits clearly and consistently.  

### Step 1. Copy the files locally  
- Copy these two files from the repo:  
  - `/.github/gitmessage.txt` → rename to `.gitmessage`  
  - `/.github/gitconfig.txt` → rename to `.gitconfig` (only if you want to override your global config; optional)  

Best place to store them: your **home directory**.  
- On Windows: `C:\Users\<YourName>\`  
- On macOS/Linux: `/Users/<YourName>/` or `/home/<YourName>/`  

### Step 2. Tell Git to use the template  
Run this command (adjust the path if needed):  

```bash
git config --global commit.template ~/.gitmessage
```
On Windows (PowerShell):  
```powershell
git config --global commit.template "C:\Users\<YourName>\.gitmessage"
```

### Step 3. Using the template  
Run:
```bash
git commit
```
Git opens your editor (VSCode if configured). Fill out the template and save.

---

## 🔁 Daily Sync Routine

Before starting new work, always pull the latest changes:

```bash
git checkout main
git pull origin main
git checkout your-branch-name
git merge main
```
> **Why:** Minimizes conflicts by rebasing/merging `main` into your work early and often.

---

## 🧭 VSCode: How it knows your branch (and what “origin” is)

- VSCode shows your **current branch** in the blue Status Bar (bottom-left).  
- Under the hood, Git records your active branch via the **`HEAD`** pointer.  
  - Inspect it: open `.git/HEAD` (you’ll see something like `ref: refs/heads/main`).  
  - CLI: `git rev-parse --abbrev-ref HEAD`
- **origin** is just the default name of the **remote** on GitHub.  
  - Your local branch can **track** a remote branch (its **upstream**).  
  - See which upstream you’re tracking:  
    ```bash
    git rev-parse --abbrev-ref --symbolic-full-name @{u}
    ```
  - Set/replace upstream explicitly:  
    ```bash
    git branch -u origin/main
    # or the first time you push:
    git push -u origin your-branch
    ```

---

## 💬 Need Help?

- Ask in our group chat or drop a comment on the PR.  
- Mistakes are expected here, fixing them is part of the learning process!  

---
