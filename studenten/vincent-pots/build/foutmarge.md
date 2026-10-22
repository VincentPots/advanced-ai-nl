# Foutmarge: prompt v3 en v4

Datum: 21 oktober 2026

## Opzet

- **Model:** `claude-haiku-5-5` (het model van je testset, volgens `kosten.md`).
- **Aanroep:** `claude -p --tools "" --model claude-haiku-5-5 --no-session-persistence`. Elke run is een nieuwe, aparte sessie zonder tools. Het model kreeg alleen de prompt en de input. De verwachte antwoorden zijn niet meegegeven.
- **Codex:** niet gebruikt. `codex` is op deze machine niet geïnstalleerd.
- **Inputs:** T01, T02, T04, T05, T06, T07, T08, T09, T10 (9 stuks). **T03 is weggelaten.** De vakpagina ERP staat als voorbeeld in de prompt zelf, dus die test is niet eerlijk. Dat staat ook in je log.
- **Runs:** 3 per versie per input, dus 54 runs. Alle 54 zijn gelukt.
- **Verwachte antwoorden:** de kolom "Juiste antwoord" uit `test-set.md`, ongewijzigd.

### Welke versie is welke

- **v4** = `build/prompt.md`, je laatste versie.
- **v3** = `build/prompt-v3.md`. Die heb ik gereconstrueerd uit `log.md`: in v4 is alleen de definitie van een opdracht in regel 9 veranderd. v3 heeft de oude definitie terug, zonder "en waarvoor in de tekst zelf staat wat of wanneer" en zonder de zin over koppen zoals "Exam information". De rest is gelijk. Het is dus geen exacte kopie van wat je toen draaide. Heb je v3 ergens anders bewaard, vervang het dan en draai opnieuw.

### Scoreregel

Een run is **juist** (✓) als de lijst precies de verwachte opdrachten en deadlines bevat, zoals in de kolom "Juiste antwoord". Kleine verschillen in woordkeus, jaartal en hoofdletters tellen niet mee. Dit telt wel als **fout** (✗):

- een extra opdracht
- een extra datum (bv. "beschikbaar tot")
- een toelichting tussen haakjes, een link of een extra uur dat niet in de verwachte kolom staat
- een ontbrekende opdracht of deadline
- "geen duidelijke deadline" waar de verwachte kolom een deadline heeft, of andersom

De score per run is het aantal juiste inputs op 9.

## Resultaat

| Versie | Run 1 | Run 2 | Run 3 | Laagste | Hoogste |
|---|---|---|---|---|---|
| v3 (gereconstrueerd) | 1/9 | 1/9 | 1/9 | 1/9 | 1/9 |
| v4 (huidig) | 1/9 | 0/9 | 1/9 | 0/9 | 1/9 |

## Per input

| Input | v3 r1 | v3 r2 | v3 r3 | v4 r1 | v4 r2 | v4 r3 |
|---|---|---|---|---|---|---|
| T01 Advanced AI | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T02 Digital Business | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T04 Financieel Management | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T05 Français | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T06 Marketingcommunicatie | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T07 Marktonderzoek | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ |
| T08 Aankondigingen | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T09 Modules ERP | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| T10 Aankondigingen MARCOM | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |

Waarom de fouten:

- **T01:** deadline 23:59 in plaats van 23:49, plus een toelichting tussen haakjes.
- **T02:** negen opdrachten in plaats van één.
- **T04:** vijf opdrachten in plaats van één.
- **T05:** één of meer extra opdrachten naast "L'entreprise de demain".
- **T06:** de extra datum "beschikbaar tot jan 31" staat erbij.
- **T07 v4 r2:** toelichting tussen haakjes ("achterstallig, 0/1 pt, geen inlevering"). De andere runs zijn juist.
- **T08:** geen van de runs heeft precies "Eerste post — vrijdag 2 oktober (deadline verlengd)". Wel heeft v3 r3 de marker "[DEADLINE VERLENGD]", maar met een link en het uur erbij. v4 r3 heeft de marker ook, met een link naar `https://canvas` die niet in de tekst staat.
- **T09:** de verwachte uitkomst is "geen opdrachten gevonden". Alle runs zetten er oefeningen van Odoo-lessen bij.
- **T10:** alle runs hebben een extra item voor de groepen 9, 12, 21 en 22, en de inschrijving krijgt "geen duidelijke deadline" in plaats van "asap".

## Claim uit week 3

Claim (week 3): de wijziging van v3 naar v4 zorgt dat het model geen dingen meer opneemt die geen opdracht zijn.

**Ingetrokken.** De laagste score van v4 (0/9) ligt niet hoger dan de hoogste van v3 (1/9), en de bereiken overlappen. Het verschil valt binnen de foutmarge. Bij T09 nam v4 nog steeds drie items op die geen opdracht zijn, net als v3. Niet slechter, maar ook niet bewezen beter.

## Let op bij het lezen

- **Verwachte antwoorden T01, T02, T04 en T05 zijn op 22 oktober nagekeken en kloppen.** De kolommen zijn dus niet gewijzigd, en de scores in deze test zijn eerlijk gemeten. Eerder vermoedde ik dat die kolommen de eerste lijst van de student waren. Dat was niet zo.
- **Drie runs per versie is weinig.** Het verschil van 1/9 tussen v3 en v4 komt door één run (T07 v4 r2, een toelichting). Dat is geen bewijs dat v3 beter is.
- **Ruwe uitvoer:** `/private/tmp/claude-501/-Users-vincentpots-Documents-advanced-AI-advanced-ai-nl-studenten-vincent-pots/4c00a925-793a-4994-80d1-0a54afcdf2f3/scratchpad/runs/`, één bestand per run (`v3-t01-r1.out` t/m `v4-t10-r3.out`). De v3-prompt staat in `build/prompt-v3.md`.
