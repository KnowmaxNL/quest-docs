---
title: 🗃️ Collecties
permalink: /topics/collections
category: Onderwerpen
order: 5
---

Een collectie beschrijft een verzameling van [documenten](/topics/document-structure) binnen Knowmax Quest. Collecties kunnen worden gebruikt om documenten te groeperen en te ordenen. Een collectie kan bijvoorbeeld een verzameling van documenten zijn die een bepaald onderwerp behandelen of een verzameling van documenten die door een bepaalde auteur zijn geschreven. Zie een collectie als een handmatig aangemaakte verzameling van documenten. 

# Hiërarchie
Onderdelen binnen een collectie kunnen in een hiërarchie geplaatst worden. Ieder onderdeel in de collectie heet een collectie node. Een collectie node kan een titel hebben en kan optioneel naar een [document](/topics/document-structure) of [documentversie](/topics/document-structure) verwijzen. Zonder verwijzing naar een document of documentversie is de collectie node enkel een structuuronderdeel waaronder weer andere collectie nodes kunnen voorkomen.

# Verwijzing naar een document of documentversie
Als een collectie node naar een document of documentversie verwijst, wordt de [Quest identificatie](/quest-id) van het document opgenomen. Een eventuele documentversie wordt in een apart veld aangegeven. Als geen documentversie wordt opgegeven, wordt de huidige actieve versie van het document gebruikt. Er kan niet verwezen worden naar een [documentnode](/topics/document-structure) binnen een documentversie.

Als bij een collectie node met een verwijzing naar een document geen titel wordt opgegeven, wordt automatisch de titel van het document of de documentversie gebruikt. De titel is bij collectie nodes zonder verwijzing naar een document altijd verplicht.

# Metadata
Collecties kunnen metadata bevatten met extra eigenschappen van de gehele collectie.

# API
De endpoints om met collecties te werken bevinden zich in de namespaces die beginnen met **/api/collection** en **/api/collectionnode**.

## Beschikbare collecties opvragen
***Endpoint***
```
POST /api/collection/all
```

Gebruik als body een [Knowmax List Request](/topics/knowmax-list-request) om de gewenste collecties op te vragen.

Beschikbare velden voor sortering en filtering:
| Veldnaam | Omschrijving | Type | Contains |
| --- | --- | --- | --- |
| name | Naam | string | ja |
| label | Label, uniek per collectie | string | ja |
| associatedQuestId | [Quest id](/topics/quest-id) van optioneel document dat associatie heeft met collectie | string | ja |
| id | Interne identificatie van collectie | number | - |
| createdBy | Naam van aanmaker collectie | string | - |
| created | Tijdstip van aanmaken collectie | datetime | - |
| modifiedBy | Naam van wijziger collectie | string | - |
| modified | Tijdstip van laatste wijziging collectie | datetime | - |
| metadata.[FieldName] | Metadata veld. [FieldName] beschrijf metadata en heeft formaat **label van famile**.**label van metadata** | string | - |

## Hiërarchie van nodes in collectie opvragen

***Endpoint***
```
GET /api/collection/hierarchy/{collectionLabel}
```

Geeft alle nodes op root niveau in collectie met label {collectionLabel} terug. Optioneel kan het veld **parentId** gebruikt worden om de nodes onder een specifieke collectie node op te vragen. 