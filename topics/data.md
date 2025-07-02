---
title: Data
permalink: /topics/data
category: Onderwerpen
order: 8
---

De [documentnodes](/topics/document-structure) van documentversies bevatten de inhoudelijke data van een document.

Afhankelijk van het soort document, kunnen documentversies ook resources en document alternatieven bevatten. Resources kunnen bijvoorbeeld afbeeldingen zijn waarnaar vanuit het document verwezen wordt. Een document alternatief is een alternatieve versie van een document, bijvoorbeeld een PDF uitvoering van een XML document.

Resources en document alternatives zijn altijd onlosmakelijk en exclusief verbonden met een documentversie. Ze zijn ontstaan tijdens het [importeren](/concepts/importers) van een documentversie.

# API voor opvragen data
***Endpoint***
```
GET /api/document/data/{id}
```

Dit endpoint wordt gebruikt voor het opvragen van alle data behorende bij een document node, resource of document alternative.

De in het path verwerkte parameter **id** is de [identificatie](/concepts/quest-id) van de documentnode, resource of document alternative.

## Integratie Knowmax Link Manager
Als Knowmax Quest geconfigureerd is om samen te werken met de Knowmax Link Manager, kunnen Knowmax Link Manager projectielinks direct in het resultaat verwerkt worden. Dit werkt alleen als de uiteindelijke uitvoer van het resultaat een HTML document is.

## Preview
Met de parameter **preview** kan het aantal woorden voor een preview ingesteld worden. De preview is beschikbaar voor anonieme gebruikers. Het maximaal aantal woorden voor een preview is 100. Een preview kan alleen gemaakt worden voor documenten die een HTML uitvoer hebben.

## Transformatie
Met de parameter **transform** kan de uitvoer van de data getransformeerd worden. De volgende soorten transformaties zijn beschikbaar:

| Naam | Omschrijving | 
| --- | --- |
| XML naar JSON | Transformeert XML data naar JSON |
| XSLT | Transformeert XML data met een XSLT stylesheet |

### XML naar JSON
De XML naar JSON transformatie werkt als een transformatie actie en wordt aangegeven door de parameter **transform** de waarde **{xmltojson}** te geven. Volgens een vastgestelde conventie wordt de XML omgezet naar JSON. De exacte uitvoer is altijd afhangend van de XML structuur.

### XSLT
#### Definitie van een transformatie
Voor een XSLT transformatie moet in Knowmax Quest een transformatie definitie aangemaakt worden. De transformatie definitie beschrijft de eigenschappen van de uit te voeren XSLT transformatie en bevat de XSLT en eventuele andere resources. Iedere transformatie heeft een label als unieke identificatie. Het label van de transformatie kan in de parameter **transform** opgegeven worden om deze transformatie toe te passen.

#### Automatische selectie van een transformatie
Het is ook mogelijk transformatietypen te definiëren. Per transformatie definitie kunnen met ***Autoselect JSON*** 1 of meerdere transformatietypen gedefinieerd worden. Met regels vastgelegd voor welk type document een transformatie geschikt is. Door de parameter **transform** het transformatietype op te geven, wordt automatisch de juiste transformatie definitie geselecteerd. Een transformatietype moet altijd tussen blokhaken **[transformatietype]** geplaatst worden.

***Autoselect JSON***
```json
{
  "fancy": [{
      "ImporterId": "BasisWettenBestandToestand"
    }
  ]
}
```

Deze autoselect JSON beschrijft het transformtype ***fancy***. Deze transformatie zal gebruikt worden als tijdens het importeren van de documentversie de **importer** met identificatie ***BasisWettenBestandToestand*** gebruikt is.

Naast **ImporterId** is het ook mogelijk om te selecteren op **QuestId**, **QuestVersion** en het voorkomen of hebben van een betaalde **metadata** waarde via **Meta**.

Onderstaande autoselect JSON beschrijft het transformatie type ***platform***. Deze transformatie zal gebruikt worden de import ***QuestIni*** is gebruikt en als er geen metadata waarde is met label ***DublinCore.type*** en waarde ***ABC***.
```json
{
  "platform": [{
      "ImporterId": "QuestIni",
       "Meta": [{
        "Label": "DublinCore.type",
        "Value": "ABC",
        "Negate": true
      }]
    }
  ]
}
```