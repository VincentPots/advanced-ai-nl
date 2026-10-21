# Modeltest: welk model en welke effort

Datum: 21 oktober 2026

## Mijn gok (vóór de runs)

Ik verwacht dat **setup A (Sonnet 5.5, effort medium)** het best scoort op mijn testset. Ik gok dat Haiku 5.5 (B) minder goed scoort en Opus 5.5 (C) niet veel beter dan Sonnet.

## Opzet

- **Prompt:** v4 (`build/prompt.md`), dezelfde als de foutmarge.
- **Inputs:** T01, T02, T04 t/m T10 (9 stuks). T03 weggelaten, zoals in de foutmarge.
- **Runs:** 1 per setup per input, 27 aanroepen in totaal.
- **Effort:** medium voor alle drie, zodat alleen het model verschilt.
- **Aanroep:** `claude -p --model <model> --effort medium --tools "" --no-session-persistence --output-format json`. Elke run een nieuwe sessie zonder tools. `--output-format json` is toegevoegd, zodat de tokens en de kost uit de uitvoer te lezen zijn. De aanroep draaide vanuit een scratchpad-map, niet vanuit je eigen map, zodat `CLAUDE.md` en `context.md` niet meegaan.
- **Scoreregel:** dezelfde als in `foutmarge.md`: juist als de lijst exact de verwachte opdrachten en deadlines bevat.

## Setups

| Setup | Model | Effort |
|---|---|---|
| A | Sonnet 5.5 (`claude-sonnet-5-5`) | medium |
| B | Haiku 5.5 (`claude-haiku-5-5`) | medium |
| C | Opus 5.5 (`claude-opus-5-5`) | medium |

## Resultaat

Gedraaid op 21 oktober 2026: 27 aanroepen, 1 run per setup per input. Score volgens dezelfde regel als in `foutmarge.md`. De verwachte antwoorden zijn niet aangepast.

| Setup | Model | Score (n = 9, 1 run) | Juist bij | Output per run (gem.) | Waarvan denken (gem.) | Kost per run | Per maand (20 runs) |
|---|---|---:|---|---:|---:|---:|---:|
| A | Sonnet 5.5 | 1/9 | T09 | 224 | 74 | $0,0139 | $0,28 |
| B | Haiku 5.5 | 0/9 | (geen) | 730 | 584 | $0,0009 | $0,02 |
| C | Opus 5.5 | 2/9 | T07, T09 | 308 | 167 | $0,0295 | $0,59 |

Per input:

| Input | A | B | C |
|---|:-:|:-:|:-:|
| T01 Advanced AI | ✗ | ✗ | ✗ |
| T02 Digital Business | ✗ | ✗ | ✗ |
| T04 Financieel Management | ✗ | ✗ | ✗ |
| T05 Français | ✗ | ✗ | ✗ |
| T06 Marketingcommunicatie | ✗ | ✗ | ✗ |
| T07 Marktonderzoek | ✗ | ✓ | ✓ |
| T08 Aankondigingen | ✗ | ✗ | ✗ |
| T09 Modules ERP | ✓ | ✗ | ✓ |
| T10 Aankondigingen MARCOM | ✗ | ✗ | ✗ |

- **Kost:** `total_cost_usd` uit de uitvoer van Claude Code. Per run zit er ongeveer 5.400 tokens prompt en input in (inclusief cache). Haiku is ongeveer 15 keer goedkoper dan Sonnet en ongeveer 33 keer goedkoper dan Opus.
- **Output:** Haiku schrijft het meeste, vooral denkwerk: 584 van de 730 tokens. Sonnet denkt het minst.
- **Foutmarge:** de score ligt op 0 tot 2 van de 9. Met één run per setup is het verschil tussen de drie setups binnen de foutmarge.
- **Let op bij de scores:** T01, T02, T04 en T05 tellen met de huidige verwachte kolom voor geen enkel model als juist. In je `log.md` staat al dat die kolommen alleen je eerste lijst zijn. Met die vier inputs meet de test dus vooral de verwachte kolom. Alleen T07 en T09 laten verschil zien tussen de setups.
- **Vorige meting:** de vorige resultaatsectie (commit `44a2146`) had dezelfde scores (1, 0 en 2 van de 9), maar andere tokenaantallen en kosten. Die is hier vervangen. De oude versie staat nog in de git-geschiedenis.

**Mijn gok klopte niet.** Ik verwachtte dat Sonnet het best zou scoren. Opus scoorde het hoogst (2/9), Sonnet 1/9, Haiku 0/9. Het verschil tussen Sonnet en Opus is één input, dus binnen de foutmarge.

**Conclusie:** op score zijn de setups niet van elkaar te onderscheiden. Op kost is Haiku het goedkoopst, ongeveer 15 keer goedkoper dan Sonnet. Met één run per setup kan ik niet bewijzen dat Haiku even goed is. Een schone vergelijking vraagt meer runs per setup, en eerst de verwachte kolommen van de vier inputs nakijken.
