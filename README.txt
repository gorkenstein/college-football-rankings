OCTOBER 25 SITE RECOVERY PACKAGE

Why the site could look reverted
--------------------------------
The newest website code itself was still the cumulative Oct. 18 build, but its
last-resort built-in team list was an older AP poll. If the new open week's
pool_week_teams record was missing, the page silently used that old list, which
made the website look like an older version.

This package fixes that behavior.

What is preserved
-----------------
- Week-by-week standings columns (Week 6, Week 7, Week 8, ...)
- Clickable weekly scores and other users' scored ballots
- AP extended rankings / every ORV team
- Miami name normalization for game data
- Full vote-pool head-to-head games
- Sign-in and online ballot submission
- PDF output
- Sunday automatic game refresh
- Dated weekly AP scoring behavior

New protection
--------------
For the open ballot, the browser now tries:
1. This week's pool_week_teams record
2. The latest verified pool_polls extended ranking
3. Only then a built-in fallback

The built-in fallback is updated to the Oct. 25 poll, and the page labels which
source it used. The footer also shows:
  Site build: 2026-10-25.1

Install / recover
-----------------
1. GitHub:
   Replace index.html
   Replace version.json

2. If score-week is NOT already v7, deploy score-week-v7-index.ts
   with Verify JWT OFF.

3. If refresh-games is NOT already v4, deploy refresh-games-v4-index.ts
   with Verify JWT OFF.

4. Supabase SQL Editor:
   Run 13_force_current_score_and_seed.sql

5. Refresh the website. At the bottom, confirm:
   Site build: 2026-10-25.1

Do not upload an older index.html after this file.
