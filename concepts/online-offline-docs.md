---
title: Online en offline documentversies
permalink: /concepts/online-offline-docs
---

In Knowmax Quest kunnen versies van documenten de status **online** of **offline** hebben. Alleen valide versies kunnen de status online hebben. Een valide versie is een versie zonder fouten die de werking van de documentversie belemmeren. Knowmax Quest [importers](\concepts\importers) bepalen automatisch of een document valide is of niet. Binnen de beheeromgeving van Knowmax Quest kunnen versies handmatig als online of offline worden ingesteld.

Alle functies van de Web API geven standaard alleen versies met status online terug tenzij expliciet anders is aangegeven in de documentatie. Wat je terugkrijgt bij het opvragen van een offline versie kan per Web API functie verschillen. De functie **Api/Document/Data** geeft bijvoorbeeld een HTTP 404 fout. De **functie Api/Document/Info** zal resultaat geven over het gevonden document maar niet over de gevraagde documentversie. In het resultaat zal de parameter **Located** de waarde **false** hebben.

## Offline versies opvragen
Door de parameter **allowoffline** met waarde **true** aan het verzoek toe te voegen, zullen ook offline versies worden gegeven.

## Voorbeelden
Stel versie **2** van document **docs/regeling-abc** heeft de status **offline**. Het volgende verzoek zal dan geen resultaat geven omdat de versie offline is:
```
http://quest.bris.nl/Api/Document/Info/docs/regeling-abc/hfd1[2]
```
Door met de parameter **allowoffline** expliciet aan te geven dat het opvragen van een versie met status **offline** is toegestaan, zal het verzoek wel resultaat geven:
```
http://quest.bris.nl/Api/Document/Info/docs/regeling-abc/hfd1[2]?allowoffline=true
```