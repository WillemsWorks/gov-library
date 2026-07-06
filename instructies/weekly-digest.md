# Kennisbank Weekly Digest — Instructie

*Dit bestand is de enige bron van waarheid voor de wekelijkse Cowork-taak.
De taak zelf bevat alleen nog: token lezen, dit bestand ophalen, en
opvolgen. Wijzigingen aan hoe de digest werkt: alleen hier aanpassen.*

## Doel

Vind nieuwe publicaties, artikelen en onderzoek van de afgelopen 7 dagen
die relevant zijn voor Paul's GOV Library. Maak een compacte digest,
publiceer op meerdere plekken (lokaal, research-log, HTML-pagina).

## Skills die deze taak gebruikt

- **gov-library-github-sync** — voor alle GitHub-lees/schrijfacties (authenticatie, GET/PUT met sha, foutafhandeling)
- **gov-library-html** — voor het genereren van de HTML-pagina en het bijwerken van digest.html

Als een van beide skills niet beschikbaar/ingeschakeld is: meld dit expliciet, sla de betreffende stap over, verzin de mechaniek niet zelf opnieuw.

## Stap 1 — Onderwerpen ophalen (dynamisch, niet vast)

Haal `research-log/gov-index.json` op (publiek, geen token nodig via raw.githubusercontent.com). Gebruik de `onderwerpen`-lijst van elk doc in dit bestand als basis voor zoekopdrachten — niet een vaste, hardcoded lijst. Zo zoekt de taak automatisch mee zodra er een nieuw GOV-doc bijkomt in dit bestand, zonder dat deze instructie hoeft te veranderen.

Vertaal de onderwerpen naar minimaal 6 gerichte zoekopdrachten, verdeeld over de aanwezige docs — niet alle 12+ docs per se elke week, maar wel over de volle breedte heen gedurende meerdere weken.

## Stap 2 — Filteren

Neem alleen items op die:
- Gepubliceerd zijn in de afgelopen 30 dagen (voorkeur: afgelopen 7 dagen)
- Echte nieuwe inzichten, onderzoek of toepassingen bieden — geen basisherhaling
- Duidelijk aansluiten op een GOV-thema uit gov-index.json
- Komen van betrouwbare bronnen (Harvard Business Review, McKinsey, MIT Sloan, academische journals, toonaangevende practitioners)

## Stap 3 — Schrijven

Schrijf per item:
- **Titel** met URL
- **Bron & datum**
- **GOV-koppeling**: welk GOV-framework dit raakt (1 zin)
- **Kern**: wat is er nieuw of inzichtelijk (2-3 zinnen, Nederlands)
- **Toepassing**: hoe Paul dit kan gebruiken als interim manager/consultant (1-2 zinnen, Nederlands)

Streef naar 5-8 items. Kwaliteit boven kwantiteit.

Bereken het ISO-weeknummer van de publicatiedatum zelf (bijv. `datetime.isocalendar()`). Nooit aannemen — reken na.

**Clusterindeling (definitief):** groepeer elk digest-item onder één van de vier vaste clusters uit `gov-index.json`:
- Verandering & Leiderschap
- Team & Mensen
- Innovatie & Marketing
- Commercie & Klant

Elk doc in `gov-index.json` heeft een `cluster`-veld — gebruik dat om een item te clusteren op basis van het GOV-doc waar het bij hoort.

**Uitzondering: Strategie.** Dit doc heeft geen vast cluster (`cluster: null`, `context_afhankelijk: true`). Beoordeel per Strategie-gerelateerd artikel zelf: gaat het over richting/positionering vóór een veranderopgave → Verandering & Leiderschap. Gaat het over het verkennen/valideren van een nieuwe propositie of markt → Innovatie & Marketing. Geen vaste regel, per artikel op inhoud beoordelen (zie `beslisregel`-veld in gov-index.json).

## Stap 4 — Opslaan (lokaal)

Map: `/Users/paul/Documents/Claude/Kennisbank-Digests/`
Bestand: `digest-[YYYY-MM-DD].md`

Outputformaat:
```
# 📚 Kennisbank Update — week [weeknummer], [datum]

*Nieuwe publicaties relevant voor de GOV Library*

---

## [Thema]
**[Titel](URL)**
*[Bron] · [datum]*
**GOV-koppeling:** [frameworknaam]

[Kern: 2-3 zinnen]

💡 *[Toepassing: 1-2 zinnen]*

---
[herhaal per item]
---
*Automatisch gegenereerd op [datum] · GOV Library van Paul Willems*
```

## Stap 4b — Research-log (via gov-library-github-sync skill)

1. Haal `research-log/gov-index.json` op
2. Bepaal per item het best passende doc-bestand; past niets: `research-log/ongeplaatst.md`
3. Voeg per bestand onderaan toe:
   ```
   ## [datum] — [Titel](URL)
   **Status:** nieuw
   **Bron:** [bron] · [publicatiedatum]
   **Kern:** [2-3 zinnen]
   ```
4. Commit-message: `Research-log update [datum]: [thema]`

## Stap 4c — Digest-archief (via gov-library-github-sync skill)

1. PUT naar `research-log/digest-latest.md` (overschrijven)
2. PUT naar `research-log/digests/digest-[YYYY-MM-DD].md` (nieuw)

## Stap 4d — HTML-publicatie (via gov-library-html + gov-library-github-sync skills)

Volg de workflow "nieuwe digest-editie publiceren" uit de gov-library-html skill. Publiceer als `digest-[YYYY-MM-DD].html`, voeg kaart toe aan `digest.html`.

## Afsluiting

Presenteer het lokale bestand via `mcp__cowork__present_files`. Meld kort: GitHub-publicatie gelukt / overgeslagen (geen token of skill) / gedeeltelijk gefaald (en welk deel).

## Regels

- Volledig Nederlands (titels/bronnen mogen Engels blijven)
- Bondig — leesbaar op een telefoon
- Geen opvulling, geen samenvatting van samenvattingen
- Minder dan 3 relevante items: zeg dat eerlijk
