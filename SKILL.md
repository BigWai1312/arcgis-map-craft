---
name: arcgis-map-craft
description: Create polished, offline, editable ArcGIS Pro thematic maps for reports, presentations, and spatial analysis at city, county, town, planning-zone, and village scales.
metadata:
  author: BigWai1312
---

# LEEZY'sGISPicture

Use this skill when a map must be analytically readable, visually consistent, offline, and editable in ArcGIS Pro. It covers thematic maps with DEM, hillshade, water, roads, administrative boundaries, town polygons, planning zones, village points, and report-ready layout elements.

## Working Principles

- Read the actual source data and the current project before editing. Do not reuse a map image or styling from an unrelated report as a substitute for the current data.
- Make the map express one clear spatial conclusion. A map is not complete merely because it displays numeric values.
- Preserve source data, indicator values, codes, geometry, and class fields. Put processed layers and exports in a separate output folder or GDB.
- Prefer local data and offline projects. Do not add online basemaps or web layers to a deliverable that must run on a production computer without internet.
- Produce an editable ArcGIS Pro project plus exported images when the user asks for a map. Do not insert images into a DOCX unless explicitly requested; provide Markdown links or a separate map folder first.

## Data And Scale

Before symbolizing, identify the intended scale and the feature that carries the conclusion:

- City or county scale: show the complete study boundary and its surrounding terrain, major rivers, roads, and neighboring spatial relationships.
- Town or planning-zone scale: retain the town/planning-zone code, name, indicator value, class code, and geometry in the output table. Use projected polygons for thematic results.
- Village scale: use village points when the source is point data. Treat placeholder points as placeholders and keep the source identifier for later spatial linking.
- If an administrative boundary, DEM, water, road, or point source is missing, search the supplied local project folders first. If downloading is necessary, record the source, date, license, spatial reference, file hash, and offline copy.
- Use one projected coordinate system for the working map, preferably a suitable local CGCS2000 projected system. Reproject source layers into the working GDB; do not modify the original files.
- Check geometry validity, coverage, field types, null values, duplicate codes, and the relationship between the indicator field and the class field before drawing.

## Basemap Construction

Build a quiet, complete background that supports orientation without competing with the thematic result.

Recommended drawing order from background to foreground:

1. Full-frame DEM with no uncovered raster edge inside the map frame.
2. Light DEM tint and hillshade. Use vertical exaggeration when relief is visually too flat; a factor around 2–3 is a reasonable starting point and must remain a cartographic effect, not an analytical transformation.
3. Optional pale outside mask or study-area emphasis.
4. Thematic polygons, points, or analysis result.
5. Roads, water, administrative boundaries, labels, and other reference elements with restrained symbols.
6. Optional decorative city-edge shadow below the thematic result and above the background.

Default visual treatment:

- DEM: pale gray-green or pale green, low contrast, about 5–15% transparency after testing the exported image.
- Hillshade: neutral gray-green, usually 5–15% transparency for a clean report map. Increase darkness only when terrain is not legible at final output size.
- Water: blue. Use blue for rivers, lakes, and water bodies so the thematic palette remains distinguishable.
- Roads: light gray or muted gray-brown, with major roads wider than secondary roads. Use a casing/core double-line symbol where the scale supports it.
- County boundaries: muted gray dash-dot line; township boundaries: finer, lighter lines. The county boundary must not overpower the thematic result.
- Main rivers: approximately 1.2–1.5 pt; tributaries: approximately 0.5–0.7 pt; adjust for map scale.
- Labels: only label the administrative units, major rivers, roads, or points needed for interpretation. Do not turn on every label.

## Thematic Symbolization

- Choose a classification method from the actual data distribution. Do not force equal intervals, natural breaks, or unique values merely because the software default is convenient.
- Use sequential or diverging colors that match the meaning of the indicator. Avoid rainbow ramps and excessive high-saturation colors.
- When water features are blue, avoid blue for the thematic result. For water-resource abundance indicators, use a light-to-dark green sequence; darker green means greater abundance.
- Do not encode a larger value as a red warning color unless the indicator is explicitly a risk, pressure, or deficit measure. For example, a high production-water modulus means more water resources per unit area; it is not automatically a water-supply risk.
- Rename fields and class labels into readable Chinese. Do not leave `GRIDCODE`, raw field names, unexplained 1–5 values, or per-class counts in the final legend unless requested.
- Keep the thematic layer visually dominant. Lower the contrast of DEM, hillshade, roads, boundaries, and surrounding context before increasing thematic saturation.

## Layout Standard

Use a compact map page so the study boundary fills the map frame and does not leave a large empty side panel.

- Put the complete city or study boundary at the largest useful extent while retaining a small, even margin for the map frame and geographic ticks.
- The main map frame should occupy most of the page. Aim for the study boundary to fill roughly 85–95% of the frame width and height when the geometry allows it.
- Put the central-city inset in the natural empty area at the upper left. Keep its heading and scale bar close to the inset.
- Put the north arrow at the upper right. Use the native `ArcGIS 指北针 2` style when available.
- Put the legend at the lower right. Use two columns: the left column contains the thematic classes; the right column contains reference explanations such as main rivers, roads, county boundaries, and unmatched data.
- Create one white or very pale translucent legend panel that covers the complete legend area. The panel must be behind every legend title, swatch, line sample, and label, and all legend content must remain inside the panel.
- Put the title, legend, scale bars, north arrow, and other required layout elements inside the map frame/page composition. Remove unnecessary outer page rectangles; retain the inner map-frame boundary.
- Do not show internal figure codes, source notes, projection notes, processing subtitles, or long estimation explanations inside the exported image unless the user requests them. Put the indicator unit directly in the legend title.

## Coordinate Frame And Typography

- Use a geographic graticule around the map frame so the four sides show longitude/latitude coordinates. Keep interior grid lines invisible or very light.
- Use major ticks around 30 minutes and minor ticks around 10 minutes where the map extent supports them. Labels should include `E` and `N` and remain readable at final size.
- Chinese text: `SimSun` / 宋体. English letters and numbers: `Times New Roman`.
- Main title: usually SimSun, bold, approximately 24–28 pt depending on page size.
- Legend title: SimSun, bold, 20 pt.
- Legend class labels and numeric values: Times New Roman, bold, 16 pt.
- Scale bars: two divisions, `km`, Times New Roman, bold, 16 pt. Remove unnecessary subdivisions.
- Keep font families consistent after reopening the project; do not assume that a screen preview proves the font was saved.

## Optional Floating Shadow

For a presentation-style floating city effect, create a separate decorative shadow layer rather than altering the study geometry:

- Duplicate the city boundary, offset it slightly toward the lower-right, and use one or more buffers to create a soft, middle, and edge shadow.
- A longer, darker effect can start around 2–3 km of offset, with buffer distances around 0.8–1.8 km. Tune the values against the map scale and keep the shadow outside the true boundary.
- Use dark gray or dark gray-green with transparency. The shadow should be visible along the edge but never compete with the thematic colors, labels, rivers, or legend.
- Export shadow-on and shadow-off previews separately when the user is deciding on the final style.
- Record that the shadow is decorative and does not change the indicator geometry, spatial statistics, or analytical result.

## Export And Validation

For a normal delivery, keep the source and editable outputs together in a clearly named folder:

- Editable `.aprx` with all paths local and relative where practical.
- File geodatabase containing processed vectors and rasters, with all required sidecars preserved for Shapefiles.
- PNG preview for quick review.
- JPEG at 600 dpi or higher when requested for reports or printing.
- PDF for vector-preserving delivery. EPS is optional for English journal workflows when the target software accepts it.
- A short JSON or Markdown QA record describing source data, projection, classification, layer counts, export settings, and known limitations.

Before reporting completion, reopen the exported project and check:

- No broken layers, online layers, missing rasters, or uncovered DEM area inside the map frame.
- The city/study boundary is fully visible and occupies the intended frame.
- Thematic values and class codes match the source table; no values were silently rounded, recoded, sorted, or dropped.
- The legend panel is below all legend content in drawing order and encloses both columns.
- The inset, legend, title, north arrow, and scale bars do not cover the study boundary or one another.
- County boundary dash pattern, water blue, non-blue thematic colors, font families, two scale-bar divisions, graticule labels, and export DPI match the requested style.
- The final raster dimensions and embedded DPI are correct, and the preview is inspected at the intended report size.

## ArcMap Compatibility

ArcGIS Pro is the primary production environment for this skill. When the target computer uses ArcMap 10.2, keep the same data, field names, colors, layout positions, and cartographic specifications, but implement symbols and layout elements with ArcMap-compatible manual settings. Do not rely on ArcGIS Pro CIM-only edits, Pro-only project files, or online services for the old production computer.
