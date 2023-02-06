---
title: Authenticatie en autorisatie
permalink: /concepts/authentication
---

## Mehtodes van authenticatie en autorisatie
Knowmax Quest kent een aantal verschillende manieren om gebruikers te authenticeren en te autoriseren. In dit document wordt uitgelegd hoe deze werken en hoe ze gebruikt kunnen worden.

## Bearer token
Alle verzoeken naar de API van Knowmax Quest moeten een geldig bearer token in de header hebben voor authenticatie en autorisatie van de gebruiker. het bearer token beschrijft wie de gebruiker is en wat de gebruiker mag.

## Toepassingen
Er zijn verschillende manieren om een bearer token voor toegang tot de API van Knowmax Quest te verkrijgen. De gekozen manier hangt af van de toepassing.

## Server-to-server authenticatie
Bij server-to-server toepassingen gaat het altijd om twee vertrouwde toepassingen die met elkaar communiceren. De Knowmax Quest server aan de ene kant en de vertouwde server van de gebruiker aan de andere kant. Het vertrouwen bestaat er uit dat de geheime Knowmax Magma API sleutel velig kan worden opgeslagen op de server van de gebruiker.

Voor server-to-server toepassingen, gebruikt Knowmax Quest het Knowmax Magma systeem. Met een Knowmax Magma API sleutel kunnen gebruikers een bearer token verkrijgen.

***Endpoint***
```url
POST /api/authentication/magma
```

***Request body ```application/json```***
```json
{
  "magmaName": "waarde",
  "secret": "waarde"
}
```

## Client-to-server authenticatie
Client-to-server toepassingen werken op een client, zoals een webbrowser of een mobiele app. We kunnen er niet op vertrouwen dat de geheime Knowmax Magma API sleutel er veilig kan worden opgeslagen. Verder zullen er mogelijk vele clients zijn die communiceren met de Knowmax Quest server. Het is niet praktisch die allemaal met 1 Knowmax Magma API sleutel te laten werken. We veliezen dan de mogelijkheid om een enkele client de toegang te ontzeggen zonder dat de andere clients daar last van hebben.

Voor client-to-server toepassingen zijn er twee manieren om een bearer token te verkrijgen.

### Knowmax Licentie token
Knowmax Quest kan optioneel gekoppeld zijn aan een Knowmax Licentiesysteem. In dat geval kunnen gebruikers met een geldig token voor het Knowmax Licentiesysteem, dat token gebruiken om een bearer token voor Knowmax Quest te verkrijgen. Het token voor het Knowmax Licentiesysteem geeft toegang tot de persoonlijke licentie van een gebruiker en is door de gebruiker verkregen met de kennis van bijvoorbeeld een wachtwoord.

```
POST /api/authentication/licencesystem
```

### Gedelegeerde authenticatie
Bij deze opzet wordt server-to-server authenticatie gebruikt om een bearer token te verkrijgen voor een andere gebruiker. Een bearer token voor de client wordt in dit geval op de vertrouwde server aangevraagd namens de gebruiker. Deze bearer token kan vervolgens in de client gebruikt worden voor directe communicatie met de Knowmax Quest server.

```
POST /api/authentication/magma
```