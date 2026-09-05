# Dadventure

A one-page site: a full-screen map that zooms leg by leg while cards of the letters scroll over it.
Live at https://jacobdixon.github.io/dadventure/

## Files
- `index.html` — the whole app. Loads the two data files below; no build step.
- `dadventure.md` — the letters. Edit this to change anything on the page.
- `timeline.json` — the route, one entry per day, made from a Google Maps Timeline export.
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

The `date:` line is what links a letter to its route. The `place:` line is the heading. Photos are optional.

## Splitting a day into cards
A line with just `---` splits a day into cards. The page cuts each day's route into legs
(flights, long drives, "around town" stretches) and hands them to the cards in order.
To pin a card to a specific stretch of the day, add `leg: 09:00-12:11` right after the `---`.
Photos listed on the day go on its first card; add a `photos:` line after a `---` for later cards.

## Adding a day
Copy any block, paste it at the bottom, change the day number, date, and text. If the day exists in `timeline.json` the map will follow; if not, the letter still shows, just without a route.

## Viewing locally
`index.html` needs to be served (browsers block file:// fetches): `python3 -m http.server` in this folder, then open http://localhost:8000.
