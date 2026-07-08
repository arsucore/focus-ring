# FOCUS

A precision rhythm/reaction game — tap, react, survive.

## Deploy on GitHub Pages

1. Push these three files to the root of your repo (or a `/docs` folder):
   - `index.html`
   - `manifest.json`
   - `sw.js`
2. In your repo, go to **Settings → Pages**, set the source branch/folder, and save.
3. Your game will be live at `https://<username>.github.io/<repo>/`.

That's it — no build step, no server, no environment variables needed.

## What was fixed

- **PWA manifest**: was embedded as an inline `data:` URI on the `<link>` tag. Moved to a real `manifest.json` file, which is more reliable and lets browsers/OSes fetch it normally.
- **Service worker**: was being registered from a `blob:` URL, which browsers reject for service worker scripts (registration silently failed, so offline caching never actually worked). It's now a real `sw.js` file registered with a relative scope, so it also works correctly if the site is deployed under a GitHub Pages *project* subpath (`username.github.io/repo/`) rather than a root domain.
- **Removed a leftover, unused JSONBin credential** (`JSONBIN_BIN_ID`/`JSONBIN_URL`) that was dead code from an earlier draft. It wasn't referenced anywhere, but it looked like a real secret and had no place in a public repo.
- Confirmed HTML is well-formed (balanced tags, no duplicate IDs), all `onclick`-style handlers resolve to real functions, all `getElementById` lookups resolve to real elements, and the inline JavaScript has no syntax errors.

## Note on the admin panel

Tapping the "FOCUS" title 5× opens a password-gated stats screen (`letmein67`). It only reads this browser's own local session history (`localStorage`) — nothing is sent to or fetched from a server — so the password is just a UI gate, not real access control. Fine to leave as a fun easter egg, but don't rely on it to protect anything sensitive.
