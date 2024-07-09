---
title: Rechten
permalink: /concepts/rights
---

Het bij [authenticatie](/concepts/authentication) verkregen bearer token beschrijft wie de gebruiker is en wat de rechten van de gebruiker zijn. Deze rechten worden uitgedrukt in claims. Claims zijn stukjes informatie die in het bearer token zijn opgenomen. Afhankelijk van de toegekende rechten is het gebruik van bepaalde functionaliteit van de API wel of niet toegestaan.

# Beschikbare rechten

| Naam | Beschrijving |
| --- | --- |
| AllowUse | Staat gebruik van basisfunctionaliteit toe. |
| [AllowData](/concepts/rights-allowdata) | Staat het opvragen van data toe. |
| AllowModify | Staat het maken van wijzigingen in data toe. |
| AllowIndex | Staat het opvragen en beheren van indexen toe. |
| AllowManagement | Staat toegang tot de beheerinterface toe. |
| AllowAuthenticate | Staat authenticatie namens andere gebruikers toe. |
| AllowStatistics | Staat het gebruik van Knowmax Quest Statistics toe. |

# Toekennen van rechten
Rechten voor Knowmax Magma API sleutels worden bij uitgifte ingesteld door Knowmax. 

Bij [authenticatie](/concepts/authentication) via een token van het Knowmax Licentiesysteem geldt dat alleen indien het token een geclaimde plaats in de licentie beschrijft, de gebruiker het [AllowData](/concepts/rights-allowdata) recht heeft. Het is mogelijk dat op basis van de licentie ook andere rechten toegekend worden. Knowmax heeft beheer over de instellingen die beschrijven welk onderdeel uit de licentie toegang geeft tot welk recht van Knowmax Quest.

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