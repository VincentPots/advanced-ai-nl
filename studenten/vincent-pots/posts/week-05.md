# Week 5: Goedkoop is mijn tool, goed nog niet

## Mijn foutmarge

In week 3 schreef ik: "Ik verwachtte dat mijn model na de wijziging geen dingen meer zou opnemen die geen opdracht waren." Die verwachting trek ik in, want de bereiken overlappen: v4 is niet aantoonbaar beter dan v3.

Ik draaide Haiku 5.5 op 9 inputs, 3 runs per versie, samen 54 runs. Versie 4 scoorde 1, 0 en 1 op 9, dus een bereik van 0 tot 1. Versie 3 scoorde drie keer 1 op 9. Die van v3 heb ik uit mijn log gereconstrueerd, geen exacte kopie.

## Model en effort

Ik gokte vooraf dat Sonnet 5.5 (setup A) het best zou scoren. Dat klopte niet. Op effort medium, met 9 inputs en 2 runs per setup, scoorde A gemiddeld 2,0 op 9 ($0,0098 per run), B (Haiku 5.5) 3,5 op 9 ($0,0008) en C (Opus 5.5) 3,5 op 9 ($0,0205). De kosten zijn niet betrouwbaar gemeten (kosten.md). Ik zet B in productie, omdat B even hoog scoort als C en het goedkoopst is.

## Mijn value chain

Handwerk kost 5 minuten (een schatting, niet gemeten). Met de tool kost het 2 minuten, dus ik win 3 minuten per run. Ik gebruik de tool 3 keer per week in 30 lesweken (een aanname): 90 runs en 4,5 uur per jaar. Bij een uurkost van €25,50 voor de werkgever is dat €114,75 per jaar. De tool kost ongeveer €0,36 per jaar (1 dollar = 0,90 euro, een aanname), dus netto ongeveer €114,39. Als het handwerk maar 3 minuten kost, blijft ongeveer €37,89 over. Mijn zwakste cijfer is die 5 minuten handwerk.

## Mijn dashboard

Publieke link: https://claude.ai/artifact/WkukwseEuoF86uorou43F7

## Mijn AI-ismen

> Dat past bij mijn prompt, want een opdracht te veel is minder erg dan een die ontbreekt. (week 4)

Patroon: "want"-redenering. Herschreven: Liever een opdracht te veel in de lijst dan eentje te weinig, zo staat het in mijn prompt.

> De kost van de tool is bijna niets. Het getal hangt vooral af van de minuten, en die zijn geschat. (week 4)

Patroon: afgeronde samenvattingszinnen. Herschreven: De tool kost ongeveer €0,36 per jaar en de 3 minuten winst per run heb ik geschat.

> Een bedrijf dat mijn tool via de API gebruikt, betaalt alleen mijn deel, dus de bovengrens is ruim. (week 4)

Patroon: "dus"-conclusie. Herschreven: Via de API betaalt een bedrijf waarschijnlijk minder dan mijn €0,36 per jaar, want mijn bedrag bevat ook de context van Claude Code.

> Mijn conclusie blijft dan dezelfde: de tool is de moeite, zolang ik de lijst nakijk op te veel. (week 4)

Patroon: afsluiter met "dezelfde conclusie". Herschreven: Bij 3 minuten handwerk houd ik nog €37,89 per jaar over.

> Wat opvalt: in mijn 5 tests miste de tool geen enkele opdracht. De fouten zijn altijd te veel in de lijst, nooit te weinig. (week 4)

Patroon: "Wat opvalt:" en "altijd…, nooit…". Herschreven: In mijn 5 tests van 13 oktober (T06 tot en met T10, prompt v2) miste de tool nooit een opdracht, en bij elke fout stonden er extra items of toelichtingen in.

## Mijn testset groeit

Set v2 loopt van T01 tot en met T20 en is van 27 oktober. T11 tot en met T20 zijn tien nieuwe, echte inputs. Ik stopte bij 20 in plaats van 30, omdat T14 al meer dan een kwartier kostte. Per vakpagina gebruikte ik de opdrachten, de modulepagina en de aankondigingen als input.

Het meest verraste me T17: de tool nam tien extra items op. Bij T09 waren het er drie extra, dus zoveel had ik niet verwacht.

Mijn score op set v2 is 9 op 20 juist (n = 20, 1 run, prompt v4 op Haiku). De 💪-regel is nog niet vastgelegd: als er 💪 bij staat, kan het beide zijn, een opdracht of geen opdracht. Het symbool maakt dus niet uit. Daardoor blijft vergelijken met v1 onzeker.
