# weather lines

a quiet, monochrome 10-day forecast in the spirit of the old lines.io weather view. each thin grey line is one run of an ensemble weather model; the black line is their average. where the grey lines bunch up the forecast is confident, where they fan out it isn't.

one static `index.html`, no build step, no api key. the browser pulls data straight from [open-meteo](https://open-meteo.com/).

## what it shows

- temperature (°f), precipitation (in/hr), wind (mph) and cloud cover (%), hourly for 10 days
- night shading from that day's sunrise and sunset
- a dashed "now" line; hover or drag across a panel (or focus one and use ← →, shift for a day) to read any hour. it eases back to now when you leave
- a day/date/hi-lo strip that stays pinned while you scroll
- click the place name in the heading to change it: type a city, pick from the list (or use your current location). it remembers your choice on that device
- model picker in the status line: noaa gfs (31 runs), ecmwf (51), google weathernext 2 (64)
- theme button (next to the model name) cycles: match your device → light → dark. remembered per device

the clock and readouts update every minute and the forecast re-fetches every 30 minutes. on each update only the values that changed get a brief tint behind them. "pause updates" in the footer stops all of that until you resume.

## accessibility

aimed at wcag 2.2 aa, checked with axe-core (no violations, light and dark) and by keyboard:

- every control works from the keyboard with a visible focus ring; focused items are never hidden under the pinned day strip
- each chart is a slider over the hours. arrow keys step an hour, shift+arrow or page up/down a day, home/end jump to the ends, esc returns to now. screen readers hear the hour, the average and how far apart the runs are ("friday 3 pm: 47°, runs 44° to 51°")
- "show the forecast as a table" gives the same 10 days as a data table: high, low, spread of highs across runs, rain, max wind, cloud cover and daylight
- model menu and place search follow the aria menu-button and combobox patterns; model, place, theme and pause changes are announced
- text contrast is at least 4.9:1 in both themes, even mid-pulse; `prefers-contrast: more` darkens the runs and gridlines, `forced-colors` (windows high contrast) uses system colors, and `prefers-reduced-motion` drops the glide and the pulse
- auto-updates can be paused (2.2.2), and the layout reflows to 320px wide with no sideways scrolling

the thin grey runs are deliberately faint. the information they carry (how much the runs agree) is also in the slider readouts and the table, so the chart isn't the only way to get it.

## url options

| param | example | default |
|---|---|---|
| `lat`, `lon` | `?lat=53.35&lon=-6.26` | last place you picked, else seattle |
| `name` | `&name=dublin` | `seattle, wa` |
| `model` | `gfs025`, `ecmwf_ifs025`, `google_weathernext2_ensemble` | `gfs025` |
| `theme` | `light`, `dark` | your last choice, else follows the device |

## hosting on github pages

1. create a repo (for example `weather`) and commit `index.html` and this readme to `main`
2. settings → pages → build and deployment → deploy from a branch → `main` / `(root)`
3. it'll be live at `https://particle.github.io/weather/` within a minute or two

## data and attribution

forecast data comes from the open-meteo ensemble api (`ensemble-api.open-meteo.com/v1/ensemble`), sunrise/sunset from their forecast api, and place search from their geocoding api. open-meteo is free for non-commercial use, and its data is licensed cc by 4.0. the footer link covers the attribution.
