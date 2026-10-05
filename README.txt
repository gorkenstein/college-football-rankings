AP EXTENDED RANKINGS + FULL H2H UPDATE

WHAT CHANGES
============
1. Every team receiving AP votes is treated as an extended sequential ranking:
   AP Top 25 = ranks 1-25, then "Others receiving votes" = 26, 27, 28, 29, etc.

2. The next ballot automatically contains EVERY AP vote-getter in that order.

3. The website displays the source rank after each team name, for example:
   Georgia (2), Kentucky (26), North Dakota State (35).
   The rank is DISPLAY ONLY; the clean team name is still stored in ballots.

4. Head-to-head now includes games where BOTH teams are anywhere in the
   current AP vote-receiving pool, not just Top 25 teams.

5. CFBD refresh now loads FBS + FCS games so North Dakota State is covered.

6. Scored ballots can show extended AP ranks beyond 28. The scoring formula
   itself remains unchanged: ballot positions 1-25 are scored, and any
   official rank beyond 28 is -1.

TIE POLICY
==========
When two ORV teams have the same vote total, use the exact order AP displays
them so every team has one deterministic sequential rank. On Oct. 4,
Minnesota and Arizona both had 19 votes; AP listed Minnesota first, so the
pool uses Minnesota (32) and Arizona (33).

INSTALL ORDER
=============
STEP 1 — Supabase SQL Editor
Run: 07_extended_ap_rankings.sql
This also seeds the current Oct. 4 poll into the next open ballot.

STEP 2 — Supabase Edge Function: refresh-games
Replace the entire function with: refresh-games-v3-index.ts
Keep Verify JWT OFF. Deploy.

STEP 3 — Supabase Edge Function: score-week
Replace the entire function with: score-week-v5-index.ts
Keep Verify JWT OFF. Deploy.

STEP 4 — GitHub Pages
Replace:
  index.html
  version.json

STEP 5 — Refresh current ballot game/H2H data now
In Supabase SQL Editor run: 08_refresh_current_ballot_games.sql
Wait about 15 seconds, then inspect net._http_response.

EXPECTED CURRENT OCT. 4 EXTENDED RANKS
======================================
26 Kentucky
27 Wake Forest
28 Wisconsin
29 Duke
30 Northwestern
31 Nebraska
32 Minnesota
33 Arizona
34 James Madison
35 North Dakota State

After GitHub Pages updates, reload the site. The current ballot should be
seeded from the Oct. 4 AP poll and team names will display their source rank.
