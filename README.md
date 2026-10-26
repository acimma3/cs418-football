# cs418-football
cs 418 football group

# Members:
- Antonio
- John Leveille
- Kevin Cox
- Nishant

# Research Questions (Revised):
- Q1: How do rushing and passing success rates individually correlate with NFL team win percentages?
- Q2: How do yards to go and field position affect the average EPA of punting versus going for it on fourth down?
- Q3: How does average WR separation correlate with receiving yards per target, and does this relationship change based on route depth?

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

# Eda:
- Reference [Eda](eda.ipynb)

# Datasheet:
- Reference [Datasheet](DATASHEET.md)
- Our biggest limitation is that we can only include plays that were properly recorded by nflverse and NFL Next Gen Stats. We have verified that all 32 NFL teams have data from all 18 weeks of regular season play. However, we cannot guarantee that all stats from those games are correct or complete.
