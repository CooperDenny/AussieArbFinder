# AussieArbFinder
An R Markdown report that scans live head-to-head (H2H) odds from Australian bookmakers for arbitrage: markets where backing every outcome at the best available price guarantees a profit. It uses the `oddsapiR` package to fetch odds from [The Odds API](https://the-odds-api.com), and the `tidyverse` and `DT` packages to find and display the best prices.

## What it finds

- **H2H arbitrage**: for each upcoming match, the best price for every outcome across bookmakers. If the implied probabilities add up to less than 100%, the market is an arb. The table shows how to split a $100 outlay (`stake_per_100`) so every result returns the same amount (`return_per_100`).
- **Back/lay arbitrage**: a bookmaker back bet paired with a Betfair lay bet on the same outcome.

Betfair prices are adjusted for commission (10% on NRL, 5% elsewhere), so the comparison is on what you would actually be paid. Start times are shown in Melbourne time, with daylight saving.

## Setup

1. Get an API key from [the-odds-api.com](https://the-odds-api.com).
2. Add it to your `.Renviron` (run `usethis::edit_r_environ()`), then restart R:
   ```
   ODDS_API_KEY=your_key_here
   ```
   `.Renviron` is git-ignored. Never commit the key.
3. Install the packages: `install.packages(c("oddsapiR", "tidyverse", "DT", "knitr", "kableExtra"))`.
4. Knit `H2H-Arbitrage-Finder.Rmd`. Each run makes one API request per active sport, which counts towards your monthly quota (shown at the top of the report).

Odds move quickly and bookmakers limit accounts that arb, so confirm every price before betting.

## Contents
- `H2H-Arbitrage-Finder.Rmd`: The R Markdown document containing the analysis code.
- `H2H-Arbitrage-Finder.html`: The most recent knitted report (a snapshot, not live odds).
- `references.bib`: BibTeX file containing citations for external resources.
- `AussieArbFinder.Rproj`: R project file for the AussieArbFinder project.

# Citation
To cite this analysis or any of the packages used, please reference the following:

- Gilani, Saiem. oddsapiR: The SportsDataverse's R Package for The Odds API. (2022). https://oddsapiR.sportsdataverse.org
