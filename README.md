# STARK Udlejning Akademiet

Standalone, moderne udgave af jeres SharePoint-akademi, klar til Netlify/GitHub.

## Struktur

```
index.html              ← selve sitet (design, navigation, søgning, routing)
data/academy-data.json  ← alt indhold (25 sider, 789 indholdsblokke)
images/                 ← her lægger du diagrammer/billeder (se nedenfor)
```

Alt indhold er hentet og renset fra jeres 25 SharePoint-sider: tekst, lister,
tekniske spec-tabeller (fx skurvogns-mål) og FAQ-sektioner. Struktur og
sprog er bevaret 1:1 fra kilden — jeg har kun fjernet SharePoint-support-støj
(webpart-metadata, gentagne "AI-agent"-bokse, navigations-duplikater osv.).

## Sådan deployer du

1. **Netlify (nemmest):** Træk hele mappen ind på [app.netlify.com/drop](https://app.netlify.com/drop) — færdig.
2. **GitHub + Netlify:** Push mappen til jeres repo, og forbind det som I plejer (ingen build-step nødvendig — det er statiske filer).

Sitet kræver ingen build, ingen server, ingen dependencies udover Google Fonts (Barlow / Barlow Condensed, samme som jeres nettopriser-skabelon).

## Billeder / diagrammer

De originale diagrammer og billeder ligger inde på jeres interne SharePoint og
kunne ikke hentes automatisk (kræver login). Sitet bruger **de originale
SharePoint-filnavne** (fra SiteAssets-biblioteket), så du kan downloade
billederne direkte og lægge dem i `/images/` uden at omdøbe noget:

- Hvor et billede mangler, vises der lige nu et pænt "diagram tilføjes"-kort
  med det forventede filnavn skrevet i klartekst.
- Så snart en fil med det navn ligger i `/images/`, viser sitet automatisk
  det rigtige billede i stedet — ingen kodeændringer nødvendige.

Se **`billed-tjekliste.md`** for en komplet liste over alle 59 billeder,
organiseret pr. side, med filnavn og kontekst-tekst så du nemt kan genkende
hvilket billede der er tale om. Jeg har allerede sorteret generiske/dekorative
SharePoint-baggrundsbilleder (banner-"tapet", stock-fotos) fra — de tilføjer
ingen værdi og er ikke med i listen.

## Sådan opdaterer du indhold

Alt tekstindhold ligger i `data/academy-data.json` — almindelig, læsbar JSON.
Du kan redigere direkte i filen (fx rette en FAQ-tekst eller tilføje et
punkt til en liste) uden at skulle røre `index.html`. Strukturen er:

```json
{
  "categories": [...],   // navigationens kategorier + sider
  "pages": [
    {
      "id": "skurvogne-diagrammer",
      "category": "skurvogne",
      "slug": "diagrammer",
      "label": "Diagrammer & specifikationer",
      "blocks": [
        { "type": "rte", "html": "…" },        // brødtekst
        { "type": "spec", "title": "…", "rows": [["Højde (cm)","295 cm"]] },
        { "type": "image", "file": "…", "caption": "…" },
        { "type": "faq", "q": "…", "a": "…" }
      ]
    }
  ]
}
```

## Links

Alle links i indholdet er nu tjekket og rettet:

- **Links til andre Akademi-sider** (fx "se sikkerhedsvejledningerne") peger nu
  internt på den rigtige side i sitet (`#/kategori/side`) i stedet for på en
  død SharePoint-URL.
- **Dybe SharePoint-links** (enkelte dokumenter, undersider og guides) er
  fjernet, fordi de løbende bliver døde. I stedet står der ét fast sted at gå
  hen: **Toolbox** (hovedsiden for Udlejning) og AI-robotten
  **"Den lille hjælper"** i Teams. Navnet på dokumentet/siden er bevaret i
  teksten, så man stadig ved, hvad man skal lede efter.
- Henvisningen står som en fast boks på alle 25 sider og som en kort note i
  bunden af de FAQ-svar, der tidligere havde et dybt SharePoint-link.
- De to URL'er styres ét sted i `index.html` (`TOOLBOX_URL` og `HELPER_URL`),
  så de kun skal rettes ét sted, hvis de ændrer sig.
- **Øvrige eksterne links** (forms.office.com, Eloomi, stark.dk) åbner
  fortsat i nyt faneblad, markeret med et lille ↗-ikon.
- **Mailto-links** er urørt.

Hver kategoris **Overblik-side** har desuden fået en ny "Udforsk emnet"-sektion
øverst, med tydelige kort der linker til alle undersider i kategorien — uanset
om det oprindelige SharePoint-indhold nævnte dem i brødteksten eller ej.

## Design

Følger jeres eksisterende STARK Udlejning-designsystem 1:1 (samme som
nettopriser-skabelonen og det interne prisværktøj):
- Farver: navy `#1B3A6B` + orange `#E87722`
- Typografi: Barlow / Barlow Condensed
- Samme radius, skygger og komponent-stil (kort, badges, sticky header)
- Jeres logo hentes direkte fra `stark-udlejning.netlify.app/top_logo.png`

## Funktioner

- Fuld navigation med 6 kategorier / 25 sider, sidebar + mobil-menu
- Live søgning på tværs af alt indhold (titler, brødtekst, spec-tabeller, FAQ)
- FAQ-accordions pr. side
- Forrige/næste-navigation i bunden af hver side
- Links til andre Akademi-sider peger internt; eksterne henvisninger samles ét sted (Toolbox + "Den lille hjælper")
- Fuldt responsivt, ingen build-proces, ingen eksterne dependencies udover fonte

## Testet

Al routing, søgning, FAQ-accordions og sidevisning er automatisk testet på
tværs af alle 25 sider (0 fejl).
