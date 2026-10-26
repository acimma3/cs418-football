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
