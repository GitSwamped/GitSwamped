# 📘 GLOSSARY – GitSwamped

**Branch** — A movable pointer to a series of commits. Lets you work on changes without affecting `main` until you merge.

**HEAD** — Git’s pointer to your current checkout (usually a branch).  
- View: `git rev-parse --abbrev-ref HEAD`  
- File: `.git/HEAD`

**Remote** — A repository hosted elsewhere (e.g., GitHub). The default remote name is **origin**.

**Upstream / Tracking branch** — The remote branch your local branch is linked to.  
- Set it: `git push -u origin your-branch`  
- Change it: `git branch -u origin/main`

**Clone** — Download a remote repo to your machine (`git clone ...`).

**Fork** — Your own copy of someone else’s repo on GitHub. You usually clone *your fork*.

**Stage** — Mark changes to include in the next commit (`git add`).

**Commit** — Record a snapshot of staged changes with a message explaining *what/why*.

**Push** — Send your local commits to the remote (`git push`).

**Pull** — Get remote commits into your local branch (`git pull` = fetch + merge).

**Fetch** — Update your remote-tracking refs without merging (`git fetch`).

**PR (Pull Request)** — A GitHub review workflow to propose merging changes into another branch (commonly `main`).

**.gitignore** — A config file listing files/paths Git should not track (e.g., `node_modules/`, `.env`).

**Line endings (CRLF vs LF)** — Windows uses CRLF; Linux/macOS use LF. Git can normalize via `core.autocrlf`.  
- Windows recommended: `git config --global core.autocrlf true`

**SSH vs HTTPS** — Two ways to authenticate to GitHub.  
- HTTPS often uses a **Personal Access Token (PAT)**.  
- SSH requires adding your public key to GitHub.

**Rebase vs Merge** — Two ways to integrate changes from `main` into your branch. For the sandbox, merging is fine.
