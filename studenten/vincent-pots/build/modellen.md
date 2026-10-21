# Modeltest: welk model en welke effort

Datum: 21 oktober 2026

## Mijn gok (vóór de runs)

Ik verwacht dat **setup A (Sonnet 5.5, effort medium)** het best scoort op mijn testset. Ik gok dat Haiku 5.5 (B) minder goed scoort en Opus 5.5 (C) niet veel beter dan Sonnet.

## Opzet

- **Prompt:** v4 (`build/prompt.md`), dezelfde als de foutmarge.
- **Inputs:** T01, T02, T04 t/m T10 (9 stuks). T03 weggelaten, zoals in de foutmarge.
- **Runs:** 1 per setup per input, 27 aanroepen in totaal.
- **Effort:** medium voor alle drie, zodat alleen het model verschilt.
- **Aanroep:** `claude -p --model <model> --effort medium --tools ""`, elke run een nieuwe sessie zonder tools.
- **Scoreregel:** dezelfde als in `foutmarge.md`: juist als de lijst exact de verwachte opdrachten en deadlines bevat.

## Setups

| Setup | Model | Effort |
|---|---|---|
| A | Sonnet 5.5 (`claude-sonnet-5-5`) | medium |
| B | Haiku 5.5 (`claude-haiku-5-5`) | medium |
| C | Opus 5.5 (`claude-opus-5-5`) | medium |

## Resultaat

Gedraaid op 21 oktober 2026: 27 aanroepen, 1 run per setup per input. Score volgens dezelfde regel als in `foutmarge.md`.

| Setup | Model | Score (n = 9, 1 run) | Juist bij | Output per run (gem.) | Kost per run | Per maand (20 runs) |
|---|---|---:|---|---:|---:|---:|
| A | Sonnet 5.5 | 1/9 | T09 | 167 | $0,0205 | $0,41 |
| B | Haiku 5.5 | 0/9 | (geen) | 772 | $0,0005 | $0,01 |
| C | Opus 5.5 | 2/9 | T07, T09 | 300 | $0,0375 | $0,75 |

- **Kost:** per run gerekend met de officiële tarieven, met de tokens uit de JSON-uitvoer. Cache-write van 1 uur, zoals in `kosten.md`. De kost is die van de API-aanroep met alleen prompt en input; Claude Code stuurt in een gewone sessie meer context mee.
- **Foutmarge:** de score van Sonnet, Haiku en Opus ligt op 0 tot 2 van de 9. In `foutmarge.md` lag de foutmarge van Haiku met dezelfde prompt op 0 tot 1 van de 9. Met één run per setup kan ik dus geen van de drie als beter aanwijzen.

**Mijn gok klopte niet.** Ik verwachtte dat Sonnet het best zou scoren. Opus scoorde het hoogst (2/9), Sonnet 1/9, Haiku 0/9. Dat verschil valt binnen de foutmarge.

**Conclusie volgens de regel van de README:** het verschil valt binnen de foutmarge, dus de setups zijn op score niet te onderscheiden. Kies dan op kost: Haiku is ongeveer 40 keer goedkoper dan Sonnet. Dat is een keuze voor jouw memo, niet voor deze meting. Met één run per setup kan ik niet bewijzen dat Haiku even goed is. Een schone vergelijking vraagt meer runs per setup.
