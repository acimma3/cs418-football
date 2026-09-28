# cs418-football
cs 418 football group

# Members:
- Antonio
- John Leveille
- Kevin Cox
- Nishant

# Research Question(s):
- Is rushing or passing more effective in winning NFL games?
- How much does average WR separation correlate with receiving yardage?

# Primary Datasets:
- nflverse_acquire.ipynb -> 
    - Play by Play data for 2025, can look for other seasons
    - Shape is (48771, 372)
    - Each row is one play of a game
    - Notable columns:
        posteam (team with possession), yards_gained, success, passer, rusher, receiver
    
- player_stats_acquisition.ipynb -> nflverse - https://github.com/nflverse/nflreadpy
    - Player Weekly Stats
    - Shape (94848, 150)
    - One row = stats for one player for one week
    - Notable columns:
        player_name, team, passing_yards, rushing_yards

# Secondary Datasets:
- team_stats.ipynb 
    - Team stats for the 2025 regular season
    - Shape is (32, 136)
    - Each row is one team that played in the 2025 regular 
    - Notable columns: passing_yards, rushing_yards, passing_tds, rushing_tds
- nextgen_receiving_acquisition.ipynb -> NFL Next Gen Stats Receiving Data
    - Data acquired using nflreadpy
    - 2025 regular season
    - Focused on Wide Receivers (WR)
    - Raw dataset shape: (1402, 23)
    - Filtered WR weekly observations: 888
    - Final cleaned dataset shape: (887, 19)
    - Notable columns:
        player_gsis_id, player_display_name, team_abbr, week,
        avg_separation, avg_cushion, avg_intended_air_yards,
        targets, receptions, catch_percentage, yards, avg_yac,
        avg_expected_yac, avg_yac_above_expectation
    - Created variables:
        yards_per_target, yards_per_reception
    - Used to investigate how average WR separation relates to receiving yardage
    - Cleaned dataset saved as nextgen_wr_receiving_2025.csv