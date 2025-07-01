---
title: Intelligentie modellen
permalink: /concepts/intelligencemodels
---

Er kunnen verschillende Artificiële Intelligentie (AI) modellen op Knowmax Quest aangesloten worden. Het gaat om zogenaamde Large Language Models (LLM). Alle populaire modellen, zoals die van OpenAI, Ollama en Microsoft, kunnen gebruikt worden. Knowmax Quest is voorbereid om ook toekomstige modellen laagdrempelig te ondersteunen. 

# Configuratie van AI modellen
De configuratie van AI modellen wordt gedaan in de Knowmax Quest beheeromgeving. Per AI model wordt een Intelligentiemodel definitie aangemaakt. In de meeste gevallen zal de configuratie in overleg met Knowmax worden gemaakt.

# Taak type
Per Intelligentiemodel kan een taak type worden ingesteld. Dit taak type bepaalt de functionaliteit van het AI model. De volgende taak types zijn beschikbaar:
* **Chat completion**: Wordt gebruikt voor chat toepassingen, waarbij het AI model antwoorden genereert op basis van de input van de gebruiker. Deze worden direct gebruikt door [Knowmax Quest Research](/concepts/research) en [Knowmax Quest Document Insight](/concepts/document-insight).
* **Embedding**: Dit taak type wordt gebruikt om tekst te converteren naar vectoren, die vervolgens kunnen worden gebruikt voor semantische zoekopdrachten of vergelijkingen. Deze vectoren worden opgeslagen in de Microsoft Azure AI Search [index](/concepts/indexes).