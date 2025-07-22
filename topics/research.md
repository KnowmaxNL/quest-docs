---
title: 🧠 Knowmax Quest Research
permalink: /topics/research
category: Onderwerpen
order: 17
---

Knowmax Quest Research stelt gebruikers in staat om in natuurlijke taal vragen te stellen over alle documenten die zijn opgenomen in een Microsoft Azure AI Search [index](/topics/indexes) inclusief een gevectoriseerde weergave van de inhoud van de documenten. Antwoorden worden door [artificiële intelligentie](/topics/intelligencemodels) (AI) gegenereerd. Knowmax Quest Research biedt een geavanceerd alternatief voor zoeken. 

Het verschil met [Knowmax Quest Document Insight](/topics/document-insight) is dat Knowmax Quest Research niet alleen antwoorden geeft op vragen over de inhoud van een specifiek document, maar ook over de inhoud van meerdere documenten die zijn opgenomen in de Microsoft Azure AI Search index. Dit maakt het mogelijk om bredere en meer complexe vragen te stellen en antwoorden te krijgen die zijn gebaseerd op een breder scala aan informatie. Nadeel van antwoorden op basis van zoekresultaten is dat mogelijk niet alle relevante informatie wordt meegenomen in het antwoord. Dit kan gebeuren als de zoekopdracht niet specifiek genoeg is of als er veel documenten zijn over een soortgelijk onderwerp.

# Context
Na een antwoord van Knowmax Quest Research, kan de gebruiker vervolgvragen stellen om het gekregen antwoord te verfijnen. Op deze manier kan de gebruiker een gesprek aangaan met Knowmax Quest Research. Voor het vastleggen van een gesprek wordt gebruik gemaakt van de [Knowmax Quest Intelligence Conversations](/topics/intelligence-conversations) module. Deze module legt het gesprek vast en maakt het mogelijk om later terug te kijken naar de interactie met Knowmax Quest Research.

# Filtering
Dankzij het gebruik van [Microsoft Azure AI Search](/topics/indexes), is het mogelijk de voor Knowmax Quest Research te gebruiken zoekresultaten te filteren op basis van metadata die aan de documenten zijn gekoppeld. Daarmee is het mogelijk om gerichter te zoeken en alleen de meest relevante informatie te vinden. 

# Document Intent
De kwaliteit van het antwoord van Knowmax Quest Research is sterk afhankelijk van de kwaliteit van de uitgevoerde zoekopdrachten. De resultaten van die zoekopdrachten worden ten slotte gebruikt om een aanwoord te genereren. Om de kwaliteit van de resultaten van de zoekopdracht te verbeteren, is het optioneel mogelijk door de gebruiker in de vraag genoemde documenten vast te stellen. Deze zogenaamde **document intent** kan worden gebruikt om de zoekopdracht te beperken tot 1 of meerdere specifieke documenten.

Het vaststellen van de door de gebruiker genoemde document gaat via AI. Vervolgens kan Knowmax Quest op zoek naar corresponderen documenten. Als deze gevonden zijn, wordt de uit te voeren zoekopdracht beperkt tot deze documenten. Dit kan de relevantie van de zoekresultaten verbeteren en ervoor zorgen dat het antwoord beter aansluit bij de vraag van de gebruiker.

Binnen de context van een conversatie zal Knowmax Quest Research deze document intent automatisch gebruiken voor vervolgvragen, tenzij in die vervolgvragen een nieuwe document intent wordt vastgesteld. 

# Endpoint
Het endpoint voor Knowmax Quest Research is:

```
POST /api/intelligence/research
```

Meer informatie over het [antwoord van intelligence model](/topics/ai-answer-format).