# Modeltest: welk model en welke effort

Datum: 21 oktober 2026

## Mijn gok (vóór de runs)

Ik verwacht dat **setup A (Sonnet 5.5, effort medium)** het best scoort op mijn testset. Ik gok dat Haiku 5.5 (B) minder goed scoort en Opus 5.5 (C) niet veel beter dan Sonnet.

## Opzet

- **Prompt:** v4 (`build/prompt.md`), dezelfde als de foutmarge.
- **Inputs:** T01, T02, T04 t/m T10 (9 stuks). T03 weggelaten, zoals in de foutmarge.
- **Runs:** 2 per setup per input, 54 aanroepen in totaal. Run 1 is de eerste serie, Run 2 is de herhaling.
- **Verwachte antwoorden:** de kolom "Juiste antwoord" in `test-set.md`. Voor T02, T04 en T05 zijn die bijgewerkt naar de volledige lijsten, voordat run 2 is gedraaid. Voor de rest zijn ze ongewijzigd.
- **Effort:** medium voor alle drie, zodat alleen het model verschilt.
- **Aanroep:** `claude -p --model <model> --effort medium --tools "" --no-session-persistence --output-format json`. Elke run een nieuwe sessie zonder tools. `--output-format json` is toegevoegd, zodat de tokens en de kost uit de uitvoer te lezen zijn. De aanroep draaide vanuit een scratchpad-map, niet vanuit je eigen map, zodat `CLAUDE.md` en `context.md` niet meegaan.
- **Scoreregel:** dezelfde als in `foutmarge.md`: juist als de lijst exact de verwachte opdrachten en deadlines bevat. Kleine verschillen in woordkeus, jaartal en hoofdletters tellen niet mee. Een extra toelichting tussen haakjes, een extra datum of een extra opdracht telt wel als fout.

## Setups

| Setup | Model | Effort |
|---|---|---|
| A | Sonnet 5.5 (`claude-sonnet-5-5`) | medium |
| B | Haiku 5.5 (`claude-haiku-5-5`) | medium |
| C | Opus 5.5 (`claude-opus-5-5`) | medium |

## Resultaat

| Setup | Model | Score run 1 | Score run 2 | Gem. score | Output run 1 / run 2 | Kost per run (gem.) | Per maand (20 runs) |
|---|---|---:|---:|---:|---:|---:|---:|
| A | Sonnet 5.5 | 2/9 | 2/9 | 2,0 | 224 / 210 | $0,0098 | $0,20 |
| B | Haiku 5.5 | 3/9 | 2/9 | 2,5 | 730 / 661 | $0,0008 | $0,02 |
| C | Opus 5.5 | 4/9 | 3/9 | 3,5 | 308 / 319 | $0,0205 | $0,41 |

Per input (run 1 / run 2):

| Input | A | B | C |
|---|:-:|:-:|:-:|
| T01 Advanced AI | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T02 Digital Business | ✓ / ✓ | ✓ / ✓ | ✓ / ✓ |
| T04 Financieel Management | ✗ / ✗ | ✓ / ✗ | ✓ / ✗ |
| T05 Français | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T06 Marketingcommunicatie | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T07 Marktonderzoek | ✗ / ✗ | ✓ / ✓ | ✓ / ✓ |
| T08 Aankondigingen | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T09 Modules ERP | ✓ / ✓ | ✗ / ✗ | ✓ / ✓ |
| T10 Aankondigingen MARCOM | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |

- **Kost:** `total_cost_usd` uit de uitvoer van Claude Code. De kost van run 2 is lager dan die van run 1, omdat de prompt dan al in de cache zit. Het gemiddelde is het gemiddelde van de twee runs. Haiku is ongeveer 12 keer goedkoper dan Sonnet en ongeveer 25 keer goedkoper dan Opus.
- **Output:** Haiku schrijft het meeste, vooral denkwerk: gemiddeld 521 van de 696 tokens over de twee runs. Sonnet denkt het minst.
- **Foutmarge:** de scores liggen tussen 2 en 4 van de 9, over twee runs. Het verschil tussen de setups is één of twee inputs. Met twee runs per setup is dat binnen de foutmarge.
- **Let op bij de scores:** T05 is door geen enkel model juist, want elk model vindt twee of drie opdrachten die net anders zijn dan de verwachte drie. T06, T08 en T10 falen vrijwel altijd op een extra datum, een beschrijving of een extra opdracht. Dat zijn scoreregel-fouten, geen grote inhoudelijke fouten.
- **Handmatig scoren:** ik heb de runs met de hand tegen de kolom gelegd. Twee keuzes kunnen anders uitpakken: ik heb een ontbrekende jaarvermelding tussen haakjes niet als fout gerekend, en ik heb "beschikbaar tot" met een puntkomma in plaats van haakjes als gelijk gerekend.

**Mijn gok klopte niet.** Ik verwachtte dat Sonnet het best zou scoren. Opus scoort gemiddeld het hoogst (3,5/9), gevolgd door Haiku (2,5) en Sonnet (2,0). Het verschil tussen Opus en Sonnet is anderhalve input, dus binnen de foutmarge.

**Conclusie:** op score zijn de setups met twee runs niet van elkaar te onderscheiden. Op kost is Haiku het goedkoopst, en Sonnet kost ongeveer 12 keer zoveel per run en Opus ongeveer 25 keer zoveel. Een schone vergelijking vraagt meer runs per setup, en een scoreregel die de kleine verschillen niet als fout telt.
