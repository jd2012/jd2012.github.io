# Park City Ski School Private Lesson Availability

This folder contains the publicly viewable private-lesson availability calendar and its live data feed.

- `index.html`: printable, mobile-friendly calendar. Reads `data.json` from a public GitHub raw URL at each page load. If the fetch fails, the page displays its bundled 2026–27 snapshot and warns that live refresh failed.
- `data.json`: current day-by-day data and `updatedAt` timestamp. **Future CSV refreshes should update this file, not the HTML.**

## Update procedure for future ChatGPT sessions

When the site owner uploads an updated Ski School Summary CSV and says to update the site:

1. Read and validate the CSV. It has 12 activity/page rows across 6 pages, with `date1..date25` and `day1..day25` columns.
2. Map activity code `18190` to `ski` and `18195` to `snowboard`. The CSV contains values for each day in the named `dayN` field, on the corresponding `dateN` (MM/DD) field.
3. Derive years from the report's `begindate` and `enddate` fields, accounting for the New Year rollover. Validate that each listed date has both integer counts and that the number of unique dates matches `numberofdays` in the CSV.
4. Replace the entire `availability` object of `data.json`, and set `updatedAt` to the time the CSV was uploaded or published, with a Mountain Time offset. Preserve the JSON structure `{ "schemaVersion": 1, "updatedAt": "ISO timestamp", "source": "CSV filename", "availability": { "YYYY-MM-DD": { "ski": 0, "snowboard": 0 } } }`.
5. Commit the change to `jd2012/jd2012.github.io` on `main` using the connected GitHub app. Do not edit the HTML for ordinary updates. The calendar refreshes the feed on new page loads and updates its footer timestamp automatically.

## Hosting

The source files are in the public repository `jd2012/jd2012.github.io`. If GitHub Pages is enabled for the `main` branch root, the calendar page should be served under `https://jd2012.github.io/park-city-private-availability/`; live hosting has not yet been verified.

**Original ChatGPT Sites site**: `https://park-city-private-availability.quietcomet18.chatgpt.site`. That is a separate deployment and does not update just because GitHub changed. To preserve this URL, publish the provided `index.html` once through the original ChatGPT Sites project. Afterwards the unchanged HTML will fetch new `data.json` automatically. The Sites publishing connector was unavailable when this repository was set up; no claim is made that the original site has been updated.
