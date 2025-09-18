# 🔐 Enable 2FA the Right Way (GitSwamped)

This short guide helps students/teammates turn on **strong** 2FA so your org can safely require it and (optionally) disallow SMS.

---

## ✅ What we recommend
1. **Authenticator app (TOTP)** — Microsoft Authenticator, Authy, or Google Authenticator.
2. **Passkey or Security Key** — Windows Hello, Touch ID, or a hardware key (e.g., YubiKey).
3. **Recovery codes** — Save them offline (password manager notes, printed page in a safe place).

> Why no SMS? SMS can be intercepted or SIM‑swapped. App codes or passkeys are stronger.

---

## 🧭 Steps (1–3 minutes)

### 1) Add an authenticator app
- GitHub → **Settings → Password and authentication → Two‑factor authentication**.
- Click **Enable two‑factor authentication** → **Set up using an app**.
- Scan the QR code in your authenticator app and enter the 6‑digit code to verify.

### 2) Add a passkey (optional but recommended)
- On the same page, choose **Add a passkey**.
- Use Windows Hello, Touch ID, an external key, or a password manager that supports passkeys.

### 3) Save recovery codes
- Click **Download** or **Print** your recovery codes.
- Store them where you can reach them if your phone is lost.

### 4) Remove SMS 2FA (if present)
- If you previously enabled **Text message (SMS)**, remove it after adding the app/passkey:
  - **Settings → Password and authentication → Two‑factor methods → Text message → Remove**.

---

## 🧑‍🏫 For org owners (GitSwamped)
Once everyone has an app/passkey:
1. Org → **Settings → Security/Authentication** → **Require two‑factor authentication**.
2. (Optional) Enable the **secure methods only** policy (disallows SMS).
3. Review the “impacted users” list; anyone without strong 2FA will be prompted to fix it.

---

## 🧯 Common gotchas
- **New phone?** Re‑enroll your authenticator *before* wiping the old one (most apps support account transfer or backup).
- **Time drift errors (codes not working)?** Sync time on your phone and computer.
- **Locked out?** Use a recovery code or ask an org owner to temporarily remove the 2FA requirement until you recover access.

---

## 🛠 Quick blurb to paste in course docs
> Turn on 2FA with an **authenticator app** (not SMS). Add a **passkey** if possible and store **recovery codes** safely. If SMS was enabled, remove it after adding a stronger method. Our org may enforce “secure methods only,” which disallows SMS.
