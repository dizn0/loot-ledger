# Loot Ledger

A loot split calculator for YunaMS expedition bosses. Enter what dropped and how many people are in the run, and it splits the loot by share value so everyone gets a fair cut.

**Live:** https://dizn0.github.io/loot-distributor/

## Bosses

- Pink Bean
- Empress Cygnus
- Magnus (coming soon)
- Lotus (coming soon)

## How it works

- Every item is worth a set number of shares (shown on the diamond badge). The tool adds up all the shares and divides them evenly among the players still in the roll.
- Top-tier single-roll items (Explorer's/Cygnus' Blessing, Perfect Pendant, Timeless Moonlight, Maple Warrior 30) are rolled on their own first, and those winners sit out the rest.
- Pink Bean shares are counted in Rock of Time (1 point = 1 RoT). Empress is valued off scrolls and Diamonds.
- Hover the (i) next to any item for what it is and how its share value was set.
- The share button builds a clean results card you can drop straight into Discord.

Loot distribution is ultimately the host's call. The tiers are a guide, and the in-app explainer covers the common alternatives (single roll for everything, flat split, etc.).

## Prices

Item values are 7-day market averages from yuna.ms/market, refreshed hourly by a GitHub Action.

- `prices.json` holds the latest values. It is seeded with estimates so the page shows prices immediately, even before the first run.
- `scripts/fetch_prices.py` reads each item's market page and pulls its average price.
- `.github/workflows/update-prices.yml` runs the scraper hourly and commits any changes back.

To add or fix a priced item, open its page on yuna.ms/market, copy the number from the URL (`yuna.ms/market/<id>`), and add it to `TARGETS` in `scripts/fetch_prices.py`. Category items (any weapon, glove, etc.) and items with no stable market are intentionally left unpriced and valued off Rock of Time instead.

## Structure

```
index.html                            the app (single self-contained file)
prices.json                           latest market prices
scripts/fetch_prices.py               price scraper
.github/workflows/update-prices.yml   hourly updater
```

No build step. `index.html` is one file with everything inlined.

## Local preview

Prices are fetched at load, so open it over a local server rather than the file directly:

```
python -m http.server
```

Then visit http://localhost:8000. (Opening the file with `file://` will show the seed estimates only, since browsers block local fetches.)

## Credits

Loot-split idea inspired by [Tzei](https://yuna.ms/forum/index.php?members/tzei.2311/)'s in-house tool. Built by [dizno](https://yuna.ms/forum/index.php?members/dizno.2863/) with the help of Fable 5.
