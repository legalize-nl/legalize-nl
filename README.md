# legalize-nl

Nederlandse wetgeving als versiebeheerde Markdown-bestanden.

## Inhoud

- `nederland/` — 1.800+ Markdown-bestanden met Nederlandse wetten
- Elke wet geïdentificeerd door BWB-ID (bijv. `BWBR0001840.md`)
- Volledige versiegeschiedenis: elke wijziging is een Git-commit
- Verwijzingen naar rechterlijke uitspraken (ECLI) gekoppeld aan wetversies

## Bestandsstructuur

Elk Markdown-bestand bevat:

- **YAML-frontmatter** met metadata:
  - `titel` — officiële titel
  - `identificatie` — BWB-ID
  - `laatste_wijziging` — inwerkingtredingsdatum van deze versie
  - `wijziging_stb` — Staatsblad-referentie
  - `kamerstukken` — Kamerstuknummers
  - `ecli_citations` — rechterlijke uitspraken die deze wet citeren
  - `ecli_citations_versioned` — citaten gekoppeld aan historische versies

- **Markdown-body** — wettekst met artikelstructuur

Voorbeeld:
```yaml
---
titel: Grondwet
identificatie: BWBR0001840
laatste_wijziging: '2023-02-22'
wijziging_stb: Stb. 2023, 62
kamerstukken: '35741'
ecli_citations:
  total_judgments: 42
  top_articles:
  - article: 1
    cited_in_judgments: 15
    sample_eclis:
    - ECLI:NL:HR:2022:1234
---
```

## Mogelijkheden

- **Versiegeschiedenis** — `git log` toont alle wijzigingen chronologisch
- **Vergelijkingen** — `git diff` vergelijkt twee versies
- **Herkomst** — `git blame` traceert elke regel naar de oorspronkelijke wijziging
- **Historische weergave** — bekijk de wet zoals die op een bepaalde datum gold
- **Rechtspraakverwijzingen** — ECLI-identifiers linken naar uitspraken op rechtspraak.nl
- **Versiegebonden citaten** — uitspraken gekoppeld aan de geldende wetversie op uitspraakdatum

## Gebruik

```bash
git clone https://github.com/legalize-nl/legalize-nl

# Wijzigingsgeschiedenis bekijken
git log --oneline -- nederland/BWBR0001840.md

# Versies vergelijken
git diff HEAD~1 HEAD -- nederland/BWBR0001840.md

# Wet op specifieke datum bekijken
git show $(git rev-list -n1 --before="2020-01-01" HEAD):nederland/BWBR0001840.md

# Zoeken in alle wetten
grep -r "discriminatie" nederland/

# Rechtspraakverwijzingen bekijken
grep -A 20 "ecli_citations:" nederland/BWBR0001854.md
```

## Bronnen

- **Wetgeving**: [wetten.overheid.nl](https://wetten.overheid.nl) — Basiswettenbestand (BWB), publiek domein
- **Rechterlijke uitspraken**: [rechtspraak.nl](https://rechtspraak.nl) — open data met ECLI-identifiers

## Bijwerken

Geautomatiseerde synchronisatie binnen enkele minuten na publicatie in het Staatsblad.

## Omvang

Dekt het Basiswettenbestand (BWB): wetten, AMvB's, ministeriële regelingen en overige nationale regelgeving. Circa 45.000 regelingen; de repository bevat alle actief onderhouden wetten.
