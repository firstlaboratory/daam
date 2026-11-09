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
