SCORED BALLOT SHARING UPDATE

What this adds
--------------
- Signed-in pool members can tap any player name in Season Standings.
- A completed scored ballot opens only after that week's AP poll is published.
- If a player has multiple scored weeks, a Week dropdown appears.
- Any displayed scored ballot can be saved as PDF.
- Signed-out visitors can see standings, but player names are not clickable.
- Pre-deadline/unscored ballots remain private.
- No email addresses are exposed.

INSTALL
-------
1. Supabase -> SQL Editor:
   Run 05_scored_ballot_sharing.sql once.

2. GitHub repository:
   Replace index.html with this package's index.html.
   Replace version.json with this package's version.json.

3. Wait for GitHub Pages to update, then refresh the site.

No Edge Function change is required.
