---
title: Metadata definities
permalink: /concepts/metadata
---

## Inleiding
Alle voor documenten gevonden metadata wordt vastgelegd. Voor ieder soort metadata is een metadata definitie beschikbaar die een beschrijving geeft van het soort metadata. Deze beschrijving wordt bijvoorbeeld gebruikt tijdens het indexeren van de metadata door het zoeksysteem of het aanbieden van een editor voor het bewerken van specifieke metadata.

## Beschikbare metadata definities
Er is een overzicht beschikbaar van alle definities van in het systeem opgenomen metawaarden. Tijdens het [importeren](/concepts/importers) van documenten worden metadata definities automatisch aangemaakt indien deze voor een bepaald soort metadata nog niet bestaan. Vanuit het overzicht kunnen per metadatadefinitie de eigenschappen worden bekeken en bewerkt.

Er bestaat ook standaard metadata die Knowmax Quest automatisch voor alle documenten beheerd. De metadata definities voor deze standaard metadata kunnen niet bewerkt worden. Er is een overzicht beschikbaar met informatie hoe deze standaard metadata beschikbaar is via het zoeksysteem.

## Identificatie
De primaire identificatie van metadata definities is opgebouwd uit een label en het label van de familie waar de definitie onderdeel van is. Binnen een familie moeten de labels van metadata definities uniek zijn. Naast deze primaire identificatie hebben metadata definities ook een client naam. Dit is een tweede identificatie waarin familie- en metadata identificatie label zijn samengevoegd. De client naam identificatie maakt het gebruik in client applicaties eenvoudiger.

## Datatype hint
Alle waarden voor metadata worden als tekst opgeslagen. Met een datatype hint kan worden aangegeven hoe de waarde te interpreteren. Het ingebouwde zoeksysteem kan deze hint gebruiken om metadata op de juiste wijze te indexeren. Daarnaast kunnen specifieke client systemen de hint gebruiken om de metadata op een bepaalde manier te verwerken. De volgende datatypen zijn beschikbaar.

Parameter | Omschrijving
---|---
Date | Datum notatie volgens [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).
DateTime | Datum en tijd notatie volgens [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).
Boolean	| Gebruik 0 voor false en 1 voor true.
Integer | Geheel getal.
Double | Gebroken getal. Gebruik punt als scheidingsteken.
Textarea | Groot tekstveld.
QuestId	| Kan een refentie naar een Quest document bevatten. Bij het opvragen van dit veld kan Knowmax Quest automatisch de gegevens van het gerefereerde Quest document meegeven.
Markdown | Verrijkte tekst volgens markdown standaard toegestaan. Als het veld opgenomen wordt in de zoekindex zal de inhoud worden omgezet naar tekst zonder verrijking.
Json | Waarde uitgedrukt als JavaScript Object Notation.