# Spring in the Alps

An interactive research display comparing **March and April week by week** in
Morzine, Méribel, La Tania, La Plagne and Megève.

## Open the display

Open `index.html` in a modern browser and choose **Load historical data**.
No installation, build or API key is required. An internet connection is required
to retrieve ERA5/ERA5-Land historical records from Open-Meteo. If your browser restricts
requests from local files, serve the page as described below.

After loading, all statistics and filters work without further requests in the
same tab. Reloading the page requires downloading again; the CSV preserves the
calculated values and provenance. No weekly values are bundled or fabricated
when the provider is unavailable.

Alternatively, serve the repository with Python:

```sh
python -m http.server 8000
```

Then visit http://localhost:8000.

## Publish with GitHub Pages

The included workflow publishes only `index.html` after pushes to `main`.
To enable it:

1. In **Settings → Pages → Build and deployment**, choose **GitHub Actions**
   as the source. Repository administrator access may be required.
2. Merge the dashboard and workflow into `main`.
3. In **Actions**, wait for **Deploy dashboard to GitHub Pages** to succeed.
   If the changes were merged before Pages was enabled, run that workflow
   manually with **Run workflow → main**.

Once deployed, the default site address is **https://edanzwick.github.io/ski/**.
The deployment's `github-pages` environment also links to the published URL.
Subsequent pushes to `main` automatically update it; other branches do not deploy.
No API keys, build dependencies or manually configured secrets are needed.

GitHub Pages availability depends on the repository's visibility and account
plan. The published dashboard will normally be publicly accessible, even when
the source repository is private. This setup does not itself enable Pages in
repository settings or confirm that a deployment has completed.

## Explore

- Switch between March, April and both months; select ski areas.
- Scroll through all eight measures without selecting a statistic: snow depth,
  snowfall, snow days, daily maximum/minimum temperatures, liquid rain,
  total precipitation and rain days.
- Inspect date ranges and complete-year coverage alongside every weekly value.
- Explore an interactive weekly line chart above each statistic’s table. Charts
  follow the month and ski-area filters, with consistent area colors and line patterns.
- Hover, tap or focus a chart point to see its value, units, date range, source model
  and contributing years. Tab into a chart, then use arrow keys to visit points,
  Home/End to jump to the first/last point, or Escape to clear the details.
  On small screens, scroll charts horizontally; full data tables remain available.
- Missing values appear as gaps, never zeros. Week 5’s shorter duration is labeled
  on each chart; lines compare period averages, not daily observations.
- Download every measure for the selected areas and periods as CSV, including
  contributing years, source requests, grid coordinates, retrieval times and caveats.

## Research limitations

The display uses **ECMWF/Copernicus ERA5 and ERA5-Land reanalysis via Open-Meteo**, not forecasts,
resort-reported base depths or independently validated station observations.
The common target sample is **2016–2025**, not a 30-year climate normal.
Direct archive access was unavailable in the development environment; historical
data is therefore requested by the browser, not embedded as unverified numbers.
Failed requests remain missing and can be retried without reloading successful
year/model requests. Snow depth uses ERA5-Land; all other measures use ERA5.

Weeks are fixed **UTC calendar date blocks**: days 1–7, 8–14, 15–21, 22–28,
and 29–month end. The last period has three days in March and two in April;
its totals must not be compared as seven-day totals.
Each metric is first aggregated within a complete year/period and then averaged
equally across complete years. Temperatures and hourly depth are means; snowfall,
rain and precipitation are totals; event days are counts. Snow days require
at least 1 cm of fresh snow; rain days require at least 1 mm of liquid rain.
The counts can overlap. Missing records or unexpected units exclude that metric’s
year/period, not replace it with zero. Per-value year counts and contributing
years make partial coverage explicit.

ERA5’s approximately 25 km grid and ERA5-Land’s approximately 11 km grid cannot resolve individual ski slopes.
Approximate locality coordinates select grid cells, with elevation downscaling
disabled; nearby areas can share cells. Returned grid coordinates and elevations
are shown by model in the source notebook. Modeled snow depth is not groomed piste depth;
Open-Meteo warns that ERA5-Land snow depth tends to be overestimated.
The API converts snowfall water equivalent using a fixed 7:1 snow-to-water depth
ratio. Snow depth and snowfall come from different model grids.
**Total precipitation includes snow’s water equivalent; liquid rain is separate.**

Sources: [Open-Meteo historical API documentation](https://open-meteo.com/en/docs/historical-weather-api),
[provider API specification](https://github.com/open-meteo/open-meteo/blob/main/openapi/historical-weather.yml),
[Copernicus ERA5](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels),
[Copernicus ERA5-Land](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-land),
[Hersbach et al. (2020)](https://doi.org/10.1002/qj.3803), and
[Muñoz-Sabater et al. (2021)](https://doi.org/10.5194/essd-13-4349-2021).
Data attribution: Open-Meteo, CC BY 4.0; ECMWF/Copernicus ERA5 and ERA5-Land.
The free API is subject to non-commercial usage terms and rate limits.

The dashboard uses no external libraries, fonts or analytics. Its only data
requests are twenty sequential annual, multi-location archive requests (two models per year) after the
user presses the load button; a request times out after 45 seconds.
There is no existing build, lint or automated test suite in this repository.
