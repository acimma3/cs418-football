# cs418-football
cs 418 football group

Members:
-Antonio
-John Leveille
-Kevin
-Nishant

Research Question(s):
-Is rushing or passing more effective in winning NFL games?
How much does average WR separation correlate to yardage?

Primary Datasets:

-nflverse_acquire.ipynb -> 
    - Play by Play data for 2025, can look for other seasons
    - Shape is (48771, 372)
    - Each row is one play of a game
    - Notable columns:
        posteam (team with possession), yards_gained, success, passer, rusher, receiver
    
-player_stats_acquisition.ipynb -> nflverse - https://github.com/nflverse/nflreadpy
    - Player Weekly Stats
    - Shape (94848, 150)
    - One row = stats for one player for one week
    - Notable columns:
        player_name, team, passing_yards, rushing_yards

Secondary Datasets:
-
-
