# ✦ Sealnote

> **Encrypted notes that even the developer can't read.**

A single HTML file. No server. No cloud. No installation. Open it and start writing — your notes are encrypted on your device and never leave it.

---

## How it works

When you create a note, it is encrypted in your browser using AES-256-GCM before being saved. Your password never leaves your device. The encryption key is derived locally using PBKDF2 with 600,000 iterations. Even if someone copies your entire browser data folder, they cannot read a single word without your password.

---

## Features

- **Zero Knowledge** — your notes are encrypted before saving. No one can read them but you.
- **No server** — everything happens locally in your browser. There is nothing to breach on our end.
- **Single file** — the entire app is one `sealnote.html` file. No installation, no dependencies.
- **Works offline** — after the first load, the app runs fully without internet.
- **Rich text editor** — bold, italic, headings, lists, links, images, and more.
- **Image support** — drag & drop, paste, or upload images. Auto-compressed before saving.
- **Pin & color notes** — organize your notes visually. Both are stored encrypted.
- **Sort & search** — sort by newest, oldest, A→Z, or Z→A. Search across all notes instantly.
- **Export notes** — export any note as Markdown, HTML, or plain text.
- **Import notes** — import `.md`, `.txt`, or `.html` files directly.
- **Encrypted backup** — export all your notes as a single encrypted `.sealnote` file.
- **Restore backup** — import a `.sealnote` backup on any device or browser using your password.
- **Backup reminders** — a badge warns you when your last backup is getting old.
- **Auto-save** — notes save automatically as you type.
- **Session timeout** — auto-logout after 15 minutes of inactivity.
- **Security guide** — built-in guide explaining what the app protects and what it does not.

---

## Security

| Property | Implementation |
|---|---|
| Encryption | AES-256-GCM |
| Key derivation | PBKDF2 × 600,000 iterations, SHA-512 |
| Password verification | PBKDF2 × 100,000 iterations, SHA-256, independent salt |
| IV | 12-byte random, unique per encryption operation |
| Metadata (pin, color) | Encrypted — not visible in IndexedDB |
| Timing attack protection | DUMMY_SALT ensures constant-time response |
| Brute force protection | Progressive lockout: 30s → 2min → 10min → 30min |
| XSS protection | DOMPurify with strict tag and URI allowlists |
| Content Security Policy | `object-src none`, `base-uri self` |
| Session | Auto-expires after 15 minutes of inactivity |

All encryption runs in your browser using the native [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API). No third-party crypto libraries.

---

## Limitations

These are honest trade-offs, not bugs.

- **Notes are stored per browser.** Chrome and Edge have separate storage. Use Export All to move notes between browsers or devices.
- **No sync between devices.** Your notes live on one device. Backup + import is the only way to transfer them.
- **No mobile app.** The app runs in a browser only. There is no iOS or Android version.
- **Clearing browser data deletes your notes.** IndexedDB is wiped when you clear browser history or site data. Always keep a backup.
- **If your device is compromised, your notes can be read.** Encryption protects data at rest. If an attacker runs malware on your device, they can capture your password or read memory directly. This is a fundamental limit of all client-side apps, not specific to Sealnote.
- **No collaboration.** Notes are single-user only.
- **`unsafe-inline` in CSP.** Required by the single-file architecture. Separating JS into an external file would remove this limitation.

---

## Usage

1. Download `sealnote.html`
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari)
3. Create an account with a strong password
4. Start writing

That is it. No sign-up, no email, no tracking.

> **Tip:** If you can't find your backup file in the import dialog, type the filename (e.g. `sealnote_backup`) in the search box and press open.

---

## Backup & restore

Your notes exist only on your device. Regular backups are strongly recommended.

**To back up:** Click ⚙ → **Export all notes** → save the `.sealnote` file somewhere safe.

**To restore:** Click ⚙ → **Import backup** → select your `.sealnote` file → enter the password you used when the backup was created.

Backup files are encrypted with AES-256-GCM. They are safe to store anywhere.

---

## Open source

Every line of code is in `sealnote.html`. Your trust should be based on code you can read, not on promises.

---

## License

MIT