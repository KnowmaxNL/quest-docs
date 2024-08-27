---
title: Collecties
permalink: /concepts/collections
---

Een collectie beschrijft een verzameling van [documenten](/concepts/document-structure) binnen Knowmax Quest. Collecties kunnen worden gebruikt om documenten te groeperen en te ordenen. Een collectie kan bijvoorbeeld een verzameling van documenten zijn die een bepaald onderwerp behandelen of een verzameling van documenten die door een bepaalde auteur zijn geschreven. Zie een collectie als een handmatig aangemaakte verzameling van documenten. 

# Hiërarchie
Onderdelen binnen een collectie kunnen in een hiërarchie geplaatst worden. Ieder onderdeel in de collectie heet een collectie node. Een collectie node kan een titel hebben en kan optioneel naar een [document](/concepts/document-structure) of [documentversie](/concepts/document-structure) verwijzen. Zonder verwijzing naar een document of documentversie is de collectie node enkel een structuuronderdeel waaronder weer andere collectie nodes kunnen voorkomen.

# Verwijzing naar een document of documentversie
Als een collectie node naar een document of documentversie verwijst, wordt de [Quest identificatie](/quest-id) van het document opgenomen. Een eventuele documentversie wordt in een apart veld aangegeven. Als geen documentversie wordt opgegeven, wordt de huidige actieve versie van het document gebruikt.