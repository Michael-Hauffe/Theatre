# Ghost Matinee: notes for anyone (human or AI) changing this code

## House rules

1. **Comment heavily. This applies to all code, now and in the future.**
   - Every section starts with a header comment explaining what it is for.
   - Every function gets a comment saying what it does, in plain words.
   - Any line whose purpose isn't obvious gets an inline comment explaining *why*.
   - Write comments for someone who is not a programmer but wants to follow along.
   - When you change code, update the comments next to it in the same edit.
2. **Keep the shortcut sheet in sync.** If you add or change a keyboard shortcut in the
   script, update the `#keySheet` list in the HTML too.
3. **Keep the admin command list in sync.** New `/admin` commands go in `ADMIN_HELP`
   (what `/admin show commands` shows), `parseAdmin()`, `execAdmin()` and, if everyone must
   react, `applyAdmin()`. Also add them to the table in README.md.
4. **Keep the debug screen useful.** When you add a feature with state worth checking,
   add a row for it in `dbgRows()`.
5. **Change `BUILD` with every update pushed to `main`** (the `const BUILD` line in the script,
   e.g. "v2.2 · date" -> "v2.3 · date"). Players' pages compare it with the website to offer a
   Refresh when they're running an old saved copy; if it doesn't change, nobody gets told.
6. **Never change the `-working` branches.** `v1.0-working` and `v2.0-working` hold versions
   the owner confirmed working (both on November 1, 2026). New work goes on `main`. When the
   owner confirms a new version, save it as a new `vX.Y-working` branch and list it in README.md.

## How the project is laid out

- `index.html` is the whole game: styles, HTML and script in one file. The top of the
  file has an overview, and each section of the script has its own header comment.
- `posters/` holds every lobby poster as an image file; `posters/posters.json` lists which
  ones are in the rotation, in order (the order sets the "image" numbers for admin commands).
- `tools/poster-maker.html` draws the 20 built-in posters with code and offers each as a JPG
  download. The game doesn't use it; it's for making or editing posters.
- The site is served by GitHub Pages straight from the `main` branch.

## Things that are easy to get wrong

- `<!doctype html>` must stay the very first line of `index.html`.
- Library versions are pinned (three.js r128, PeerJS 1.5.4). Upgrading three.js
  changes APIs used throughout; test thoroughly if you do.
- Every message from other players is untrusted. Pass text through `clean()` and
  numbers through `num()` / `clamp()` before using them, and never insert it as HTML.
- The room host's browser is the referee for the projector. All claims go through
  `hostProjRequest()`; don't let other players change `proj` directly.
