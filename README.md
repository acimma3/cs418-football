# cs418-football
cs 418 football group

Members:
-Antonio
-John Leveille
-Kevin Cox
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
-team_stats.ipynb 
    - Team stats for the 2025 regular season
    - Shape is (32, 136)
    - Each row is one team that played in the 2025 regular 
    - Notable columns: passing_yards, rushing_yards, passing_tds, rushing_tds
-
