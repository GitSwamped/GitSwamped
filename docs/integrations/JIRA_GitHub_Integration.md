# 🔗 Jira ↔ GitHub Integration Guide (GitSwamped)

This guide shows how to connect a GitHub repository to a Jira Cloud project and use **issue keys** + **Smart Commits** to auto‑link branches, commits, and pull requests — and (optionally) transition issues, add comments, and log time from your commit messages.

> TL;DR: install **GitHub for Jira**, connect your repo, include your Jira issue key (e.g., `SWMP-12`) in your **branch names, commit titles, and PR titles**. Jira will do the rest.

---

## ✅ What you get after integrating
- A **Development** panel on each Jira issue showing branches, commits, and PRs.
- Links on GitHub PRs to the related Jira issue(s).
- Optional **Smart Commits** to transition issues, add comments, and log time from git.
- Automatic traceability from idea → code → review → merge.

---

## 🧰 Prerequisites
- **Jira Cloud** project and you know its project key (e.g., `SWMP`).
- A GitHub repository you have admin access to (or your org admin can approve the app).
- Permission to install Jira apps on your site (or ask a Jira admin to do Step 1).

---

## 1) Install the “GitHub for Jira” app (Jira Cloud)
1. In Jira, go to **Apps → Explore apps**.
2. Search for **“GitHub for Jira”** (publisher: Atlassian).
3. Click **Install** → **Get started**.
4. In the app config screen, click **Connect GitHub organization/account** and authorize.
5. Select the **repositories** you want to link (you can choose a single repo for a class project).

> ⏳ First‑time sync can take a few minutes while it indexes your repos.

**Screenshot placeholders (add later in `docs/images/`):**
- `docs/images/jira_install_marketplace.png`
- `docs/images/jira_github_connect.png`
- `docs/images/jira_select_repos.png`

---

## 2) Verify the connection
- Open a Jira issue (e.g., `SWMP-12`). You should see an empty **Development** panel.  
- In GitHub, open your repo → **Settings → Integrations** (or “Installed GitHub Apps”) and confirm **GitHub for Jira** has access to this repo.
- Make a tiny test commit that references the issue key (see examples below) and push; refresh the Jira issue after a minute.

---

## 3) Use the issue key everywhere (best practice)
Include your issue key **exactly** as shown in Jira (uppercase + hyphen + number) in:
- **Branch names** (recommended pattern)
  ```text
  feature/SWMP-12-jira-linking-guide
  bugfix/SWMP-34-fix-typo
  docs/SWMP-56-contributing-notes
  ```
- **Commit titles** (first line)
  ```text
  SWMP-12 Add first draft of Jira linking guide
  ```
- **PR titles**
  ```text
  SWMP-12: Add Jira ↔ GitHub integration guide
  ```

> The key can appear anywhere in the title, but putting it **first** is the most reliable and readable.

---

## 4) Smart Commits (optional power‑ups)
Smart Commits let you **transition issues**, **add comments**, and **log time** from your commit messages.

### Common patterns
```text
SWMP-12 #comment First pass; screenshots coming later
SWMP-12 #time 1h 30m Documented setup and verification
SWMP-12 #transition In Progress
SWMP-12 #transition Done
```

- `#comment <text>` — adds a comment to the issue.
- `#time <duration>` — logs time (e.g., `30m`, `1h 15m`, `2h`).
- `#transition <Status Name>` — moves the issue along your workflow.  
  - The status name must match your Jira **transition** label (capitalization/spaces matter).  
  - Some projects use shorthand transitions like `#done` or `#in-progress` if those transitions exist; if not, prefer `#transition <Exact Name>`.

> ⚠️ Smart Commits **run as the Jira user** mapped to the commit author. If your commit email isn’t associated with a Jira user, linking still works, but transitions/time logging may be skipped. Add your GitHub email to your Jira profile if needed.

---

## 5) VS Code + commit template
If you use our optional commit template (`/.github/gitmessage.txt`):
- Put the **issue key in the first title line**.
- Example title line:
  ```text
  SWMP-12 Add Jira linking guide #comment Draft with placeholders
  ```
- See **CONTRIBUTING.md → “Commit Message Template”** for setup steps.

---

## 6) Branch protection + PR hygiene (nice to have)
- Require PRs to **main** and at least one review (even self‑review in a sandbox).
- Encourage PR titles to **start with the issue key**.
- Keep PRs small; one issue per PR is easiest to trace.

---

## 7) Troubleshooting checklist
- **No links in Jira?**  
  - App installed? Repo selected in the app settings? Wait 1–5 minutes after pushing.  
  - Is the **issue key present** in the branch/commit/PR title? (Must be the real key like `SWMP-12`, not “SWMP12”.)  
  - Is the repo **private**? Ensure the app has access to that private repo.
- **Smart Commits didn’t transition/comment?**  
  - Does your commit email match a Jira user with permission to transition that issue?  
  - Does your workflow include a transition matching the text you used? If not, use `#transition <Exact Status Name>`.
- **Forks / personal clones**  
  - If you push from a forked repo, that fork **also** needs to be connected in the app (or push branches to the main repo instead).
- **Multiple Jira sites**  
  - Make sure you installed the app on the **same** Jira site that hosts your project (e.g., `yourteam.atlassian.net`).

---

## 8) Security & scope tips
- Only grant the app access to the repositories you intend to link.  
- You can disconnect repos later from the app’s settings.  
- Organization admins can centrally manage which repos are connected.

---

## 9) Quick examples you can copy

**Create a branch (include key):**
```bash
git checkout -b feature/SWMP-12-jira-linking-guide
```

**Commit with a Smart Commit:**
```bash
git add docs/JIRA_GitHub_Integration.md
git commit -m "SWMP-12 Add Jira ↔ GitHub integration guide #comment Draft; screenshots placeholders added"
git push -u origin feature/SWMP-12-jira-linking-guide
```

**Open a PR (title includes key):**
```
SWMP-12: Add Jira ↔ GitHub integration guide
```

After pushing, refresh the Jira issue — you should see your branch/commit/PR under **Development**.

---

## 10) File locations in this repo
- This guide: `docs/JIRA_GitHub_Integration.md` (move it there after commit).  
- Screenshots: add to `docs/images/` and update the placeholders above.  
- Commit template: `/.github/gitmessage.txt`  
- Optional git config sample: `/.github/gitconfig.txt`

---

Happy linking! If something’s unclear, open an issue or ask in chat — we’ll swamp‑walk it together. 🐊
