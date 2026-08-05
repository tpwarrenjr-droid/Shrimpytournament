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

## 2. Turn on keywords (recommended)

Captains typing a word beats captains keeping a link. This needs a database that
lets records be named, which takes about four minutes once:

1. https://console.firebase.google.com -> **Add project** (skip Analytics).
2. **Build -> Realtime Database -> Create Database**, pick a region,
   **Start in test mode**.
3. Copy the URL at the top (`https://your-project-default-rtdb.firebaseio.com`).
4. Paste it between the quotes on the `const DB_URL = "";` line near the top of
   the script in `index.html`.
5. On the **Rules** tab, replace the contents with:

   ```json
   { "rules": { "boards": { "$b": { ".read": true, ".write": true } } } }
   ```

   (Test mode expires after 30 days; this doesn't.)

Now the app asks for a keyword instead of a link. You pick one, hand it to the
five captains, and they type it in. Skip this and the app still works — boards
just get a random ID shared by link instead.

## 2b. Start the board and share it

Open your link. You'll be asked to **start a new board** or **join** one with a
code. Start one, then tap **Copy share link** and send that link to all 20
players. Everyone who opens it sees the same scores, refreshing every three
seconds.

The board code shows next to the Copy button. **Write it down.** Anyone can get
back into the tournament by pasting that code into the join box, even if they
lose the link.

The page never creates a board on its own, so a stray visit can't strand your
tournament.

## 3. Everyone adds it to their home screen

Tell people to open your link first, then:

- **iPhone (Safari)** — Share button -> **Add to Home Screen** -> Add.
  It must be Safari; Chrome on iOS can't install it.
- **Android (Chrome)** — a prompt usually appears. If not: menu (three dots) ->
  **Install app** or **Add to Home Screen**.

It opens full screen with no browser bars. Each device remembers its board, so
the app rejoins your tournament on launch. If it ever asks which board to use,
paste the code — nothing is lost.

## Day of

- **Teams** — paste the 20 names, hit Draw teams.
- **Golf** — enter each team's scramble total. 4 / 3 / 2 / 1 / 0 by finish.
- **Games** — each game has its own schedule and its own format. Set **teams per
  match** (2-5), **rounds**, and **points per win** on the Format panel. Two
  teams per match gives head-to-head with a bye; five gives one match with
  everyone in it. The panel tells you the most a team can score, so you can
  balance games against golf. Changing teams-per-match clears that game's
  results, since the schedule changes shape.
- **Board** — the running total.

Tap **How to use** at the top for the captain's instructions, in the app.

Rename a game by tapping its name. Add games at the bottom of the Games tab;
they get the same format and the same 4-point ceiling.

Anyone can enter anything from any phone at any time. Entries merge field by
field, so two people saving at the same moment can't overwrite each other — if
you enter a golf score while someone else taps a Beer Dye winner, both stick.
Only the exact same field edited twice resolves to whoever tapped last.

Lose signal mid-round and the app keeps working. Entries queue on your phone and
push automatically when you're back in range. The footer badge reads **live**,
**syncing** or **offline** so you always know where you stand.

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
