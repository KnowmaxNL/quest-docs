---
title: 🔎 Filtering in Azure AI Search index
permalink: /topics/azure-ai-search-filtering
category: Onderwerpen
order: 12
---

De door Knowmax Quest gebouwde index in Microsoft Azure AI Search bevat verschillende velden die kunnen worden gebruikt voor filtering. Voor iedere index is een set standaardvelden beschikbaar. Daarnaast kunnen er aan de hand van een index veld definitieset extra velden worden toegevoegd die specifiek zijn voor de documenten in Knowmax Quest.

Meer informatie over het toepassen van OData filtering in Microsoft Azure AI Search: [OData Filtering in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-query-odata-filter)

# Standaardvelden

| Field name | Type | Omschrijving |
|------------|------|-------------|
| Id | String | Unieke identificatie |
| TenantId | String | Identificatie van de tenant/klant |
| DocumentId | Int32 | Identificatienummer van het document |
| DocumentVersionId | Int32 | Identiticatienummer van versie van het document |
| DocumentNodeId | Int64 | Identificatienummer van de node in de documentversie |
| QuestId | String | Quest identificatie van document of document node |
| QuestIdParts | StringCollection | Onderdelen van de quest-identificatie |
| QuestIdPrefix | String | Eerste deel (voor eerste /) van de quest-identificatie |
| QuestIdPostfix | String | Laatste deel (na laatste /) van de quest-identificatie |
| DocumentQuestId | String | Quest identificatie van document waar node onderdeel van is |
| DocumentQuestIdParts | StringCollection | Onderdelen van de document-quest identificatie |
| IsDocument | Boolean | Geeft aan of het een document betreft (true) of een node binnen een documentversie (false) |
| Version | Int32 | Versienummer |
| Current | Boolean | Documentversie is huidige versie |
| Archive | Boolean | Documentversie is gearchiveerd |
| Status | String | Status van documentversie |
| Online | Boolean | Documentversie is online beschikbaar |
| Valid | Boolean | Documentversie is geldig |
| Date | DateTimeOffset | Datum van de documentversie |
| UntilDate | DateTimeOffset | Einddatum van de geldigheid van de documentversie |
| Modified | DateTimeOffset | Datum van laatste wijziging van de documentversie |
| ModifiedBy | String | Gebruiker die de laatste wijziging heeft gemaakt |
| Created | DateTimeOffset | Aanmaakdatum van de documentversie |
| CreatedBy | String | Gebruiker die de documentversie heeft aangemaakt |
| ImporterId | String | Identificatie van de importer gebruikt voor het importeren van deze documentversie |
| OriginId | String | Identificatie van de oorsprong van deze documentversie (bijvoorbeeld Knowmax Trinidad) |
| ContentType | String | Type van de inhoud |

## Voorbeelden
### Alleen onderdelen uit versie 1 van het Knowmax Quest document met identificatie `documents/abc`
Gebruik enkele quotes bij type *string*.
```
DocumentQuestId eq 'documents/abc' and Version eq 1
```

### Onderdelen met ergens in de identificatie `test` (bijvoorbeeld `documents/test/abc`)
Gebruik *any* syntax bij velden met type StringCollection.
```
DocumentQuestIdParts/any(p: contains(p, 'test'))
```

### Alleen documenten met versie datum na 1 januari 2023
```
Date gt 2023-01-01T00:00:00Z
```

# Metadata
Knowmax Quest documenten, documentversies en document nodes kunnen [metadata](/topics/metadata) bevatten. Met een **index veld definitie** is het mogelijk deze metadata op te nemen in de Microsoft Azure AI Search index. Een verzameling van **index veld definities** wordt een **index veld definitieset** genoemd. Deze index veld definitieset kan worden ingesteld in de index definitie en wordt gebruikt om de metadata van documenten in de Microsoft Azure AI Search index op te nemen.

Alle metadata die op deze manier wordt opgenomen is beschikbaar binnen de namespace **Metadata**. Bijvoorbeeld een metadata veld `Uitgever` van het type *string* is als volgt te gebruiken in een filter:
```
Metadata/Uitgever eq 'Knowmax'
```

