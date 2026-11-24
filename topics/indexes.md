---
title: 🔎 Indexes
permalink: /topics/indexes
category: Onderwerpen
order: 11
---

Een index is een datastructuur die het zoeken naar gegevens in een database of een andere gegevensopslag vergemakkelijkt. Het fungeert als een soort inhoudsopgave, waardoor het systeem snel de locatie van specifieke gegevens kan vinden zonder de hele dataset te doorzoeken. Knowmax Quest gebruikt de index om documenten efficiënt te doorzoeken, te filteren en op te halen.

# Microsoft Azure AI Search
Knowmax Quest maakt gebruik van Microsoft Azure AI Search als zoeksysteem. Daar worden de indexen in opgeslagen. Microsoft Azure AI Search is een krachtig zoeksysteem dat gebruikmaakt van geavanceerde algoritmen en machine learning-technieken om snel en nauwkeurig resultaten te leveren.

Daarnaast beschikt Microsoft Azure AI Search over een vector database, die wordt gebruikt in Knowmax Quest Intelligence oplossingen zoals [Knowmax Quest Research](/topics/research). Deze vector database maakt het mogelijk om complexe zoekopdrachten uit te voeren op basis van semantische vergelijkingen en contextuele relevantie, waardoor de zoekresultaten nog nauwkeuriger en relevanter worden voor de gebruiker.

# Indexdefinities
Een **indexdefinitie** beschrijft hoe Knowmax Quest een index in Microsoft Azure AI Search beheert. De definitie kan aan een applicatie worden gekoppeld en bepaalt onder andere of indexering actief is, welke documenten worden opgenomen, welke velddefinities worden gebruikt en of een embeddingmodel wordt toegepast. Eén indexdefinitie verwijst optioneel naar één **indexvelddefinitieset**; een set bevat de velddefinities die de metadata naar velden in de index mappen.

De configuratie is opgebouwd uit drie niveaus:

1. **Metadatadefinitie** — beschrijft de betekenis en herkomst van een metadatawaarde, bijvoorbeeld de definitie `Product/Status`. Zie [Metadata](/topics/metadata).
2. **Indexvelddefinitie** — koppelt één metadatadefinitie aan een veldnaam en een Azure AI Search-type, met opties voor onder andere meervoudige waarden, zoeken en filteren.
3. **Indexvelddefinitieset** — een benoemde, herbruikbare verzameling van indexvelddefinities. De indexdefinitie kiest welke set wordt toegepast.

De set maakt de koppeling; de metadatadefinitie zelf wordt niet aangepast. Een set kan door meerdere indexdefinities worden gebruikt. Zonder gekoppelde set bevat de index geen door deze set gedefinieerde metadata-velden.

## Voorbeeld van een metadata-mapping

Stel dat documenten metadata bevatten volgens de metadatadefinitie `Product/Status`. In de set `Productdocumenten` staat hiervoor een indexvelddefinitie:

| Instelling | Waarde in het voorbeeld |
|---|---|
| Metadatadefinitie | Familie `Product`, label `Status` |
| Naam van indexveld | `status` |
| Type | `Edm.String` |
| Meerdere waarden (`IsCollection`) | Aan |
| Filterbaar | Aan |
| Doorzoekbaar | Uit |

De index krijgt hiervoor een veld in het complexe veld `Metadata`, met de veldnaam `Metadata/status`. Een documentwaarde als `Gepubliceerd` wordt daarmee beschikbaar als metadata in Azure AI Search. De veldnaam is de zoekindexnaam; de metadatadefinitie blijft de bron van de waarde.

## Indexvelddefinitie instellen

Een indexvelddefinitie heeft de volgende onderdelen:

| Eigenschap | Betekenis en aandachtspunten |
|---|---|
| Metadatadefinitie | De bronmetadata. Deze moet al bestaan; een indexvelddefinitie verwijst ernaar via de definitie-ID. De combinatie van familielabel en label identificeert de definitie voor mensen en bij import. |
| Naam (`Name`) | Naam van het veld binnen `Metadata`. Maximaal 60 tekens; begint met een letter of cijfer en bevat verder alleen letters, cijfers en underscores. De naam moet binnen de set uniek zijn en mag niet botsen met een gereserveerd systeemveld. |
| Type (`Type`) | De API accepteert Azure AI Search EDM-typen: `Edm.String`, `Edm.Boolean`, `Edm.DateTimeOffset`, `Edm.Double`, `Edm.Int32`, `Edm.Int64`, `Edm.GeographyPoint` en de overeenkomstige `Collection(...)`-typen. Kies voor metadata-omzetting een ondersteund scalair type; zie hieronder. |
| Meerdere waarden (`IsCollection`) | Bepaalt of de index het veld als verzameling aanmaakt en meerdere metadatawaarden als array opslaat. Gebruik voor meerdere waarden een scalair `Type` (bijvoorbeeld `Edm.String`) en zet deze optie aan. Deze instelling staat los van de metadata-scheidingstekens: die bepalen hoe de opgeslagen metadatawaarde eventueel eerst wordt gesplitst. |
| Filterbaar (`IsFilterable`) | Maakt filterexpressies op dit veld mogelijk. |
| Sorteerbaar (`IsSortable`) | Maakt sorteren op dit veld mogelijk. Verzamelingvelden kunnen niet sorteerbaar zijn. |
| Facetteerbaar (`IsFacetable`) | Maakt het veld bruikbaar voor facetten. |
| Doorzoekbaar (`IsSearchable`) | Full-text doorzoeken is alleen van toepassing op een niet-verzamelingveld van type `Edm.String`. De API valideert niet iedere combinatie van type en veldopties; de indexbouwer kan bij ongeldige combinaties waarschuwingen loggen. |
| Analyzer (`Analyser`) | Analyzer voor een doorzoekbaar stringveld. Als deze is ingevuld, wordt deze gebruikt als analyzer voor indexering én zoeken. |
| Search-/Index-analyzer | `SearchAnalyser` en `IndexAnalyser` worden gebruikt als de algemene `Analyser` leeg is én beide specifieke analyzers zijn ingevuld. Gebruik analyzer-namen die Azure AI Search ondersteunt. |
| Metadata-overerving naar nodes (`NodePropagationType`) | Bepaalt of metadata van document en documentversie ook in de indexvermelding van documentnodes wordt opgenomen. `Allways` (standaard) neemt deze mee; `Never` sluit ze uit voor nodes. Metadata die rechtstreeks op de node is vastgelegd, blijft wel beschikbaar. |

> **Let op met `IsRetrievable`:** deze eigenschap bestaat in het model en het beheerscherm, maar de huidige opbouw van het Azure-indexschema past deze waarde niet expliciet toe. Vertrouw er daarom niet op dat `false` het veld niet-opvraagbaar maakt; controleer dit gedrag voordat een integratie erop leunt.

### Omzetting van metadatawaarden

Metadatawaarden in Knowmax Quest zijn tekst. Bij het vullen van de index zet de indexer een waarde om op basis van het ingestelde EDM-type:

- Boolean: `true` of `1` wordt `true`; andere niet-lege waarden worden `false`.
- `Edm.DateTimeOffset`, `Edm.Double`, `Edm.Int32` en `Edm.Int64`: de tekst moet naar het betreffende type te parsen zijn. Waarden die leeg zijn of niet kunnen worden omgezet, worden niet aan het indexveld toegevoegd.
- `Edm.String`: de tekst blijft tekst.
- Andere toegestane typen, zoals `Edm.GeographyPoint` en `Collection(...)` als typewaarde, worden momenteel niet door de metadata-omzetter geconverteerd en leveren dus geen waarde op. Gebruik voor meervoudige metadatawaarden daarom een scalair `Type` in combinatie met `IsCollection=true`, en gebruik alleen typen waarvan de omzetting in de indexer wordt ondersteund.

De indexer splitst waarden op de eventuele `fieldMultiValueSeparators` van de metadatadefinitie (zie [meerdere metadatawaarden](/topics/metadata#meerdere-waarden-voor-metadatadefinitie)). Bij `IsCollection=true` worden de geldige waarden als verzameling opgeslagen. Bij een niet-verzamelingveld van type `Edm.String` worden meerdere verschillende waarden samengevoegd met een spatie. Bij een niet-verzamelingveld van een ander type wordt alleen de eerste geldige waarde gebruikt. De onderliggende metadatawaarde wordt hierdoor niet gewijzigd.

## Indexdefinitie configureren

Naast de velddefinities bevat een indexdefinitie onder meer:

- **Modus**: `Local` is een lokale index die door Knowmax Quest wordt beheerd; `LocalAllowsRemote` staat extern onderhoud van een lokale index toe; `Remote` duidt een extern beheerde index aan. Bij `Remote` maakt de lokale indexer het Azure-indexschema niet zelf aan.
- **Ingeschakeld / gepauzeerd**: alleen ingeschakelde en niet-gepauzeerde definities worden normaal door de indexservice verwerkt.
- **Standaard en prioriteit**: markeren de standaardindex en beïnvloeden de verwerking van indexwerk wanneer meerdere definities actief zijn.
- **Filter**: beperkt welke documenten in de index worden opgenomen. De filter ondersteunt onder meer voorwaarden op metadata, importer, Quest-ID en Quest-status; zie de beschrijving bij het veld `Filter` in de API-definitie.
- **Rebuild en rebuildschema**: `Rebuild` vraagt een volledige nieuwe indexopbouw aan; `RebuildSchedule` kan een CRON-schema bevatten.
- **Instellingen-JSON**: bevat aanvullende index- of Research-instellingen. De beheerinterface biedt hiervoor een formulier en een ruwe JSON-weergave. Gebruik geldige JSON en de instellingen die Knowmax Quest ondersteunt.
- **Embeddingmodel**: optioneel; bepaalt of de index ook een vectorrepresentatie van inhoud krijgt. Zie [Knowmax Quest Research](/topics/research).

Knowmax Quest bouwt de lokale Azure-index in de achtergrond op. De indexservice vergelijkt de structuur van de velddefinitieset met die van de index en past een gewijzigde schema-inrichting toe. Document- en metadatawijzigingen leveren daarnaast indexacties op om de **inhoud** van de index bij te werken. Schema-aanpassing en het opnieuw vullen van bestaande documenten zijn dus niet hetzelfde. Als een wijziging in een mapping bestaande indexwaarden verandert, vraag dan zo nodig een volledige rebuild aan en controleer de buildstatus. Bij een rebuild wordt een staging-index opgebouwd en na afronding actief gemaakt.

## Beheer-API

De endpoints vallen onder de autorisatiepolicy `AllowIndex`; muterende bewerkingen vereisen daarnaast `AllowModify`. De volledige API bevat ook lijstfilters en paginering. Relevante routes:

| Resource | Route | Gebruik |
|---|---|---|
| Indexdefinitie | `GET /api/indexdefinition/id/{id}` | Eén indexdefinitie ophalen. |
| Indexdefinities | `POST /api/indexdefinition/all` | Lijst ophalen; stuur optioneel een `ListRequest` in de body. |
| Indexvelddefinitieset | `GET /api/indexfielddefinitionset/id/{id}` | Eén set ophalen. |
| Indexvelddefinitieset op naam | `GET /api/indexfielddefinitionset/name?name={naam}` | Set op exacte naam ophalen. |
| Indexvelddefinitiesets | `POST /api/indexfielddefinitionset/all` | Sets als lijst ophalen. |
| Indexvelddefinitie | `GET /api/indexfielddefinition/id/{id}` | Eén velddefinitie ophalen. |
| Indexvelddefinities | `POST /api/indexfielddefinition/all` | Velddefinities als lijst ophalen. |
| Set importeren | `POST /api/indexfielddefinitionset/import` | Velddefinities importeren; overschrijven moet expliciet worden aangevraagd. |

Maak, wijzig en verwijder indexdefinities, sets en velddefinities met respectievelijk `POST`, `PUT /{id}` en `DELETE /{id}` op de bijbehorende resource-route. Een nieuwe velddefinitie moet verwijzen naar een bestaande set en metadatadefinitie. De import van een set koppelt metadatadefinities op familielabel plus label; importregels met een onbekende metadatadefinitie worden niet geïmporteerd.

## Indexschema en beschikbare velden

De index bevat naast de optionele metadata ook de vaste velden van Knowmax Quest, zoals identificaties, titels, inhoud, beveiligingslabels en statistieken. Welke optionele groepen worden toegevoegd, hangt af van de indexdefinitie. Een overzicht van belangrijke velden en filters staat bij [Knowmax Quest Index Fields](/topics/azure-ai-search-filtering).

# Toegang tot documenten
Knowmax Quest werkt met een concept van een Security Label Provider die aan ieder document labels kan toevoegen die toegang tot het document bepalen. Voor een identiteit in Knowmax Quest kan worden bepaald tot welke labels deze identiteit toegang heeft zodat op basis van deze labels filtering kan worden toegepast. Het Knowmax Licentiesysteem is op dit moment de exclusieve Security Label Provider voor Knowmax Quest. 

# Microsoft Azure AI Search binnen een applicatie
Voor rechtstreeks gebruik van een door Knowmax Quest gebouwde index geeft Knowmax een API-key uit waarmee een applicatie Microsoft Azure AI Search kan aanroepen. Bij gebruik vanuit een browser moeten ook de CORS-instellingen van de indexdefinitie kloppen. De actieve indexgegevens zijn opvraagbaar via `GET /api/index/azuresearchindex`.

Meer informatie over Microsoft Azure AI Search: [Microsoft Azure AI Search Documentation](https://learn.microsoft.com/en-us/azure/search/)

Meer informatie over OData filtering in Microsoft Azure AI Search: [OData Filtering in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-query-odata-filter)

Meer informatie over de beschikbare velden in een door Knowmax Quest gebouwde Microsoft Azure AI Search index: [Knowmax Quest Index Fields](/topics/azure-ai-search-filtering)

# CORS
Bij rechtstreeks gebruik van de Microsoft Azure AI Search API vanuit een browser, is het noodzakelijk om CORS (Cross-Origin Resource Sharing) in te stellen. Dit zorgt ervoor dat de browser verzoeken naar de API toestaat vanuit verschillende domeinen. De CORS-instellingen worden vastgelegd in de index definitie en Knowmax Quest zal deze toepassen op de Microsoft Azure AI Search index.

# Configuratie door Knowmax
De configuratie van een index definitie wordt in de meeste gevallen in overleg door Knowmax gemaakt. Dit zorgt ervoor dat de index optimaal is afgestemd op de specifieke behoeften van de organisatie en de gebruikers. Knowmax werkt samen met klanten om de juiste instellingen te bepalen, zodat de zoekfunctionaliteit in Knowmax Quest effectief en efficiënt is.

# Knowmax Quest Research
[Knowmax Quest Research](/topics/research) maakt gebruik van een Microsoft Azure AI Search index om via 1 of meerdere zoekopdrachten resultaten te krijgen die gebruikt worden om uiteindelijk met AI een antwoord op een vraag van een gebruiker te genereren. Voor het gebruikt van Knowmax Quest Research is het noodzakelijk dat er een index is met een gevectoriseerde weergave van de documenten.