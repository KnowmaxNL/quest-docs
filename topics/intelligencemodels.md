---
title: 🧠 Intelligentie modellen
permalink: /topics/intelligencemodels
category: Onderwerpen
order: 13
---

Er kunnen verschillende Artificiële Intelligentie (AI) modellen op Knowmax Quest aangesloten worden. Het gaat om zogenaamde Large Language Models (LLM). Alle populaire modellen, zoals die van OpenAI, Ollama en Microsoft, kunnen gebruikt worden. Knowmax Quest is voorbereid om ook toekomstige modellen laagdrempelig te ondersteunen. 

# Configuratie van AI modellen
De configuratie van AI modellen wordt gedaan in de Knowmax Quest beheeromgeving. Per AI model wordt een Intelligentiemodel definitie aangemaakt. In de meeste gevallen zal de configuratie in overleg met Knowmax worden gemaakt.

# Taak type
Per Intelligentiemodel kan een taak type worden ingesteld. Dit taak type bepaalt de functionaliteit van het AI model. De volgende taak types zijn beschikbaar:
* **Chat completion**: Wordt gebruikt voor chat toepassingen, waarbij het AI model antwoorden genereert op basis van de input van de gebruiker. Deze worden direct gebruikt door [Knowmax Quest Research](/topics/research) en [Knowmax Quest Document Insight](/topics/document-insight).
* **Embedding**: Dit taak type wordt gebruikt om tekst te converteren naar vectoren, die vervolgens kunnen worden gebruikt voor semantische zoekopdrachten of vergelijkingen. Deze vectoren worden opgeslagen in de Microsoft Azure AI Search [index](/topics/indexes).

# Instellingen per model
Naast endpoint, modelidentificatie en andere algemene configuratie heeft een intelligentiemodel het veld `SettingsJson`. In de beheeromgeving kunnen de instellingen via een formulier worden aangepast, of rechtstreeks als JSON. De instellingen bepalen onder meer de gesprekslimieten, modelondersteuning, systeemberichten, bijlagen en compressie.

Een volledige beschrijving van alle instellingen, standaarden en de JSON-vorm staat in het verdiepingstopic [Instellingen intelligentiemodellen](/topics/intelligencemodelsettings).

# Intelligentie modellen voor applicatie
De keuze welk intelligentie model gebruikt wordt voor Knowmax Quest Research of Knowmax Quest Document Insight wordt gemaakt in de applicatie waarin deze functionaliteit wordt aangeboden.

Mogelijk zijn meerdere intelligentie modellen voor een bepaalde applicatie beschikbaar. Met het onderstaande endpoint kunnen de voor een bepaalde applicatie beschikbare intelligentie modellen van een bepaald type worden opgehaald. Normaal gesproken zijn dat alleen intelligentie modellen van het type "Chat completion".

```
GET /api/intelligence/models
```