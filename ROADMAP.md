# RapidClip Roadmap

RapidClip is a single-page, no-login clipboard that syncs text, images and files (up to 50 MB) between devices through Firebase Realtime Database rooms.

This document lists features to add, grouped by purpose. Priority: **P1** = do first, **P2** = next, **P3** = later.

## 1. AdSense approval and revenue (P1)

AdSense often rejects single-page tools for "low value content". These items fix that.

- [ ] `ads.txt` at site root (done, deploy it)
- [ ] Privacy Policy page (must mention cookies, Google ads, Firebase)
- [ ] Terms of Use page
- [ ] About and Contact pages
- [ ] "How it works" and FAQ section on the home screen (200+ words of real text)
- [ ] Blog or guide pages, e.g. "How to copy text from phone to PC", "Send files between devices without login"
- [ ] `sitemap.xml` and `robots.txt`, then submit to Google Search Console
- [ ] Cookie consent banner for EEA/UK visitors (Google CMP or a free one)
- [ ] Don't place ads inside the room view next to buttons (accidental-click policy risk)

## 2. Security and privacy (P1)

- [ ] Firebase Realtime Database security rules: limit read/write to `rooms/$roomId`, cap value sizes, validate data shape
- [ ] Firebase App Check to stop abuse of your database from other sites
- [ ] Optional room password (hash stored, not plain text)
- [ ] Optional end-to-end encryption in the browser (Web Crypto, key kept in URL fragment)
- [ ] Auto-expiring rooms (e.g. 1 hour, 24 hours, 7 days) with cleanup via Cloud Function or scheduled job
- [ ] "Delete room now" button
- [ ] Rate limits on uploads per room
- [ ] Longer random room IDs by default (6 characters is guessable at scale)

## 3. Core clipboard features (P2)

- [ ] QR code for the room link, so a phone joins by scanning
- [ ] One-tap "Copy" and "Paste from clipboard" buttons
- [ ] Clipboard history: list of past text snippets, not only the latest
- [ ] Paste images directly with Ctrl+V into the room
- [ ] Download all files as ZIP
- [ ] Image and file previews (PDF, video, audio)
- [ ] Upload progress bar and cancel button
- [ ] Per-item expiry (self-destruct after first view or after N minutes)
- [ ] Show who is online in the room (device count)
- [ ] Text formatting helpers: code block with syntax highlighting, Markdown preview, link detection

## 4. Storage and scaling (P2)

Files are stored as base64 chunks in Realtime Database. That is costly and slow for large files.

- [ ] Move files and images to Firebase Storage (or Cloudflare R2), keep only metadata in the database
- [ ] Compress images before upload
- [ ] Set a per-room storage quota and show usage
- [ ] Monitor Firebase usage and billing alerts

## 5. UX and design (P2)

- [ ] Light/dark theme toggle (the `data-theme` attribute already exists)
- [ ] Installable PWA (manifest, service worker, offline shell)
- [ ] Share target, so mobile "Share" menu sends content to RapidClip
- [ ] Keyboard shortcuts (Ctrl+Enter to send, Esc to leave room)
- [ ] Recent rooms list (stored in localStorage)
- [ ] Accessibility pass: labels, focus states, contrast, screen reader text
- [ ] Multi-language support

## 6. SEO and growth (P2)

- [ ] Open Graph and Twitter card meta tags with a preview image
- [ ] Structured data (`WebApplication` JSON-LD)
- [ ] Landing pages for search terms: "online clipboard", "send text to another device", "file transfer without login"
- [ ] Fast load: lazy-load Firebase and ads, compress assets, target Lighthouse 90+
- [ ] Privacy-friendly analytics (Google Analytics 4 or Plausible)

## 7. Optional accounts and monetization (P3)

- [ ] Optional sign-in (Google) to keep persistent rooms
- [ ] Pro tier: larger files, longer retention, no ads, custom room names
- [ ] Browser extension and desktop app for one-click send
- [ ] Public API or CLI (`rapidclip send file.txt`)

## Suggested order

1. Policy pages, FAQ content, sitemap, consent banner (AdSense approval).
2. Firebase security rules and room expiry.
3. QR code, history, paste-image, light theme, PWA.
4. Move file storage off Realtime Database.
5. Accounts and Pro tier.
