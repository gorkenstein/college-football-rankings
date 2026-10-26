WEEK 9 TIED-RANK + MIAMI FIX

ROOT CAUSES
===========
1. WEEK 9 DID NOT SCORE
The Oct. 25 AP poll contains a real tie:
  Boise State #20
  Northwestern #20
  Arizona #22

The old scorer required unique rank numbers 1 through 25, so it rejected this
valid AP poll.

This update stores both TEAM and OFFICIAL AP RANK. Tied AP ranks are now valid.
ORV still follows the pool rule: displayed vote order becomes 26, 27, 28, etc.

2. MIAMI SHOWED AS "WRITE-IN"
The site could successfully normalize Miami while loading a snapshot, then later
perform an exact string lookup such as gameResults["Miami (FL)"]. If the current
poll stored "Miami", the exact lookup failed and the UI/PDF said "Write-in."

Every last-game and H2H lookup now uses the same normalized team identity.
Also, an official poll team with missing game data now says "No game data" —
never "Write-in."

INSTALL IN THIS ORDER
=====================
1. Supabase -> SQL Editor
   Run 14_ranked_entries_week9_fix.sql

2. Supabase -> Edge Functions -> score-week
   Replace the entire function with score-week-v8-index.ts
   Keep Verify JWT OFF
   Deploy

3. Supabase -> SQL Editor
   Run 15_score_week9_now.sql

4. GitHub
   Replace index.html
   Replace version.json

5. refresh-games
   If refresh-games is already v4, leave it alone.
   Otherwise deploy refresh-games-v4-index.ts with Verify JWT OFF.

VERIFY
======
At the bottom of the website:
  Site build: 2026-10-25.2

Week 9's scoring response should report:
- comparison_poll_date: 2026-10-25
- scored_ballots > 0
- tied_top25_ranks including Boise State #20 and Northwestern #20

The site should show Miami as an official ranked team, not a write-in.
