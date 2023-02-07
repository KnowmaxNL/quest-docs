---
title: Rechten
permalink: /concepts/rights
---

Het bij [authenticatie](/concepts/authentication) verkregen bearer token beschrijft wie de gebruiker is en wat de rechten van de gebruiker zijn. Deze rechten worden uitgedrukt in claims. Claims zijn stukjes informatie die in het bearer token zijn opgenomen. 

Afhankelijk van de toegekende rechten is het gebruik van bepaalde functionaliteit van de API wel of niet toegestaan. Welke rechten beschikbaar zijn, is afhankelijk van de toepassing en de beschikbare functionaliteit voor het desbetreffende Knowmax Quest systeem. Rechten worden ingesteld door Knowmax bij uitgifte van een Knowmax Magma API sleutel.

# Beschikbare rechten

| Naam | Beschrijving |
| --- | --- |
| AllowUse | Staat gebruik van basisfunctionaliteit toe. |
| AllowData | Staat het opvragen van data toe. |
| AllowModify | Staat het maken van wijzigingen in data toe. |
| AllowIndex | Staat het opvragen en beheren van indexen toe. |
| AllowManagement | Staat toegang tot de beheerinterface toe. |
| AllowAuthenticate | Staat authenticatie namens andere gebruikers toe. |
| AllowStatistics | Staat het gebruik van Knowmax Quest Statistics toe. |

# Afscherming data
Het recht **AllowData** is nodig om data op te kunnen vragen. Mogelijk gelden er voor de Knowmax Magma API sleutel ook nog andere beperkingen die bepalen welke data op te vragen is. Het gaat dan om een berperking waardoor alleen de data van specifieke [Quest documenten](/concepts/quest-id) op te vragen is.

## Afscherming op collectie
Knowmax kan instellingen maken die zorgen dat de Knowmax Magma API sleutel alleen toegang heeft tot documenten opgenomen in een bepaalde collectie.

## Afscherming volgens licentie
Knowmax kan instellingen maken die zorgen dat de Knowmax Magma API sleutel alleen toegang heeft tot documenten waar toegang op gegeven wordt via een bepaalde licentie.

# Welke rechten heeft mijn bearer token?
Gebruik het endpoint ```/api/authentication/rights``` om te achterhalen welke rechten het verkregen bearer token heeft. Vergeet niet het bij [authenticatie](/concepts/authentication) verkregen bearer token mee te geven in de header.

***Endpoint***
```
POST /api/authentication/rights
```

***Response body ```application/json```***
```json
{
    "allowData": true,
    "allowIndex": false,
    "allowModify": false,
    "allowStatistics": false,
    "allowManagement": false
}
```