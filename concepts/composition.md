---
title: Decompositie en compositie
permalink: /concepts/composition
---

Afhankelijk van de gebruikte [importer](/concepts/importers) kan Knowmax Quest bij het importeren van XML de XML opknippen in logische eenheden. Dit proces noemen we decompositie. Een XML bestand dat een tekstdocument beschrijft zou bijvoorbeeld tot op artikel niveau kunnen worden opgeknipt. Door dit opknippen is het mogelijk inhoud uit een XML document op ieder gewenst niveau op te vragen.

Als we de XML van het onderdeel waarin oorspronkelijk een artikel voorkwam, opvragen via de Knowmax Quest Web API via **Api/Document/Data/mydocument/hfd1/par1-2** zou de XML er na het opknippen als volgt uit kunnen zien:

```XML
<paragraaf id="par1-2">        
  <paragraaf-kop>§ 1.2. Toepassing normen en certificatie- en inspectieschema’s</paragraaf-kop>
  <quest:DocumentNode-Placeholder id="175616" title="Artikel 1. Toepassing normen en certificatie- en 
    inspectieschema’s" xmlns:quest="https://schemas.knowmax.nl/2011/Quest" />
  <quest:DocumentNode-Placeholder id="175618" title="Artikel 2. Algemene voorwaarden"
    xmlns:quest="https://schemas.knowmax.nl/2011/Quest" />    
</paragraaf>
```

De "weggeknipte" artikelen zijn in dit geval vervangen door een zogenaamde "placeholder" dat het oorspronkelijk weggeknipte onderdeel beschrijft. Deze **DocumentNode-Placeholder** is een speciaal element binnen de XML namespace **https://schemas.knowmax.nl/2011/Quest**. Het proces om bij het opvragen van XML inhoud de eerder weggeknipte onderdelen weer toe te voegen heet **composeren**. Door aan het Web API verzoek **Api/Document/Data** de parameter **compose** toe te voegen met als waarde **true** zullen alle eerder weggeknipte onderdelen weer opgenomen worden in de XML. Het volgende verzoek **Api/Document/Data/mydocument/hfd1/par1-2?compose=true** aan de Web API zou bijvoorbeeld de volgende XML kunnen opleveren:

```XML
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
Alle eerder weggeknipte XML inhoud is weer terug. Naast de waarde **true** voor de parameters compose is het ook mogelijk een geheel getal op te geven. Dit getal beschrijft dan tot hoeveel niveau's de compositie moet worden uitgevoerd. De waarde **1** voor **compose** geeft bijvoorbeeld aan dat alleen de weggeknipte onderdelen op het eerste niveau gecomposeerd mogen worden. Weggeknipte onderdelen op diepere niveau's blijven weggeknipt.