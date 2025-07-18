---
title: 💬 Knowmax Quest Intelligence Conversations
permalink: /topics/intelligence-conversations
category: Onderwerpen
order: 15
---

De module Knowmax Quest Intelligence Conversations legt gesprekken vast die gebruikers voeren met Knowmax Quest Intelligence oplossingen zoals [Knowmax Quest Document Insight](/topics/document-insight) en [Knowmax Quest Research](/topics/research). Een gesprek of conversatie is een verzameling van interacties tussen een gebruiker en een Knowmax Quest Intelligence oplossing. Deze module maakt het mogelijk om de interacties met deze oplossingen te volgen, te analyseren en te verbeteren.

# Conversatie identificatie
Elke conversatie heeft een unieke identificatie die wordt gebruikt om de interacties te volgen. Deze identificatie wordt automatisch gegenereerd wanneer een nieuwe conversatie wordt gestart. Door deze *conversatieId* in opvolgende verzoeken te gebruiken, kunnen gebruikers de context van hun interacties behouden en de voortgang van hun gesprekken volgen.

# Conversatie limiet
Per Intelligence Model is vastgelegd hoeveel paren van vraag en antwoord er maximaal in een conversatie kunnen worden opgeslagen. Na het bereiken van deze limiet wordt automatisch een nieuwe conversatie gestart. In het resultaat beschrijven de velden *conversationDepth* en *maxConversationDepth* de huidige diepte van de conversatie en de maximale diepte die is toegestaan voor het specifieke model.

Deze limiet is ingesteld om de prestaties van de AI-modellen te optimaliseren en ervoor te zorgen dat de conversaties efficiënt blijven. Bij iedere opvolgende vraag moeten ook alle voorgaande vragen en antwoorden worden meegegeven aan de AI en dit zal extra capaciteit en dus tokens kosten.

# Wat wordt opgeslagen?
Alleen de door gebruikers gestelde vragen en de antwoorden die door Knowmax Quest Document Insight of Knowmax Quest Research worden gegeven, worden opgeslagen. Eventuele systeem meldingen om de AI te sturen worden niet opgeslagen en moeten bij iedere vervolgvraag opnieuw worden meegegeven.

# Beoordeling van antwoorden
Gebruikers kunnen gesprekken beoordelen door een rating toe te voegen aan de antwoorden die ze ontvangen van Knowmax Quest Document Insight of Knowmax Quest Research. Deze ratings helpen bij het verbeteren van de kwaliteit van de antwoorden en het optimaliseren van de prestaties van de AI-modellen die worden gebruikt in deze oplossingen.

Ondersteunde waarden voor een rating zijn 1 voor een bruikbaar antwoord en 0 voor een niet bruikaar antwooord.

Het endpoint om de rating van een antwoord te geven is:

```
POST /api/intelligence/rate
```

Naast *conversationId* moet ook *conversationMessageId* worden meegegeven. Dit is de unieke numerieke identificatie van het antwoord dat beoordeeld wordt. Deze is met het gegeven antwoord ontvangen.