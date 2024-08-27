---
title: Opbouw van een document
permalink: /concepts/document-structure
---

# Document
Een document in Knowmax Quest beschrijft de Quest [identificatie](/concepts/quest-id), de titel en de archiveringsstatus. Een document in Knowmax Quest bevat geen inhoud en is enkel een container waarin verschillende versies van het document zijn ondergebracht.

# Documentversie
Binnen een document kunnen 1 of meerdere versies van het document voorkomen. De versies bevatten de feitelijke inhoud van het document. Iedere versie van een document heeft een uniek volgnummer, een publicatiedatum en optioneel een titel en omschrijving. Daarnaast bevat de documentversie eigenschappen die beschrijven of het document online bechikbaar is en of het beschouwd moet worden als de huidige versie.

# Documentonderdeel
De inhoud van documentversies kan onderverdeeld zijn in onderdelen. Deze onderdelen worden ook wel document nodes genoemd. Een meer exacte benaming zou documentversie-node zijn. Onderdelen kunnen bijvoorbeeld hoofdstukken zijn.

## Root node
Iedere documentversie heeft ten minste 1 documentonderdeel dat geldt als root node. Als de documentversie geen verdere ondervedeling heeft, bevat de root node alle data behorende bij de documentversie. Als de documentversie meerdere onderdelen zoals hoofdstukken heeft, zullen deze als kinderen van de root node worden opgenomen. 

## Document nodes met en zonder data
Een document node kan data bevatten, maar het is ook mogelijk document nodes te hebben zonder data. Dat zijn nodes die enkel als structuuronderdeel dienen voor andere nodes.

## Composeerbare document nodes
Afhankelijk van de gebruikte [importer](/concepts/importers) kan het zijn dat een document is [opgeknipt](/concepts/composition) in onderdelen. Bij een typisch hoofdstuk kunnen bijvoorbeeld de bijbehorende paragrafen als kind nodes zijn opgenomen. Ieder van de paragrafen is dan een document node en kan afzonderlijk worden opgevraagd. Het hele hoofdstuk kan ook opgevraagd worden, met en zonder de bijbehorende paragrafen. Als de bijbehorende paragrafen ook opgevraagd worden bij het opvragen van het hoofdstuk, spreken we van een composeerbare document node.

# Metadata
[Metadata](/concepts/metadata) kan op alle genoemde onderdelen voorkomen. De metadata die tijdens het importeren van de documentversie wordt vastgelegd, is onlosmakelijk met deze versie verbonden en kan niet bewerkt worden. Alle overige metadata is wel bewerkbaar voor gebruikers met de juiste rechten.