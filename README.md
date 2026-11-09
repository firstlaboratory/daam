# Daam

**Daam** (दाम, "price") is a price dictionary for everyday things: groceries, fuel, rent, vehicles, home services, appliances, gold and 250+ more items, by country, state and city, converted into any currency.

Live at **https://firstlaboratory.github.io/daam/**

## How prices work
- Most prices are typical city estimates, shown with a "usually" range.
- The **Refresh prices** button fetches, straight from the phone:
  - exchange rates (open.er-api.com) and gold/silver spot prices (gold-api.com), no key needed
  - the latest saved prices in `weekly.json` and `prices.json`
  - today's Indian mandi prices for ~68 vegetables, fruits, grains and sugar from data.gov.in, if a
    data.gov.in key is saved at the bottom of the page (data.gov.in blocks servers abroad, so this
    only works from the phone)
- A GitHub Action (`.github/workflows/daam-prices.yml`) also updates rates and gold/silver every morning.
- Each item links to places to check today's real price before buying.

## Files
- `index.html` — the whole app
- `prices.json` — daily live prices, written by `tools/update_prices.py`
- `sw.js`, `manifest.json`, `icon.svg` — install on phone and offline use

## Weekly check
Every Monday a scheduled Claude task updates `weekly.json` for items no free live source covers
(item ids and how each is checked are in `tools/weekly-items.json`):
- `weekly`: fuel, LPG, milk and dairy, eggs, meat, fish, oil, salt, tea, coffee, bread, water, every run
- `rotate`: ~40 slower-changing items per run, oldest first (rent, vehicles, appliances, services,
  and produce that isn't in the mandi data)
- `live`: skipped; the Refresh button keeps these current from mandi prices, moving the last
  checked shop price by the market's percentage change
`weekly.json` keeps every price with its own date in `updated`, and the app shows that date under each Indian price.
