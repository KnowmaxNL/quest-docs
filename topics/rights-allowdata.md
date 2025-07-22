---
title: 🛡️ AllowData recht 
permalink: /topics/rights-allowdata
category: Onderwerpen
order: 2
---

# Afscherming data
Het [recht](/topics/rights) **AllowData** is nodig om de inhoud van Quest documenten op te  vragen. De status, metadata en de inhoudsopgave van Quest documenten is ook zonder dit recht op te vragen.

## Knowmax Licentiesysteem gebruikers (client-to-server authenticatie)
Bij client-to-server [authenticatie](/topics/authentication) via een Knowmax Licentiesysteem token, zal de gebruiker alleen toegang hebben tot de Quest documenten waar toegang op is gegeven in de licentie uit het Knowmax Licentiesysteem.

## Knowmax Magma API sleutel gebruikers (server-to-server authenticatie)
Mogelijk gelden er voor de Knowmax Magma API sleutel ook nog andere beperkingen die bepalen welke data op te vragen is. Het gaat dan om een berperking waardoor alleen de data van specifieke [Quest documenten](/topics/quest-id) op te vragen is.

### Afscherming op collectie
Knowmax kan instellingen maken die zorgen dat de Knowmax Magma API sleutel alleen toegang heeft tot documenten opgenomen in een bepaalde collectie.

### Afscherming volgens licentie
Knowmax kan instellingen maken die zorgen dat de Knowmax Magma API sleutel alleen toegang heeft tot documenten waar toegang op gegeven wordt via een bepaalde licentie.