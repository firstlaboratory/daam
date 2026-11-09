# Daam

**Daam** (दाम, "price") is a price dictionary for everyday things: groceries, fuel, rent, vehicles, home services, appliances, gold and 250+ more items, by country, state and city, converted into any currency.

Live at **https://firstlaboratory.github.io/daam/**

## How prices work
- Most prices are typical city estimates, shown with a "usually" range.
- Updated every morning by a GitHub Action (`.github/workflows/daam-prices.yml`):
  - exchange rates and gold/silver spot prices (no key needed)
  - Indian mandi prices for vegetables, fruit and grains from data.gov.in, using the `DATA_GOV_IN_KEY` repository secret
- Each item links to places to check today's real price before buying.

## Files
- `index.html` — the whole app
- `prices.json` — daily live prices, written by `tools/update_prices.py`
- `sw.js`, `manifest.json`, `icon.svg` — install on phone and offline use

## Weekly Koyambedu check
Every Monday a scheduled Claude task reads the latest Koyambedu market reports for Chennai,
converts wholesale rates to typical shop prices, and writes them to `weekly.json`
(item ids are listed in `tools/weekly-items.json`). The app uses these as the new base prices,
then moves them daily with the government mandi trend on phones that have a data.gov.in key.
The check also covers staples, milk, meat, fuel and LPG every week, and re-checks ~40 slower-changing
items (rent, vehicles, appliances, services…) per run, oldest first. `weekly.json` keeps every price
with its own date in `updated`, and the app shows that date under each Indian price.
