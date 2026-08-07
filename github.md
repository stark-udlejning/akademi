repo: stark-udlejning/akademi
branch: main

## Last sync

date: 2026-08-07T08:20:00Z

### Updated in this project

- `index.html` bygget om til det nye nordiske design (samme navy/orange + Barlow)
- Nyt: ⌘K-søgning med kategorifiltre, indholdsfortegnelse pr. side, favoritter, senest set, "Kom godt i gang"-forløb
- `data/academy-data.json`: risikotillæg beregnes af listeprisen; miljøbidrag = (kundepris/nettopris + risikotillæg) × 3,5 %
- Nyt billede `images/anlaegsmaskiner-dumper.png` skal committes sammen med index.html

## Screen map

| Screen | Repo files |
| --- | --- |
| index.html — Forside | index.html (renderHome), data/academy-data.json (categories), images/500905565-IMG_4852.JPG, images/anlaegsmaskiner-dumper.png, images/1503388982-IMG_0945.JPG |
| index.html — Indholdsside | index.html (renderPage, renderBlock, buildToc, renderFaqSection), data/academy-data.json (pages) |
| index.html — Diagrammer & spec | index.html (renderImageCard, spec-blok), data/academy-data.json (pages/skurvogne-diagrammer), images/* |
| index.html — Søgning (⌘K) | index.html (buildSearchIndex, doSearch, renderFilters) |
| index.html — Favoritter | index.html (renderFavPage, localStorage) |
| Akademiet - nyt design.dc.html | designmockup af ovenstående skærme |
| Akademiet - nuværende.dc.html | genskabelse af det gamle design |
