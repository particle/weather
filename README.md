# weather lines

a quiet, monochrome 10-day forecast in the spirit of the old lines.io weather view. each thin grey line is one run of an ensemble weather model; the black line is their average. where the grey lines bunch up the forecast is confident, where they fan out it isn't.

one static `index.html`, no build step, no api key. the browser pulls data straight from [open-meteo](https://open-meteo.com/).

## what it shows

- temperature (°f), precipitation (in/hr), wind (mph) and cloud cover (%), hourly for 10 days
- night shading from that day's sunrise and sunset
- a dashed "now" line; hover or drag across a panel (or focus one and use ← →, shift for a day) to read any hour. it eases back to now when you leave
- a day/date/hi-lo strip that stays pinned while you scroll
- model picker in the status line: noaa gfs (31 runs), ecmwf (51), google weathernext 2 (64)
- follows the system light/dark setting

the clock and readouts update every minute and the forecast re-fetches every 30 minutes. on each update only the values that changed get a brief tint behind them.

## url options

| param | example | default |
|---|---|---|
| `lat`, `lon` | `?lat=53.35&lon=-6.26` | seattle |
| `name` | `&name=dublin` | `seattle, wa` |
| `model` | `gfs025`, `ecmwf_ifs025`, `google_weathernext2_ensemble` | `gfs025` |
| `theme` | `light`, `dark` | follows the system |

## hosting on github pages

1. create a repo (for example `weather`) and commit `index.html` and this readme to `main`
2. settings → pages → build and deployment → deploy from a branch → `main` / `(root)`
3. it'll be live at `https://particle.github.io/weather/` within a minute or two

## data and attribution

forecast data comes from the open-meteo ensemble api (`ensemble-api.open-meteo.com/v1/ensemble`), and sunrise/sunset from their forecast api. open-meteo is free for non-commercial use, and its data is licensed cc by 4.0. the footer link covers the attribution.
