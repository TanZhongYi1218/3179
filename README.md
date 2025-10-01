# 3179
FIT3179 Homework 4 repositories 

Step-by-step plan
1) Prepare the data (CSV for Vega-Lite)

Extract state-level 2020 values:

For each state: Female_000, Male_000, and Total_000 = Female_000 + Male_000.

Compute **FemaleSharePct = Female_000 / Total_000 * 100`.

Create a clean CSV called state_gender_2020.csv with columns:

State, Female_000, Male_000, Total_000, FemaleSharePct

Make sure state names exactly match the TopoJSON property you’ll join on (e.g., “Johor”, “Kedah”, etc.).

If necessary, standardize names here (e.g., “WP Kuala Lumpur” vs “Kuala Lumpur”).

If you want, I can generate this CSV immediately from your Excel and show you the result.

2) Get the Malaysia states map (TopoJSON)

Obtain a Malaysia Admin-1 geometry (states) and export as TopoJSON.

Keep only Malaysia; simplify geometry to keep file size small (<1 MB total download).

Confirm the object/feature name (e.g., states), and the state name property (e.g., properties.STATE_NAME).

Typical workflow: load shapefile/GeoJSON → clip/simplify → export TopoJSON.
You’ll end with a file like: malaysia_states.topojson.

3) Build the Vega-Lite spec (choropleth)

Start from a minimal spec file (e.g., female_share_map.json) that:

Loads malaysia_states.topojson with "format": {"type": "topojson", "feature": "<YOUR_FEATURE>"}.

Uses transform.lookup to join properties.<STATE_NAME_PROP> to State in state_gender_2020.csv.

Calculates FemaleSharePct (if not already in CSV—either place is fine).

Colors by FemaleSharePct using a threshold or quantize scale with a clear legend.

Adds tooltip with State, Female_000, Male_000, Total_000, FemaleSharePct.

Uses a sensible projection (e.g., "projection": {"type": "mercator"}).

Test locally (VS Code + Live Server or similar) to confirm the map renders and tooltips/legend work.

4) Create a minimal web page (GitHub Pages ready)

Make an index.html that loads Vega, Vega-Lite, and vega-embed (via CDN) and then embeds your spec:

vegaEmbed('#vis', 'female_share_map.json', {actions:false})

Ensure the relative paths to your TopoJSON and CSV are correct from the HTML page.

5) Host on GitHub Pages

Push the following structure to a GitHub repo:

/ (repo root)
├─ index.html
├─ female_share_map.json
├─ data/
│   ├─ state_gender_2020.csv
│   └─ malaysia_states.topojson
└─ README.md (optional)


Enable GitHub Pages (Settings → Pages → deploy from branch).

Open the public URL and verify the map loads.

6) Prepare the 1–2 page PDF report (for Week 9 submission)

Include:

Your name, ID, lab, tutor.

The GitHub Pages URL (HTML page embedding the map).

A screenshot of the map (full width, legend visible).

One short bullet each for:

Domain: “Malaysian population—state-level gender differences.”

Dataset: source(s), attributes used (Female_000, Male_000, computed % female), year (2020).

Transformation: Female share percentage = Female / Total * 100 (normalization for choropleth).

Idiom rationale: Choropleth suits rate/percentage across regions; shows spatial pattern of gender balance.

7) Quick quality checks (avoid common penalties)

Choropleth uses a rate (percentage), not raw totals.

Legend present with units (“%”).

Projection appropriate for Malaysia (not a world projection).

No missing states (no holes); consistent naming.

Title clearly states topic, geography, and year.
