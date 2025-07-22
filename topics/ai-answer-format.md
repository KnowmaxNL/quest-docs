---
title: 🧠 Antwoord van intelligence model
permalink: /topics/ai-answer-format
category: Onderwerpen
order: 17
---

## 📄 Outputformaat van een een intelligentiemodel

De antwoorden die door een [intelligentiemodel](/topics/intelligencemodels) worden gegenereerd, worden meestal geretourneerd in **Markdown-indeling**. Dit maakt het eenvoudig om de output op een gestructureerde en visueel aantrekkelijke manier weer te geven.

### Vaak voorkomende Markdown-elementen

- **Koppen**: `#`, `##`, `###` voor hiërarchische titels
- **Vetgedrukte tekst**: `**tekst**`
- *Cursieve tekst*: `*tekst*`
- **Lijsten**:
  - Ongeordend: `- item`
  - Geordend: `1. item`
- **Code**:
  - Inline: `` `code` ``
  - Blokken: 
    ````
    ```taal
    codeblok
    ```
    ````
- **Links**: `https://voorbeeld.com`

---

### Verwijzingen zoals `[doc1]`, `[doc2]`

Wanneer het intelligentiemodel informatie gebruikt uit specifieke bronnen (zoals Knowmax Quest documenten), worden er automatisch verwijzingen toegevoegd in de vorm van `[doc1]`, `[doc2]`, enzovoort. Deze verwijzingen corresponderen met een aparte lijst van bronnen die je als `citations` ontvangt in de API-respons, bijvoorbeeld:

```json
"citations": [
  {
    "bookTitle": "Handleiding",
    "title": "Handleiding hoofdstuk 1",
    "contents": "hier een fragment uit hoofdstuk 1",
    "questId": "handleiding/1"
  },
  {
    "bookTitle": "Handleiding",
    "title": "Handleiding hoofdstuk 2",
    "contents": "hier een fragment uit hoofdstuk 2",
    "questId": "handleiding/2"
  }
]
```

Dit soort verwijzingen zie je vaak terug in antwoorden die afkomstig zijn van [Knowmax Quest Research](/topics/research).

### Formules en wiskundige notaties
Voor antwoorden die formules of wiskundige notaties bevatten, wordt meestal LaTeX gebruikt. Dit maakt het mogelijk om complexe wiskundige concepten op een duidelijke en leesbare manier weer te geven. Een voorbeeld van een formule in LaTeX is:

```latex
E = mc^2
```

De LaTeX-notatie wordt niet automatisch gerenderd in alle omgevingen. Zorg ervoor dat je frontend Markdown ondersteunt met LaTeX-rendering (bijv. via https://katex.org/ of https://www.mathjax.org/).
In sommige gevallen kan de AI ook codeblokken gebruiken voor wiskundige berekeningen, vooral als het Python of een andere programmeertaal betreft.