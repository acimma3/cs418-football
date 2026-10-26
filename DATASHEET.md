# Datasheets for each primary dataset
## nflverse play-by-play (pbp) data:
- Motivation: The dataset was originally created and is still maintained by a team of four, with the lead Tan Ho as the original contributor to the nflverse repository where the database comes from. The whole package is intended to be an open-source NFL-focused database intended for easy visualization and analysis of NFL data.
- Composition: Each single row represents a play from the 2025 NFL season. There are 48,771 plays listed in the set, and it includes all of them, even ones called back for penalties.
- Collection: nflverse as a whole gets their data from publicly-available NFL feeds. For play-by-play specifically, it's automated collection from scraping the Next Gen Stats web API and updated the day after games are played. 
- Preprocessing: The data is processed from a raw collection file called pbp-raw, and it's available but not released on the repo.
- Uses: This has been used in tons of NFL data analysis projects that I couldn't really count.
- Distribution: The repo is distributed through its own website (nflverse.nflverse.com) and its github repo (https://github.com/nflverse), which contains the data files under the nflverse-data repo (https://github.com/nflverse/nflverse-data). The access of the files in python is using the nflreadpy package, maintained in its own repo as well (https://github.com/nflverse/nflreadpy). It's released as open source under the MIT License, which allows for unrestricted use as long as the license is included in any projects it's used in.  
- Maintanence: The project is maintained by five people all credited as authors: Sebastian Carl (also a maintainer), Ben Baldwin, Lee Sharpe, Tan Ho, and John Edwards. The specific dataset is released under Tan Ho's name.

## nflverse player stats:
- Motivation: It's the same package as the first data set, however this specific dataset (named under stats_player) was originally contributed by user mrcaseb. 
- Composition: Each row represents an individual player's stats in a single game from 2021 to 2025, with 94,848 such entries.
- Collection: The data was gathered in a similar way the other dataset was acquired by using publicly available feeds. 
- Preprocessing: Player stats is generated at the same time as play-by-play data and uses the same source, however this time it is condensed to within a single week per player.
- Uses: This has also been used in tons of NFL data analysis projects that I couldn't really count.
- Distribution: Licensing is the same as above.
- Maintanence: The project is maintained by the same people as credited before.

# Scope
## Q1: How do rushing and passing success rates individually correlate with NFL team win percentages?
- Target Population: Every NFL team that played in the 2025 season. Only regular season games count.
- Access Frame: Every NFL team and their games during the 2025 season. No gaps are found as evidenced in datasheet_checks.ipynb under Q1 Scope check.
- Sample: All plays from all games in the access frame that include 'run' or 'pass' in their play type.
- Notes: All 32 teams and their 17 regular season games are in our dataset. However, this does not guarantee that every individual play was recorded. Additionally, we can only look at correlation between rushing/passing and win percentages but that does not establish causation. 

## Q2: How do yards to go and field position affect the average EPA of punting versus going for it on fourth down?
- Target Population: Every 4th down play that occurred in the 2025 regular NFL season.
- Access Frame: All 4th down plays recorded in the nflverse 2025 regular season play-by-play dataset. 2815 relevant plays as evidenced in datasheet_checks.ipynb.
- Sample: All 4th down plays classified as 'punt', 'run', or 'pass' play types that include yards-to-go and EPA values.
- Notes: Plays involving other 4th down decisions such as field goal attempts are excluded. Important to note that our analysis can only account for decisions that were actually made, not the hypothetical alternatives.

## Q3: How does average WR separation correlate with receiving yards per target, and does this relationship change based on route depth?
- Target Population: All wide receiver plays during the 2025 regular NFL season.
- Access Frame: All wide receiver plays recorded in the 2025 NFL Next Gen Stats receiving dataset. Contains 888 observations as evidenced in datasheet_checks.ipynb.
- Sample: 887 observations from the access frame that have valid separation, receiving yards, targets, and intended air yards values. Only 1 play was excluded from the access frame due to missing receiving yards.
- Notes: Almost all of the access frame is included in our sample, however we cannot verify that the NFL Next Gen Stats receiving dataset contains every wide receiver play made during the 2025 NFL season. Therefore, we could be missing some unrecorded plays.

# Codebook
## Q1: How do rushing and passing success rates individually correlate with NFL team win percentages?
| Column | Data type | Units | Description | Range / Allowed values | Missing values | Source |
|---|---|---|---|---|---|---|
| `season_type` | String | None | Identifies regular-season or postseason games. | `REG`, `WC`, `DIV`, `CON`, `SB` | Null | nflverse PBP |
| `game_id` | String | None | Unique identifier for an NFL game. | NFL game ID | Null | nflverse PBP |
| `home_team` | String | None | Abbreviation of the home team. | NFL team abbreviations | Null | nflverse PBP |
| `away_team` | String | None | Abbreviation of the away team. | NFL team abbreviations | Null | nflverse PBP |
| `home_score` | Integer | Points | Home team's score recorded for the play. | Nonnegative integers | Null | nflverse PBP |
| `away_score` | Integer | Points | Away team's score recorded for the play. | Nonnegative integers | Null | nflverse PBP |
| `posteam` | String | None | Team possessing the football. | NFL team abbreviations | Null | nflverse PBP |
| `play_type` | String | None | Classification of the play. | `run`, `pass`, `punt`, etc. | Null | nflverse PBP |
| `success` | Float | Binary | Indicates whether a play was successful according to nflverse's success metric. | 0, 1 | Null | nflverse PBP |
| `win` | Integer | Binary | Indicates whether a team won a game. | 0 = Loss, 1 = Win | None after calculation | Derived in `eda.ipynb` |
| `win_pct` | Float | Proportion | Proportion of regular-season games won by a team. | 0–1 | Null if unavailable | Derived in `eda.ipynb` |
| `success_rate` | Float | Proportion | Average success value for a team's rushing or passing plays. | 0–1 | Null if unavailable | Derived in `eda.ipynb` |

## Q2: How do yards to go and field position affect the average EPA of punting versus going for it on fourth down?
| Column | Data type | Units | Description | Range / Allowed values | Missing values | Source |
|---|---|---|---|---|---|---|
| `season_type` | String | None | Identifies the season type. | `REG`, `WC`, `DIV`, `CON`, `SB` | Null | nflverse PBP |
| `down` | Float | None | Current offensive down. | 1–4 | Null | nflverse PBP |
| `play_type` | String | None | Type of play performed. | `run`, `pass`, `punt`, etc. | Null | nflverse PBP |
| `ydstogo` | Float | Yards | Number of yards needed to achieve a first down or touchdown. | Nonnegative integers | Null | nflverse PBP |
| `yardline_100` | Float | Yards | Distance from the opponent's end zone. | 0–100 | Null | nflverse PBP |
| `epa` | Float | Expected points | Expected Points Added by the play. | Any real number | Null | nflverse PBP |
| `decision` | String | None | Whether the team punted or attempted a fourth-down conversion. | `Punt`, `Go for it` | None after classification | Derived in `eda.ipynb` |
| `avg_epa` | Float | Expected points | Average EPA for plays grouped by yards to go and decision. | Any real number | Null if unavailable | Derived in `eda.ipynb` |
| `plays` | Integer | Plays | Number of observations within each group. | Positive integers | None after calculation | Derived in `eda.ipynb` |

## Q3: How does average WR separation correlate with receiving yards per target, and does this relationship change based on route depth?
| Column | Data type | Units | Description | Range / Allowed values | Missing values | Source |
|---|---|---|---|---|---|---|
| `player_gsis_id` | String | None | Unique identifier assigned to an NFL player. | Valid GSIS player IDs | Null | Next Gen Stats / renamed player stats ID |
| `season` | Integer | Year | NFL season associated with the observation. | 2025 for Q3 | Null | Both datasets |
| `week` | Integer | Week | NFL week associated with the observation. | 1–18 for regular-season weekly data | Null | Both datasets |
| `player_position` | String | None | Player's listed position. | `WR` for filtered dataset | Null | Next Gen Stats |
| `team_abbr` | String | None | Abbreviation of the player's team. | NFL team abbreviations | Null | Next Gen Stats |
| `avg_separation` | Float | Yards | Average distance between the receiver and nearest defender at the relevant tracking point. | Nonnegative values | Null | Next Gen Stats |
| `avg_intended_air_yards` | Float | Yards | Average intended air yards on the receiver's targets. | Numeric values, potentially negative | Null | Next Gen Stats |
| `yards` | Integer | Yards | Total receiving yards recorded for a player during a week. | -2 to 225 | Null (1 observation) | Next Gen Stats |
| `targets` | Integer | Targets | Number of times a receiver was targeted during a week. | 5–23 | No missing values | Next Gen Stats |
| `receptions` | Integer | Receptions | Number of completed receptions during a week. | 0–16 | No missing values | Next Gen Stats |
| `weekly_receiving_yards` | Numeric | Yards | Total receiving yards accumulated by a player during the week. | Numeric values | Null | Player stats, renamed |
| `weekly_targets` | Numeric | Targets | Number of times a player was targeted during the week. | Nonnegative integers | Null | Player stats, renamed |
| `yards_per_target` | Float | Yards per target | Receiving yards divided by the number of targets. | Numeric values | Undefined when targets = 0 | Derived in `eda.ipynb` |
