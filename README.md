# GPX Route Elevation to Excel

Turn a GPX track into a metre by metre Excel dataset containing distance, elevation, latitude and longitude.

This small Python utility reads track points from a GPX file, retrieves elevation values through the Google Elevation API, interpolates the route at one metre intervals and exports the result to an XLSX workbook. It is useful when a raw GPX track needs to become a structured dataset for route analysis, mapping, engineering review, fitness analysis or further work in Excel, Python or GIS software.

## What it does

* Opens a file picker for the source GPX track.
* Extracts latitude and longitude from GPX track segments.
* Requests elevations from the Google Elevation API in batches of up to 512 locations.
* Calculates cumulative geodesic distance along the route.
* Linearly interpolates distance, elevation and coordinates at one metre intervals.
* Opens a save dialog and writes the result to Excel.

## Output

The workbook contains these columns:

| Column | Meaning |
| --- | --- |
| Distance (m) | Cumulative distance from the first track point |
| Height (m) | Interpolated elevation returned by the Google Elevation API |
| Latitude | Interpolated latitude |
| Longitude | Interpolated longitude |

## Requirements

* Python 3
* An internet connection
* A Google Maps Platform API key with the Elevation API enabled
* Tkinter, normally included with the standard Windows and macOS Python installers
* gpxpy, pandas, NumPy, Requests, geopy, SciPy and openpyxl

A virtual environment is recommended. Install the Python packages with:

    python -m pip install gpxpy pandas numpy requests geopy scipy openpyxl

## Set up the API key

Open the Python file and replace the placeholder near the end:

    google_api_key = 'INSERT API KEY'

Do not commit a live API key to a public repository. Google may charge for API use or enforce request quotas, so review the limits applying to your account before processing a large track.

## Run

    python "Convert gpx to Excel Lat Long Height.py"

Choose a GPX file, choose where the Excel workbook should be saved and wait for processing to finish.

## Important limitations

* Only GPX track points are read. Routes and standalone waypoints are not included.
* The script requires at least two usable track points and corresponding elevation results.
* Interpolation creates estimated points between the original observations. It does not improve the accuracy of the source GPS positions or the elevation service.
* API errors, partial responses, rate limits and network failures receive limited handling in the current version.
* Very long routes can produce large workbooks because the output interval is fixed at one metre.
* The script installs missing packages into the active Python environment. Use a dedicated virtual environment if you do not want packages added to your main Python installation.

## Licence

GNU General Public License version 3. See LICENSE for the complete terms.
