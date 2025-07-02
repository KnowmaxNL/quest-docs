---
title: Online en offline documentversies
permalink: /topics/online-offline-docs
category: Onderwerpen
order: 21
---

In Knowmax Quest kunnen [documentversies](/topics/document-structure) de status **online** of **offline** hebben. Alleen valide versies kunnen de status online hebben. Een valide versie is een versie zonder fouten die de werking van de documentversie belemmeren. Knowmax Quest [importers](/concepts/importers) bepalen automatisch of een document valide is of niet. Binnen de beheeromgeving van Knowmax Quest kunnen versies handmatig als online of offline worden ingesteld.

Alle endpoints van de API geven standaard alleen versies met status online terug tenzij expliciet anders is aangegeven in de documentatie. Wat je terugkrijgt bij het opvragen van een offline versie kan per endpoint verschillen. Het endpoint ```GET api/document/data``` geeft bijvoorbeeld een HTTP 404 fout. Het endpoint ```GET api/document/info``` zal resultaat geven over het gevonden document, maar niet over de gevraagde documentversie. In het resultaat zal de parameter **located** de waarde **false** hebben.

# Offline versies opvragen
Door de parameter **allowoffline** met waarde **true** aan het verzoek toe te voegen, zullen ook offline versies worden gegeven. Het is een _best practice_ eindgebruikers nooit documentversies aan te bieden met de offline markering.

# Voorbeelden
Stel versie **2** van document **pubs/regeling-abc** heeft de status **offline**. Het volgende verzoek zal dan geen resultaat geven omdat de versie offline is:
```
GET https://quest.knowmax.nl/api/document/info/pubs/regeling-abc/hfd1[2]
```
Door met de parameter **allowoffline** expliciet aan te geven dat het opvragen van een versie met status **offline** is toegestaan, zal het verzoek wel resultaat geven:
```
GET https://quest.knowmax.nl/api/document/info/pubs/regeling-abc/hfd1[2]?allowoffline=true
```