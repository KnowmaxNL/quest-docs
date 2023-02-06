---
title: Claims
permalink: /concepts/claims
---

# Inleiding
Het na [authenticatie](/concepts/authentication) verkregen bearer token beschrijft wie de gebruiker is en wat de rechten van de gebruiker zijn. Deze rechten worden uitgedrukt in claims. Claims zijn stukjes informatie die in het bearer token zijn opgenomen. 

Afhankelijk van de toegekende claims is het gebruik van bepaalde functionaliteit van de API wel of niet toegestaan. Welke claims beschikbaar zijn, is afhankelijk van de toepassing en de beschikbare functionaliteit voor het desbetreffende Knowmax Quest systeem. Claims worden ingesteld door Knowmax bij uitgifte van een Knowmax Magma API sleutel.

# Beschikbare claims

## AllowUse
Beschikbaar voor iedere gebruiker. Staat gebruik van basisfunctionaliteit toe.

## AllowData
Staat het opvragen van data toe.

## AllowModify
Staat het maken van wijzigingen in data toe.

## AllowIndex
Staat het opvragen en beheren van indexen toe.

## AllowManagement
Staat toegang tot de beheerinterface toe.

## AllowAuthenticate
Staat authenticatie namens andere gebruikers toe.

## AllowStatistics
Staat het gebruik van Knowmax Quest Statistics toe.