# Tournament Board

Live scoring for a 20-player, 5-team tournament: one golf scramble plus any
number of drinking games. Every event is worth up to 4 points.

Installs to the home screen and runs full screen like a real app.

## 1. Put it online

1. Create a new **public** repo on GitHub.
2. Upload everything in this folder (keep the `icons` folder intact).
3. **Settings -> Pages -> Source: Deploy from a branch**, branch `main`,
   folder `/ (root)`. Save.
4. Wait a minute, then open `https://YOUR-NAME.github.io/YOUR-REPO/`

## 2. Share it

The first time the page opens it creates a shared board and adds an ID to the
address bar, like `?board=a1b2c3`.

**Tap "Copy share link" and send that link to all 20 players.** Everyone who
opens it sees the same scores, refreshing every three seconds.

Send the link *with* the `?board=` part. A bare URL creates a brand new empty
board instead of joining yours.

## 3. Everyone adds it to their home screen

Tell people to open your link first, then:

- **iPhone (Safari)** — Share button -> **Add to Home Screen** -> Add.
  It must be Safari; Chrome on iOS can't install it.
- **Android (Chrome)** — a prompt usually appears. If not: menu (three dots) ->
  **Install app** or **Add to Home Screen**.

It opens full screen with no browser bars. The board ID is remembered on the
device, so the app rejoins your tournament even though the home screen shortcut
drops the `?board=` part.

## Day of

- **Teams** — paste the 20 names, hit Draw teams.
- **Golf** — enter each team's scramble total. 4 / 3 / 2 / 1 / 0 by finish.
- **Games** — tap winners. Round robin, 1 point per win, 4 max per game.
- **Board** — the running total.

Rename a game by tapping its name. Add games at the bottom of the Games tab;
they get the same format and the same 4-point ceiling.

The badge in the footer shows how fresh your copy is — tap it to refresh now.
If two people edit at once the later save wins, so split up who enters what.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest` | Makes it installable, sets the name and colors |
| `sw.js` | Caches the app shell so it opens instantly on bad signal |
| `icons/` | Home screen icons |

## Notes

- Scores live on jsonblob.com, a free public JSON store. No account needed, but
  anyone with your link can edit and there's no uptime guarantee. Fine for a
  tournament, not for anything you can't afford to lose.
- Scores are never cached — only the page itself is. A dead signal means the app
  still opens, but the board won't update until you're back online.
- To run it on your own database instead, put a Firebase Realtime Database URL
  in the `DB_URL` line near the top of the script in `index.html`.
- If you change `index.html` later, bump `tournament-shell-v1` to `-v2` in
  `sw.js` so everyone's installed app picks up the new version.
