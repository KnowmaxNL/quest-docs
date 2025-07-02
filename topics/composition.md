---
title: Decompositie en compositie
permalink: /topics/composition
category: Onderwerpen
order: 9
---

Afhankelijk van de gebruikte [importer](/concepts/importers) kan Knowmax Quest documentversies bij het importeren opknippen in logische eenheden. Dit proces noemen we decompositie. Een XML bestand dat een tekstdocument beschrijft met hoofdstukken en artikelen, zou bijvoorbeeld tot op artikelniveau kunnen worden opgeknipt. Door dit opknippen is het mogelijk inhoud uit een XML document op ieder gewenst niveau op te vragen. Ieder opgeknipt onderdeel krijgt een eigen identificatie en is als een [document node](/topics/document-structure) beschikbaar binnen de documentversie.

Als we de XML van het onderdeel waarin oorspronkelijk een artikel voorkwam, opvragen via de Knowmax Quest API via ```GET api/document/data/mydocument/hfd1/par1-2``` zou de XML er na het opknippen als volgt uit kunnen zien:

```XML
<paragraaf id="par1-2">        
  <paragraaf-kop>§ 1.2. Toepassing normen en certificatie- en inspectieschema’s</paragraaf-kop>
  <quest:DocumentNode-Placeholder id="175616" title="Artikel 1. Toepassing normen en certificatie- en 
    inspectieschema’s" xmlns:quest="https://schemas.knowmax.nl/2011/Quest" />
  <quest:DocumentNode-Placeholder id="175618" title="Artikel 2. Algemene voorwaarden"
    xmlns:quest="http://schemas.knowmax.nl/2011/Quest" />    
</paragraaf>
```

De "weggeknipte" artikelen zijn in dit geval vervangen door een zogenaamde "placeholder" dat het oorspronkelijk weggeknipte onderdeel beschrijft. Deze **DocumentNode-Placeholder** is een speciaal element binnen de XML namespace **http://schemas.knowmax.nl/2011/Quest**. Het proces om bij het opvragen van XML de eerder weggeknipte onderdelen weer toe te voegen, heet **composeren**. Het endpoint ```GET api/document/data``` met de parameter **compose** en waarde **true**, zal alle eerder weggeknipte onderdelen weer opnemen in de XML. Het volgende verzoek ```GET api/document/data/mydocument/hfd1/par1-2?compose=true``` aan de Knowmax Quest API zou bijvoorbeeld de volgende XML kunnen opleveren:

```xml
<paragraaf id="par1-2">        
  <paragraaf-kop>§ 1.2. Toepassing normen en certificatie- en inspectieschema’s</paragraaf-kop>
  <artikel id="art1">
    <artikel-kop>Artikel 1. Toepassing normen en certificatie- en inspectieschema’s<artikel-kop>
    <tekst>
      ...Hier de tekst voor artikel 1...
    </tekst>    
  </artikel>
  <artikel id="art2">
    <artikel-kop>Artikel 2. Algemene voorwaarden<artikel-kop>
    <tekst>
      ...Hier de tekst voor artikel 2...
    </tekst>
  </artikel>
</paragraaf>
```
Alle eerder weggeknipte XML is weer terug. Naast de waarde **true** voor de parameters compose is het ook mogelijk een geheel getal op te geven. Dit getal beschrijft dan tot hoeveel niveau's de compositie moet worden uitgevoerd. De waarde **1** voor **compose** geeft bijvoorbeeld aan dat alleen de weggeknipte onderdelen op het eerste niveau gecomposeerd mogen worden. Weggeknipte onderdelen op diepere niveau's blijven weggeknipt.

Op dit moment heeft Knowmax Quest alleen ondersteuning voor decompositie en compositie van XML documenten. Voor een PDF document is dit bijvoorbeeld niet mogelijk.