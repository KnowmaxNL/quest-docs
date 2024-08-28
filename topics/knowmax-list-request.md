---
title: Knowmax List Request
permalink: /topics/knowmax-list-request
category: topics
---

Voor verschillende endpoints die gebruikt worden om een lijst van data op te vragen, wordt gebruik gemaakt van een Knowmax List Request om de opgevraagde lijst te definiëren. 

Zo kunnen instellingen voor sortering, filtering en paging worden meegegeven.

## Eigenschappen
Een Knowmax List Request wordt als JSON in de body van een POST verzoek aan een lijst endpoint meegegeven. De volgende eigenschappen kunnen worden meegegeven:

***Request body ```application/json```***
```json
{
  "orderBy": "field1 asc, field2 desc",
  "search": "",
  "filter": "field1 eq 'value1' and field2 gt 10",
  "take": 10,
  "skip": 0,
  "count": true
}
```

### orderBy
Gebruikt voor sortering. Naam van veld gevolgd door ***asc*** voor oplopende sortering of ***desc*** voor aflopende sortering. Meerdere velden kunnen gescheiden worden door een komma. Sorteerrichtng is standaard ***asc***.

### search
Gebruikt voor full text zoekopdrachten. Beschikbaarheid en implementatie afhankelijk van endpoint.

### filter
Beperk resultaten door een filter op te geven. Filter bestaat uit een veldnaam, een operator en een waarde. Meerdere filters kunnen gecombineerd worden met ***and***. 

Operator | Omschrijving
--- | ---
eq | gelijk aan
ne | niet gelijk aan
gt | groter dan
ge | groter of gelijk aan
lt | kleiner dan
le | kleiner of gelijk aan
contains | bevat (Afhanklijk van implementatie, niet voor alle velden beschibaar)

Tekstuele waarden kunnen zonder enkele quotes worden opgegeven, waarden met spaties moeten tussen enkele quotes worden geplaatst. Getallen altijd zonder quotes. Datum en datum-tijd waarden moeten in ISO 8601 formaat worden opgegeven.

### take
Gebruikt voor paging. Geeft met een getal aan hoeveel resultaten opgevraagd moeten worden. Standaard is de waarde ***10***.

### skip
Gebruikt voor paging. Geeft met een getal aan hoeveel resultaten overgeslagen moeten worden. Standaard is de waarde ***0***.

### count
Geef waarde ***true*** om het totaal aantal resultaten te laten berekenen en mee te geven in de response. Geef waarde ***false*** om dit niet te doen. Standaard is de waarde ***false***.


