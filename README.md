# Spring in the Alps

An interactive, self-contained research display comparing April and May in
Morzine, Méribel, La Tania, La Plagne and Megève.

## Open the display

Open `index.html` directly in a modern browser. No installation, build, API key,
or internet connection is needed to use the dashboard. External source links
require internet.

Alternatively, serve the repository with Python:

```sh
python -m http.server 8000
```

Then visit http://localhost:8000.

## Explore

- Switch between April, May and a side-by-side comparison.
- Select ski areas and a snow or weather measure.
- Inspect the underlying table and linked sources.
- Download the selected areas and months as CSV, including provenance and caveats.

## Research limitations

The display contains published historical summaries, **not forecasts or independently
validated daily observations**. Source-specific search-index results were available;
direct source pages and the historical weather API were not accessible during research.
The methodology panel documents provenance, uncertain baselines and reporting
elevations. Missing values are not zero, and local weather does not describe every
ski slope. In particular, May resort snow coverage could not be verified.

Sources are OnTheSnow (April snow summaries) and Weather and Climate (weather
for all five areas; exact reference period unconfirmed). All ten area/month combinations
include temperature, total precipitation and published rainy/wet-day averages.
**Total precipitation is not rain-only rainfall.** Separate liquid-rain totals
and May snow metrics remain unverified. Provider links and limitations are in the
display and CSV export.

The dashboard uses no external libraries, fonts, analytics or live data requests.
There is no existing build, lint or automated test suite in this repository.
