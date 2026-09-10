# Dadventure

A one-page site: a full-screen map that zooms leg by leg while cards of the letters scroll over it.
Live at https://jacobdixon.github.io/dadventure/

## Files
- `index.html` — the whole app. Loads the two data files below; no build step.
- `dadventure.md` — the letters. Edit this to change anything on the page.
- `timeline.json` — the map data, one entry per day, each with a list of "scenes" (a cleaned route, flight lines, and named pins). Built from a Google Maps Timeline export and then curated by hand.
- `photos/` — put the photos here, named as listed in each day's `photos:` line.

## Map
The page uses Google's terrain map when `GOOGLE_MAPS_KEY` near the top of `index.html` is filled in
(restrict the key to your site's URL in the Google Cloud console). If Google rejects the key, or the
key is empty, it falls back to Esri World Topo tiles, which need nothing.

## Editing a day
Each day in `dadventure.md` looks like:

    ## Day 11
    date: 2026-09-01
    place: White Mountains, NH → Concord, NH → Portland, ME
    photos: 562.jpg, 564.jpg, 567.jpg

    The letter, exactly as you want it to read...

The `date:` line is what links a letter to its map scenes. The `place:` line is the heading. Photos are optional.

## Splitting a day into cards
A line with just `---` splits a day into cards. Each card shows the matching scene for its day
from `timeline.json`, in order (first card, first scene). If a day has more cards than scenes the
extras reuse the last scene. To point a card at a different scene, add `scene: 2` after the `---`.
Photos listed on the day go on its first card; add a `photos:` line after a `---` for later cards.

## Changing what the map shows
Each scene in `timeline.json` has `label`, `route` (list of [lat, lng]), `flights` (list of
[[lat,lng],[lat,lng]] pairs, drawn dashed), and `pins` (list of `{name, lat, lng}`). Add a pin by
adding to that list; remove one by deleting it. A scene with only pins zooms to the pins. Add `"zoom": 15` to a scene to set its zoom level yourself
(higher is closer; the cabin days use 15 so the lake's name shows on the Google map).

## Adding a day
Copy any block, paste it at the bottom, change the day number, date, and text. If the day exists in `timeline.json` the map will follow; if not, the letter still shows, just without a map scene.

## Viewing locally
`index.html` needs to be served (browsers block file:// fetches): `python3 -m http.server` in this folder, then open http://localhost:8000.
