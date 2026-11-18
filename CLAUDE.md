# AussieArbFinder

R Markdown document that identifies arbitrage opportunities in head-to-head (H2H) betting markets across Australian bookmakers using live odds data.

## How it works

1. Fetches live odds via the Odds API (`oddsapiR` package) for all active Australian sports markets
2. Filters to H2H markets, adjusts for Betfair lay bet commissions
3. Keeps only the best odds per outcome per match
4. Calculates the arbitrage percentage (sum of inverse of best odds) — values below 1.0 (100%) indicate a guaranteed profit opportunity, plus the stake split per $100 and the guaranteed return
5. Outputs results as an interactive `DT` table

Times: the API returns UTC. Convert for display with `with_tz(x, "Australia/Melbourne")` (the `melbourne_time()` helper), never a fixed offset — Melbourne is UTC+11 from October to April. If no sport has an Australian H2H market, the report stops early with `knitr::knit_exit()`.

Testing without a key: install a stub `oddsapiR` (functions `toa_requests`, `toa_sports`, `toa_sports_odds` returning data frames with `id, home_team, away_team, commence_time, bookmaker, market_key, outcomes_name, outcomes_price`) into a scratch library and knit against it.

## API key

**Never hardcode the API key.** Set it in `.Renviron`:

```
ODDS_API_KEY=your_key_here
```

Run `usethis::edit_r_environ()` to open the file. The code reads it via `Sys.getenv("ODDS_API_KEY")` and will throw an error if unset. `.Renviron` is listed in `.gitignore`.

Get a key at: https://the-odds-api.com

## Files

- `H2H-Arbitrage-Finder.Rmd` — Main analysis document (knit to HTML to run)
- `H2H-Arbitrage-Finder.html` — Most recent knitted output
- `references.bib` — BibTeX citations

## Packages

`oddsapiR`, `tidyverse`, `stringr`, `DT`, `knitr`, `kableExtra`
