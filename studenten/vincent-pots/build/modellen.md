# Modeltest: welk model en welke effort

Datum: 21 oktober 2026

## Mijn gok (vóór de runs)

Ik verwacht dat **setup A (Sonnet 5.5, effort medium)** het best scoort op mijn testset. Ik gok dat Haiku 5.5 (B) minder goed scoort en Opus 5.5 (C) niet veel beter dan Sonnet.

## Opzet

- **Prompt:** v4 (`build/prompt.md`), dezelfde als de foutmarge.
- **Inputs:** T01, T02, T04 t/m T10 (9 stuks). T03 weggelaten, zoals in de foutmarge.
- **Runs:** 2 per setup per input, 54 aanroepen in totaal. Run 1 is de eerste serie, Run 2 is de herhaling.
- **Verwachte antwoorden:** de kolom "Juiste antwoord" in `test-set.md`, zoals die nu staat. Die is gecontroleerd op de paginatekst. Wijzigingen: T02, T04 en T05 zijn volledige lijsten; T01, T05, T08 en T10 zijn na de runs gecorrigeerd. T06 en T09 zijn ongewijzigd.
- **Scores herberekend:** de scores hieronder zijn met de hand opnieuw berekend tegen de nieuwe kolom, met de bestaande outputs. Er zijn geen nieuwe runs gedaan.
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
| B | Haiku 5.5 | 4/9 | 3/9 | 3,5 | 730 / 661 | $0,0008 | $0,02 |
| C | Opus 5.5 | 4/9 | 3/9 | 3,5 | 308 / 319 | $0,0205 | $0,41 |

Per input (run 1 / run 2):

| Input | A | B | C |
|---|:-:|:-:|:-:|
| T01 Advanced AI | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T02 Digital Business | ✓ / ✓ | ✓ / ✓ | ✓ / ✓ |
| T04 Financieel Management | ✗ / ✗ | ✓ / ✗ | ✓ / ✗ |
| T05 Français | ✗ / ✗ | ✓ / ✗ | ✗ / ✗ |
| T06 Marketingcommunicatie | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |
| T07 Marktonderzoek | ✗ / ✗ | ✓ / ✓ | ✓ / ✓ |
| T08 Aankondigingen | ✗ / ✗ | ✗ / ✓ | ✗ / ✗ |
| T09 Modules ERP | ✓ / ✓ | ✗ / ✗ | ✓ / ✓ |
| T10 Aankondigingen MARCOM | ✗ / ✗ | ✗ / ✗ | ✗ / ✗ |

- **Kost:** `total_cost_usd` uit de uitvoer van Claude Code. De kost van run 2 is lager dan die van run 1, omdat de prompt dan al in de cache zit. Het gemiddelde is het gemiddelde van de twee runs. Haiku is ongeveer 12 keer goedkoper dan Sonnet en ongeveer 25 keer goedkoper dan Opus.
- **Output:** Haiku schrijft het meeste, vooral denkwerk: gemiddeld 521 van de 696 tokens over de twee runs. Sonnet denkt het minst.
- **Foutmarge:** de scores liggen tussen 2 en 4 van de 9, over twee runs. Het verschil tussen de setups is één of twee inputs. Met twee runs per setup is dat binnen de foutmarge.
- **Let op bij de scores:** T01, T06 en T10 falen bij alle setups in beide runs. Dat komt door de scoreregel. Een toelichting tussen haakjes, een extra datum of een extra opdracht telt als fout, ook als de rest klopt. T01 bijvoorbeeld: alle modellen zetten de titel met 23:49 tussen haakjes erbij.
- **Handmatig scoren:** ik heb de runs met de hand tegen de kolom gelegd. Drie keuzes kunnen anders uitpakken:
  - een ontbrekende jaarvermelding tussen haakjes heb ik niet als fout gerekend;
  - "beschikbaar tot" met een puntkomma in plaats van haakjes heb ik als gelijk gerekend;
  - T08 bij Haiku run 2 (`2 oktober 2026, 23:59`) heb ik als juist gerekend, want het is dezelfde datum, alleen met het jaar erbij.

**Mijn gok klopte niet.** Ik verwachtte dat Sonnet het best zou scoren. Haiku en Opus scoren gemiddeld even hoog (3,5/9), Sonnet 2,0/9. Het verschil met Sonnet is anderhalve input, dus binnen de foutmarge.

**Conclusie:** op score zijn Haiku en Opus niet van elkaar te onderscheiden, en Sonnet scoort iets lager. Op kost is Haiku het goedkoopst: Sonnet kost ongeveer 12 keer zoveel per run en Opus ongeveer 25 keer zoveel. Een schone vergelijking vraagt meer runs per setup, en een scoreregel die de kleine verschillen niet als fout telt.

## Scores per item

Dezelfde outputs, maar nu per item in plaats van per input. Dat is de regel:

- Een item is **gevonden** als de naam klopt en de deadline klopt. Toelichtingen tussen haakjes, extra datums binnen hetzelfde item en jaartallen tellen niet mee.
- Een item is **fout** als het niet in de verwachte lijst staat, of als de deadline niet klopt.
- Een verwacht item dat ontbreekt, is niet gevonden.
- T09 apart: "geen opdrachten gevonden" klopt of niet.

De verwachte lijst bevat 23 items (T01: 1, T02: 9, T04: 5, T05: 2, T06: 1, T07: 1, T08: 1, T10: 3).

| Setup | Gevonden run 1 | Gevonden run 2 | Fout items run 1 | Fout items run 2 | T09 run 1 / run 2 | Totaal gevonden (van 46) |
|---|---:|---:|---:|---:|:-:|---:|
| A, Sonnet 5.5 | 23/23 | 21/23 | 0 | 2 | ✓ / ✓ | 44 (96%) |
| B, Haiku 5.5 | 20/23 | 22/23 | 5 | 2 | ✗ / ✗ | 42 (91%) |
| C, Opus 5.5 | 21/23 | 23/23 | 3 | 1 | ✓ / ✓ | 44 (96%) |

Waar de fouten zitten:

- **T01:** A run 2, B run 1 en C run 1 zetten 23:49 als deadline. Dat is hier een keuze: de titel noemt 23:49, het veld Inleverdatum zegt 23:59. Ik heb A run 2 als fout gerekend, want het zet beide tijden als deadline.
- **T05:** B run 2 voegt "Tâches à poster lors des cours" toe.
- **T06:** B run 1 zet "jan 31" als deadline, met "dec 1" erachter.
- **T08:** B run 1 voegt "Week 1 indienen via je pull request" toe als tweede opdracht.
- **T10:** bij het item over inschrijven zetten A run 2, B run 1, B run 2 en C run 1 "geen duidelijke deadline" in plaats van "asap". B run 1 en C run 1 en C run 2 voegen "case uitwerken" toe.

**Conclusie per item:** alle drie de setups vinden 91 tot 96% van de verwachte items. Het verschil tussen de setups is twee items op 46. Haiku maakt vooral fouten door extra items toe te voegen. Sonnet en Opus maken fouten in de deadline van één item. De per-item score laat dus zien dat de modellen de inhoud grotendeels goed hebben. De lage input-scores kwamen door de scoreregel.
