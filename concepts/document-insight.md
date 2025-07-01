---
title: Knowmax Quest Document Insight
permalink: /concepts/document-insight
---

Knowmax Quest Document Insight ondersteunt de gebruiker tijdens het lezen van een document door op verschillende manieren inzicht te geven in de tekst van een specifiek documentonderdeel uit Knowmax Quest. De gebruiker kan vragen stellen over de tekst en krijgt via [artificiële intelligentie](/concepts/intelligencemodels) (AI) gegenereerde antwoorden. 

Het verschil met [Knowmax Quest Research](/concepts/research) is dat Knowmax Quest Document Insight de beschikking heeft over de gehele inhoud van een documentonderdeel en daardoor in staat is om zeer specifieke en gedetailleerde antwoorden te geven op vragen die betrekking hebben op de inhoud van dat specifieke document. Dit maakt het mogelijk om diepgaande analyses en inzichten te verkrijgen die anders misschien niet beschikbaar zouden zijn.

# Samenwerking met Knowmax Quest Research
Knowmax Quest Document Insight kan gebruikt worden om over ieder onderdeel van het document vragen te stellen. Het is afhankelijk van het gebruikte intelligentiemodel hoeveel data er gebruikt kan worden om een vraag te stellen. Als het documentonderdeel te groot is, kan het zijn dat het intelligentiemodel geen antwoord kan geven. 

Als [Knowmax Quest Research](/concepts/research) ook beschikbaar is, zal in gevallen dat het documentonderdeel te groot is automatisch omgeschakeld worden naar Knowmax Quest Research. Er zal dan een poging gedaan worden om de vraag te beantwoorden op basis van de zoekresultaten van Knowmax Quest Research. Dit zorgt ervoor dat gebruikers altijd een antwoord krijgen, zelfs als het specifieke documentonderdeel te groot is voor Knowmax Quest Document Insight.

# Context
Na een antwoord van Knowmax Quest Document Insight, kan de gebruiker vervolgvragen stellen om het gekregen antwoord te verfijnen. Op deze manier kan de gebruiker een gesprek aangaan met Knowmax Quest Research. Voor het vastleggen van een gesprek wordt gebruik gemaakt van de [Knowmax Quest Intelligence Conversations](/concepts/intelligence-conversatios) module. Deze module legt het gesprek vast en maakt het mogelijk om later terug te kijken naar de interactie met Knowmax Quest Research.

# Endpoint
Het endpoint voor Knowmax Quest Document Insight is:

```
POST /api/intelligence/document-insight
```