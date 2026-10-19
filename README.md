# RimRunnerVermont

Unofficial Vermont HS boys basketball ratings. Not affiliated with the VPA or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerVermont/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
63 teams: the VPA boys basketball schools on MaxPreps, in the VPA 2026-27 divisions (VPA Basketball Guide, divisional alignment sheet):
D1 14, D2 14, D3 16, D4 19. Danville and Twinfield (one "Danville/Twinfield/Cabot" line on the sheet) play as separate MaxPreps teams;
Northfield, Williamstown and Mid Vermont Christian (2026 VPA D4 bracket teams, not on the sheet) stay D4; Rivendell Academy (Orford, NH)
is a VPA member. No Other (non-VPA) programs met the 8-game rule. Conferences = each school's MaxPreps 2026-27 league (8: Metro, Capital,
Lake, Mountain, SVL - A, SVL - B, SVL - C, SVL - D). The VPA has no leagues; Enosburg Falls, Hazen, Middlebury, Mid Vermont Christian and
Winooski have no MaxPreps league and are independents.

## Season rule
VPA 2026-27 Basketball Guide: practice opens Nov 30, 2026; games may begin Fri Dec 11, 2026. Games involving a VPA school before that date
are left out (schedule build and nightly updater); games between two non-VPA schools are kept. A school listed against itself is never a game.
Boys: last regular-season date Feb 27; playdowns Mar 2-3, quarterfinals Mar 5-6, semifinals Mar 8-11, finals Mar 12-13, 2027.

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 04:30 and 12:00 UTC (11:30 pm / 7:00 am Eastern standard time) and
on manual dispatch. Before `SEASON_START` in index.html (the first game on the MaxPreps schedules) the script makes no requests. From then on it
reads boys basketball finals for the last 3 days from the MaxPreps Vermont scores-by-date page (team-page fallback), matches them to the schedule
by MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo
from those finals. It commits only when data changed; GitHub Pages updates from the commit.
