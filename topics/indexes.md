---
title: 🔎 Indexes
permalink: /topics/indexes
category: Onderwerpen
order: 11
---

Een index is een datastructuur die het zoeken naar gegevens in een database of een andere gegevensopslag vergemakkelijkt. Het fungeert als een soort inhoudsopgave, waardoor het systeem snel de locatie van specifieke gegevens kan vinden zonder de hele dataset te doorzoeken. Knowmax Quest gebruikt de index om documenten efficiënt te doorzoeken, te filteren en op te halen.

# Microsoft Azure AI Search
Knowmax Quest maakt gebruik van Microsoft Azure AI Search als zoeksysteem. Daar worden de indexen in opgeslagen. Microsoft Azure AI Search is een krachtig zoeksysteem dat gebruikmaakt van geavanceerde algoritmen en machine learning-technieken om snel en nauwkeurig resultaten te leveren.

Daarnaast beschikt Microsoft Azure AI Search over een vector database, die wordt gebruikt in Knowmax Quest Intelligence oplossingen zoals [Knowmax Quest Research](/concepts/research). Deze vector database maakt het mogelijk om complexe zoekopdrachten uit te voeren op basis van semantische vergelijkingen en contextuele relevantie, waardoor de zoekresultaten nog nauwkeuriger en relevanter worden voor de gebruiker.

# Indexdefinities
Een index in Knowmax Quest wordt gedefinieerd door een Indexdefinitie. Deze beschrijft de eigenschappen van de index in Microsoft Azure AI Search. Via een index veld definitieset kunnen er instellingen gemaakt worden om bepaalde metadata van documenten in Knowmax Quest vast te leggen in de Microsoft Azure AI Search index. Optioneel kan een embedding intelligentie model worden ingesteld om de inhoud gevectoriseerd op te slaan in de Microsoft Azure AI Search index.

Knowmax Quest bouwt op basis van de indexdefinitie een Microsoft Azure AI Search index. Bij het maken van wijzigingen aan documenten of metadata van documenten, wordt de index automatisch bijgewerkt.

# Toegang tot documenten
Knowmax Quest werkt met een concept van een Security Label Provider die aan ieder document labels kan toevoegen die toegang tot het document bepalen. Voor een identiteit in Knowmax Quest kan worden bepaald tot welke labels deze identiteit toegang heeft zodat op basis van deze labels filtering kan worden toegepast. Het Knowmax Licentiesysteem is op dit moment de exclusieve Security Label Provider voor Knowmax Quest. 

# Microsoft Azure AI Search binnen een applicatie
Voor het gebruik van een door Knowmax Quest gebouwde index binnen Microsoft Azure AI Search, geeft Knowmax een API key uit zodat ontwikkelaars direct de API van Microsoft Azure AI Search kan aanroepen en gebruiken in hun applicaties. Dit stelt ontwikkelaars in staat om de krachtige zoekfunctionaliteit van Microsoft Azure AI Search te integreren in hun eigen toepassingen en workflows.

Meer informatie over Microsoft Azure AI Search: [Microsoft Azure AI Search Documentation](https://learn.microsoft.com/en-us/azure/search/)

# CORS
Bij rechtstreeks gebruik van de Microsoft Azure AI Search API vanuit een browser, is het noodzakelijk om CORS (Cross-Origin Resource Sharing) in te stellen. Dit zorgt ervoor dat de browser verzoeken naar de API toestaat vanuit verschillende domeinen. De CORS-instellingen worden vastgelegd in de index definitie en Knowmax Quest zal deze toepassen op de Microsoft Azure AI Search index.

# Configuratie door Knowmax
De configuratie van een index definitie wordt in de meeste gevallen in overleg door Knowmax gemaakt. Dit zorgt ervoor dat de index optimaal is afgestemd op de specifieke behoeften van de organisatie en de gebruikers. Knowmax werkt samen met klanten om de juiste instellingen te bepalen, zodat de zoekfunctionaliteit in Knowmax Quest effectief en efficiënt is.

# Knowmax Quest Research
[Knowmax Quest Research](/concepts/research) maakt gebruik van een Microsoft Azure AI Search index om via 1 of meerdere zoekopdrachten resultaten te krijgen die gebruikt worden om uiteindelijk met AI een antwoord op een vraag van een gebruiker te genereren. Voor het gebruikt van Knowmax Quest Research is het noodzakelijk dat er een index is met een gevectoriseerde weergave van de documenten.