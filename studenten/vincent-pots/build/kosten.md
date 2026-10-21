# Kosten — Vincent Pots

Datum: 14 oktober 2026
Koers: 1 dollar = 0,90 euro (aanname)
Model: `claude-haiku-5-5` (niet Haiku 4.5 uit de tabel van de README)
Prijs Haiku 5.5: $0,10 per miljoen input-tokens, $0,50 per miljoen output-tokens (cache lezen $0,01). Bron: derde partijen (Artificial Analysis, VentureBeat, MarkTechPost), nog niet op de officiële pagina gecontroleerd.

**Gecorrigeerd in week 5 (21 oktober 2026):** de prijs klopt, en staat nu op de officiële pagina. Bron en herberekening: zie "Correctie week 5" hieronder.

| Model | Context (`/context`) | Totaal (`/cost`) | Jouw deel | Kost per run | Per maand, jouw volume | 10× | 1.000× |
|---|---:|---:|---:|---:|---:|---:|---:|
| Haiku 5.5 | ± 18.400 tot 20.100 | 20.282 (19.736 in + 546 uit) | niet betrouwbaar (−321 tot +1.372) | $0,0021 per sessie (transcript); jouw deel onzeker | n.b. | n.b. | n.b. |
| Sonnet 5.5 (berekend) | | | | n.b. | n.b. | n.b. | n.b. |

n.b. = niet bepaald. De kost per run van $0,0039 uit eerdere metingen komt niet overeen met de transcripts en is vervallen. Daarom zijn de kolommen per maand, 10× en 1.000× niet meer ingevuld.

## Sonnet 5.5: hoe berekend
- Niet gemeten. Sonnet 5.5 kost op input en output 20× zoveel als Haiku 5.5 (2 en 10 dollar tegenover 0,10 en 0,50 per miljoen tokens). Een getal per run kan pas na een schone meting, want de kost van Haiku is nog niet betrouwbaar vastgesteld.
- Voorbehoud 1: deze verhouding klopt alleen als de prijs van Haiku 5.5 klopt, en die komt uit derde partijen. Is die prijs anders, dan verandert ook de verhouding.
- Voorbehoud 2: ik ga ervan uit dat Sonnet evenveel tokens gebruikt als Haiku. Sonnet kan anders denken. Voor een echt cijfer: dezelfde meting draaien met `/model sonnet`.

## Hoe gemeten
Bron: de transcripts van de sessies in de scratchpad-map `meting` (14 oktober 2026). Elke sessie is hier één aanroep van het model, met de `usage` en `costUSD` die Claude Code opslaat.

| Sessie | Input (uncached + cache-write + cache-read) | Output (waarvan denken) | Kost (transcript) |
|---|---|---|---|
| "hoi" (547908aa) | 2 + 11.447 + 8.608 = 20.057 | 90 (69) | $0,0024 |
| "hoi" (5fa601f3) | 2 + 6.648 + 11.714 = 18.364 | 151 (0) | $0,0015 |
| Prompt + T01 (ddf35265) | 2 + 8.481 + 11.253 = 19.736 | 546 (490) | $0,0021 |

- De prompt-sessie is meting 2. De "hoi"-sessies zijn de context: het bericht "hoi" erbij is klein.
- Vorige cijfers ($0,0003, $0,0042 en $0,0039 per run) komen niet overeen met deze transcripts. Ze zijn vervallen.
- Jouw deel is niet betrouwbaar te bepalen. De prompt-sessie heeft minder input (19.736) dan "hoi"-sessie 1 (20.057). De cache-writes verschillen per sessie, en die wegen het zwaarst.

## Meting 3: eigen map, 19 oktober 2026

Sessie `070b07d4` (10:19), in `studenten/vincent-pots/`. Prompt v4 en T01 in één bericht, `/model haiku`, één aanroep van het model.

| Onderdeel | Tokens (transcript) |
|---|---|
| Input, niet uit cache | 2 |
| Cache-write | 17.137 |
| Cache-read | 24.796 |
| **Totale input** | **41.935** |
| Output (waarvan denken) | 704 (650) |

- `/cost`: **$0,0044** voor de hele sessie. Het zegt 2,6k input en 1,0k output; het transcript 2 en 704. Totaal input en kost komen overeen.
- `/context` is niet gelukt. Daarom is de context van deze meting niet gemeten, en is **jouw deel niet bepaald**. De totale input is wel bekend: 41.935 tokens.
- Waarschijnlijk is de context groter dan in de scratchpad-meting (19.736). Deze sessie laadt `CLAUDE.md`, `AGENTS.md` en `context.md` mee; die sessie niet. Dat is niet gecontroleerd.

## Volume
20 runs per maand = 5 dagen per week × 4 weken. Bron: schatting van mijn eigen gebruik (elke werkdag deadlines checken), niet geteld.

## Correctie week 5 (21 oktober 2026)

Bron: [Anthropic, pricing](https://platform.claude.com/docs/en/about-claude/pricing), tabel "Model pricing", rij "Claude Haiku 5.5 (for prompts up to 100,000 tokens)". Alle prompts in deze metingen zijn kleiner dan 100.000 tokens, dus geldt het lage tarief. Boven de 100.000 tokens is Haiku 5.5 vijf keer duurder.

Prijs per miljoen tokens: input $0,10 · cache-write $0,125 (5 minuten) of $0,20 (1 uur) · cache-read $0,01 · output $0,50.

Herberekend uit de transcripts, per aanroep:

| Meting | Totale input | Output | Kost, cache-write 1 uur | Kost, cache-write 5 minuten | Per maand (20 runs), 1 uur |
|---|---:|---:|---:|---:|---:|
| 2 (ddf35265) | 19.736 | 546 | $0,0021 | $0,0015 | $0,042 |
| 3 (070b07d4) | 41.935 | 704 | $0,0040 | $0,0027 | $0,081 |

- Meting 2 klopt met het `costUSD` uit het transcript ($0,0021) bij het tarief voor cache-write van 1 uur.
- Meting 3: het transcript zegt $0,0044, de herberekening $0,0040. Dat verschil is niet verklaard.
- Welk cache-tarief Claude Code gebruikt, is niet gecontroleerd. Het tarief van 1 uur past bij meting 2.
- Dit is de kost van één volledige sessie, met de context erbij. Jouw eigen deel is nog niet bepaald.

## Nog open
- Context van meting 3 ontbreekt (`/context` is niet gelukt). Zonder die context is jouw deel niet te bepalen.
- Verklaren waarom `/cost` in de live sessie $0,0042 gaf, terwijl het transcript $0,0021 laat zien.
- Verklaren waarom het transcript van meting 3 $0,0044 zegt, terwijl de herberekening $0,0040 geeft.
- ~~Prijs van Haiku 5.5 op de officiële pagina controleren~~: gedaan in week 5, zie "Correctie week 5".
- Een ander model met hetzelfde volume doorrekenen (ronde 2, stap 4).
