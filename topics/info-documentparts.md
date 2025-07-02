---
title: Info over documentonderdelen
permalink: /topics/info
category: Onderwerpen
order: 12
---

Voor alle onderdelen van een [document](/topics/document-structure) is beschrijvende informatie beschikbaar. 

Informatie die mogelijk beschikbaar is voor documentonderdelen:

| Informatie | Beschrijving |
| --- | --- |
| QuestId resolutie | Informatie over hoe de opgegeven [Quest identificatie](/topics/quest-id) geïnterperteerd is. |
| Metadata | Lijst van metadata. | 
| Cover | Informatie over eventuele coverafbeelding. | 
| Collecties | Informatie over collecties waarin document(versie) voorkomt. | 
| Document alternatieven | Informatie over document alternatieven | 
| Security labels | Labels die toegang geven tot document (Knowmax Licentie Systeem). |
| Social data | Informatie of document als favoriet gemarkeerd is voor huidige gebruiker. |
| Search index | Sleutels voor documentversie of documentnode zoals gebruikt in zoekindex. |

# API voor opvragen info
***Endpoint***
```
GET /api/document/info/{id}
```

Dit endpoint wordt gebruikt voor het opvragen van informatie behorende bij een document node, resource of document alternative. Het endpoint heeft veel parameters die gebruikt worden om aan te geven welke onderdelen gevraagd worden. Het is een _best practice_ om alleen de informatie op te vragen die nodig is.

De in het path verwerkte parameter **id** is de [identificatie](/topics/quest-id) van een document, documentversie, documentnode, resource of document alternatief waarvoor informatie opgevraagd wordt.
