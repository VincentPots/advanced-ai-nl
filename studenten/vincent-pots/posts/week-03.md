# Week 3 — Eén run zegt weinig: wat mijn testgevallen me leerden

## Wat ik testte en veranderde

Ik testte mijn prompt op een reeks testgevallen (T01 tot T10) en paste hem stap voor stap aan.

In v2 verzon het model een item dat nergens in de tekst stond. In v3 werd dat item anders geformuleerd (item 4), en het model zei zelf dat de inhoud en de indiening niet beschreven waren. Dat was een verbetering, maar het item bleef bestaan.

In v4 voegde ik een duidelijke regel toe: een kop zonder inhoud is geen opdracht. Een opdracht moet in de tekst zelf zeggen wat er moet gebeuren of wanneer. Daarna werd het interessanter, want de uitkomsten bleven schommelen:

- T09 gaf op 13 oktober drie items en op 16 oktober geen.
- T10 was in run 1 juist en had in run 2 één item te veel.
- T05 had in run 1 alle vier de items en miste er in run 2 één.

## Wat ontbrak er in mijn context?

Het model miste in de brontekst wat een opdracht eigenlijk is. Bij een kop zonder inhoud stond er nergens wat er moest gebeuren of wanneer het moest ingeleverd worden. Het model wist dat dus niet, en vulde die leemte zelf op met een verzonnen item (v2). In v3 zag het model de leemte wel, maar nam het de kop toch op als item. Pas met de regel in v4 kreeg het model de context die het nodig had om te beslissen: geen inhoud in de tekst, geen opdracht.

Daarnaast ontbrak er iets in mijn eigen context. Ik had niet bij elke run de promptversie vastgelegd. Daardoor kan ik bij T09 niet nagaan of de run van 13 oktober dezelfde versie gebruikte als die van 16 oktober, en kan ik het verschil niet toeschrijven aan de prompt, de input of toeval.

## Mijn eerste cijfer

Mijn eerste cijfer voor mijn eigen prompt is 12 op 20 juist (n = 10, 2 runs). Dat is 60%, dus een voldoende. De 8 fouten verdelen zich als volgt: in run 1 waren er 3, allemaal F4 (T02, T04, T06); in run 2 waren er 5, namelijk F4 (drie keer), F3 (één keer) en F1 (één keer). In totaal zijn dat dus 6 keer F4, 1 keer F3 en 1 keer F1. De meeste fouten zijn dus F4. De aanleiding voor v4 waren de verzonnen en te veel opgenomen items bij T09 en T10, en dat zijn geen F4-fouten. Omdat de uitkomsten ook nog wisselen tussen runs, durf ik niet hoger in te schatten.

## Eén wijziging

Ik denk dat de uitkomst van een run zelf kan wisselen, ook zonder dat de prompt verandert. Zeker weten doe ik dat niet, want ik kon de versie van 13 oktober niet controleren. Wat ik wel weet: één run zegt weinig. Je moet elk testgeval meerdere keren draaien voordat je besluit of een wijziging echt heeft geholpen. Ik ga daarom bij elke run de promptversie en de datum noteren, zodat ik later wel kan nagaan wat er precies is getest.
