---
title: Metadata definities
permalink: /concepts/metadata
---

Knowmax Quest kan voor documenten, documentversies, documentnodes en collecties metadata vastleggen. Voor ieder soort metadata is een metadatadefinitie beschikbaar die een beschrijving geeft van het soort metadata. Iedere metadatadefinitie hoort bij een familie van metadatadefinities.

Bij Knowmax Quest generatie 4 worden de metadatadefinities direct gebruikt voor de zoekindex. Vanaf Knowmax Quest generatie 5 zijn er aparte indexdefinities beschikbaar. Deze indexdefinities kunnen verwijzingen naar meerdere metadatadefinities bevatten.

De API van Knowmax Quest heeft verschillende endpoints om met metadata te werken.

# Beschikbare metadata definities
Er is een overzicht met alle beschikbare metadatadefinities. Tijdens het [importeren](/concepts/importers) van documenten worden metadatadefinities automatisch aangemaakt indien deze voor een bepaald soort metadata nog niet bestaan. 

Er bestaat ook standaard metadata die Knowmax Quest automatisch voor alle documenten beheerd. De metadatadefinities voor deze standaard metadata kunnen niet bewerkt worden. 

# Identificatie
De identificatie van metadatadefinities is opgebouwd uit een label en het label van de familie waar de metadatadefinitie onderdeel van is. Binnen een familie moeten de labels van metadatadefinities uniek zijn. 

# Meerdere waarden voor metadatadefinitie
Er kunnen meerdere waarden voor metadata volgens een bepaalde metadatadefinitie voorkomen voor een document, documentversie of documentnode. Als voor een metadatadefinitie meerdere waarden zijn toegestaan, moeten scheidingstekens (fieldMultiValueSeparators) om meerdere waarden te herkennen gedefinieerd zijn voor die metadatadefinitie. 

De endpoints voor het muteren van metadata zullen de waarden voor een bepaalde metadatadefinitie splitsen op basis van de eventueel ingestelde scheidingstekens.

## Voorbeeld: scheidingstekens ```,/;```

Waarde | Interpretatie
---|---
a,b,c | 3 waarden: a, b en c
a;b;c | 3 waarden: a, b en c
a/b;c | 3 waarden: a, b en c
a-b,c | 2 waarden: a-b en c

## Achteraf instellen van scheidingstekens
Als de scheidingstekens voor de metadatadefintie tijdens het vastleggen van de waarde niet opgegeven zijn, zal de waarde als één waarde worden opgeslagen. Als na het vastleggen van de waarde scheidingstekens worden gedefinieerd, zullen de waarden die al zijn vastgelegd niet worden gesplitst. Mochten waarden van deze metadatadefinitie gebruikt worden in een zoekindex, dan zal de indexer van het zoeksysteem de waarden alsnog splitsen.

## Importers
Voor metadata die tijdens het importeren van documenten door de [importer](/concepts/importers) worden vastgelegd, wordt geen gebruik gemaakt van de scheidingstekens. Importers hanteren hun eigen regels om voor een bepaalde metadatadefinitie meerdere waarden vast te leggen. 

# Datatype hint
Alle waarden voor metadata worden als tekst opgeslagen. Met een datatype hint kan worden aangegeven hoe de waarde te interpreteren is. Het ingebouwde zoeksysteem kan deze hint gebruiken om metadata op de juiste wijze te indexeren. Daarnaast kunnen specifieke client systemen de hint gebruiken om de metadata op een bepaalde manier te verwerken. De volgende datatypen zijn beschikbaar.

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