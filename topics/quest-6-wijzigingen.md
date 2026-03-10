---
title: 🚀 Knowmax Quest 6 wijzigingen
permalink: /topics/quest-6-wijzigingen
category: Onderwerpen
order: 26
---

Dit onderwerp beschrijft de belangrijkste wijzigingen in Knowmax Quest 6 ten opzichte van eerdere versies. De nadruk ligt op de vernieuwde mogelijkheden in [Knowmax Quest Research](/topics/research), [Knowmax Quest Document Insight](/topics/document-insight), de beheeromgeving, PDF-uitvoer en sterk verbeterde tekstextractie.

# Belangrijkste thema's in versie 6

## Knowmax Quest Research
- Compleet nieuwe pipeline voor Knowmax Quest Research.
- Reasoning effort instelling: **Minimal**, **Low** en **Medium**.
- **Low** is vergelijkbaar met de basisinstelling in Quest 5.
- **Medium** ondersteunt agentic research in Quest 6.
- Verbeterde query intent detection.
- Query planning met:
  - LLM powered query rewriting.
  - Query time Hypothetical Answer Prediction (HyDE).
- Query execution met:
  - Parallel query execution.
  - Hybrid query (vector + keyword).
  - Verbeterde vector query resultaten met extractive captions.
  - Advanced result ranking (BM25, Reciprocal Rank Fusion, Semantic).
- Improved LLM answer synthesis.
- Verbeterde citation in Knowmax Quest Research.

## Extra tools in Knowmax Quest Research
- Extra zoekopdrachten op basis van het in de eerste fase vastgestelde antwoord.
- Lookup van verwijzingen naar documenten.
- Versie-informatie over een bepaald document.
- Metadata van een bepaald document.
- Inhoudsopgave van een bepaald document.
- Datum/tijd tools.

## Knowmax Quest Document Insight
- Knowmax Quest Document Insight profiteert direct van de verbeteringen in de gedeelde **Knowmax Intelligence** laag, waaronder nieuwe modelondersteuning en rijkere contextvastlegging in intelligentiegesprekken.

## Knowmax Intelligence
Deze verbeteringen gelden voor de gedeelde intelligentielaag waar zowel Knowmax Quest Research als Knowmax Quest Document Insight van profiteren.

- Ondersteuning voor nieuwe OpenAI modellen voor zowel Research als Document Insight.
- Experimentele ondersteuning voor modellen van Anthropic voor zowel Research als Document Insight.

### Verbeteringen in intelligentiegesprekken
- Mogelijkheid om automatisch een titel te laten genereren voor een gesprek.
- Mogelijkheid om bij een rating van een antwoord optioneel tekstuele feedback vast te leggen.
- Vastleggen van context bij antwoorden en gesprekken:
  - Het gebruikte LLM model.
  - Het onderdeel waar de vraag op slaat, bijvoorbeeld in de vorm van een Quest ID of een filter.
- Beter inzicht in welk model is gebruikt voor welk antwoord.

## Tekstextractie en documentverwerking
- Ondersteuning voor markdown text extraction met behoud van documentstructuur voor verbeterde LLM verwerking.
- Text extraction interceptors voor verbeterde tekstuele LLM weergave van content.
- Verbeterde MathML ondersteuning door herschrijven naar LaTeX en tekst.
- Custom interceptors voor specifieke inhoud.
- Verbeterde chunking van grote hoeveelheden tekst.
- Verbeterde text extractie uit PDF documenten ten behoeve van indexering.

## Beheeromgeving
- Verbeterde navigatie in de beheeromgeving.
- Vernieuwde vormgeving van de beheeromgeving.
- Powersearch in de beheeromgeving om breed te zoeken.
- Verbeterde weergave in de beheeromgeving op kleine schermen.
- Verbeterde navigatie bij tabbladen voor documenten en documentversies.
- Mogelijkheid om documentversies te filteren op aantal importlog meldingen.
- Mogelijkheid om de definitie van een intelligence model te clonen.

## PDF uitvoer module
- Verbeterde PDF-uitvoer als separate module.
- Deze module is beschikbaar als optionele add-on voor Knowmax Quest.

## Platform, prestaties en betrouwbaarheid
- Upgrade van JSON serialization mapper (AutoMapper naar Mapster) met performance verbetering.
- Performance verbeteringen in XML composer functionaliteit.
- Performance verbetering van de database door toevoegen van extra indexes.
- Verbeterde OpenAPI documentatie.
- Verbeterde downloadmogelijkheid van documentdata met short lived download token via bearer token.
- Verbeteringen om problemen bij gelijktijdige publicatie te voorkomen.

# Samenvatting
Knowmax Quest 6 introduceert een grote vernieuwing in AI-gestuurde informatieontsluiting, met een volledig vernieuwde Research pipeline, sterk verbeterde tekstextractie (inclusief markdown met structuurbehoud), een modernere beheeromgeving en betere prestaties in de gehele keten.