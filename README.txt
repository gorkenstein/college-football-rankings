MIAMI LAST-GAME / HEAD-TO-HEAD FIX

Cause
-----
The AP team pool can contain "Miami" while the game feed may use another Miami label.
The old refresh function translated Miami to "Miami (FL)" and then tried to find
that exact spelling in the active pool. If the active pool contained "Miami", the
match failed. The browser also had a second exact-name check.

This update fixes BOTH layers by using one normalized team identity:
Miami = Miami (FL) = Miami (Fla.) = Miami (Florida) = University of Miami = Miami Hurricanes.

Install
-------
1. Supabase -> Edge Functions -> refresh-games
   Replace the entire function with refresh-games-v4-index.ts
   Keep Verify JWT OFF and deploy.

2. Supabase -> SQL Editor
   Run 11_refresh_miami_game_data.sql
   Wait 10-20 seconds and inspect net._http_response.

3. GitHub
   Replace index.html and version.json.

No score-week change is required.
The index.html in this package includes the Week 6 / Week 7 / Week 8 standings work.
