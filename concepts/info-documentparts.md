---
title: Info over documentonderdelen
permalink: /concepts/info
---

Voor alle onderdelen van een [document](/topics/document-structure) is beschrijvende informatie beschikbaar. 

Informatie die mogelijk beschikbaar is voor documentonderdelen:

| Informatie | Beschrijving |
| --- | --- |
| QuestId resolutie | Informatie over hoe de opgegeven [Quest identificatie](/concepts/quest-id) geïnterperteerd is. |
| Metadata | Lijst van metadata. | 
| Cover | Informatie over eventuele coverafbeelding. | 
| Collecties | Informatie over collecties waarin document(versie) voorkomt. | 
| Document alternatieven | Informatie over document alternatieven | 
| Security labels | Labels die toegang geven tot document (Knowmax Licentie Systeem). |
| Social data | Informatie of document eventueel als favoriet gemarkeerd is voor huidige gebruiker. |
| Search index | Sleutels voor documentversie of documentnode zoals gebruikt in eventuele zoekindex. |

# API voor opvragen info
***Endpoint***
```
GET /api/document/info/{id}
```

Dit endpoint wordt gebruikt voor het opvragen van alle data behorende bij een document node, resource of document alternative.

De in het path verwerkte parameter **id** is de [identificatie](/concepts/quest-id) van de documentnode, resource of document alternative.