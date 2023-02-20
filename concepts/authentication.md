---
title: Authenticatie en autorisatie
permalink: /concepts/authentication
---

# Manieren van authenticatie en autorisatie
Knowmax Quest kent een aantal verschillende manieren om gebruikers te authenticeren en te autoriseren. We beschrijven hier hoe deze werken en hoe ze gebruikt kunnen worden.

# Bearer token
Alle verzoeken naar de API van Knowmax Quest moeten een geldig bearer token in de header hebben voor authenticatie en autorisatie van de gebruiker. Het bearer token beschrijft wie de gebruiker is en wat de [rechten](/concepts/rights) zijn van de gebruiker. Knowmax Quest gebruikt een JSON Web Token (JWT), deze wordt bij ieder verzoek aan Knowmax Quest in de ***Authorization*** header meegestuurd door gebruik te maken van het ***Bearer*** schema.

```
Authorization: Bearer <token>
```

> Zie [JWT.io](https://jwt.io/introduction/) voor meer informatie over JSON Web Tokens.

# Toepassingen
Er zijn verschillende manieren om een bearer token voor toegang tot de API van Knowmax Quest te verkrijgen. De gekozen manier hangt af van de toepassing.

# Server-to-server authenticatie
Bij server-to-server toepassingen gaat het altijd om twee vertrouwde toepassingen die met elkaar communiceren. De Knowmax Quest server aan de ene kant en de vertouwde server van de gebruiker aan de andere kant. Het vertrouwen bestaat er uit dat de geheime Knowmax Magma API sleutel velig kan worden opgeslagen op de server van de gebruiker.

> Voor server-to-server toepassingen, gebruikt Knowmax Quest het Knowmax Magma systeem. Met een Knowmax Magma API sleutel kunnen gebruikers een bearer token verkrijgen.

***Endpoint***
```
POST /api/authentication/magma
```

***Request body ```application/json```***
```json
{
  "magmaName": "name-from-knowmax-magma",
  "secret": "secret-from-knowmax-magma"
}
```

# Client-to-server authenticatie
Client-to-server toepassingen werken op een client, zoals een webbrowser of een mobiele app. We kunnen er niet op vertrouwen dat de geheime Knowmax Magma API sleutel er veilig kan worden opgeslagen. Verder zullen er mogelijk vele clients zijn die communiceren met de Knowmax Quest server. Het is niet praktisch die allemaal met 1 Knowmax Magma API sleutel te laten werken. We veliezen dan de mogelijkheid om een enkele client de toegang te ontzeggen zonder dat andere clients daar last van hebben.

Voor client-to-server toepassingen zijn er twee manieren om een bearer token te verkrijgen.

## Knowmax Licentie token
Knowmax Quest kan optioneel gekoppeld zijn aan een Knowmax Licentiesysteem. In dat geval kunnen gebruikers met een geldig token voor het Knowmax Licentiesysteem, dat token gebruiken om een bearer token voor Knowmax Quest te verkrijgen. Het token voor het Knowmax Licentiesysteem geeft toegang tot de persoonlijke licentie van een gebruiker en is door de gebruiker verkregen met de kennis van bijvoorbeeld een wachtwoord.

***Endpoint***
```
POST /api/authentication/licensesystem
```

***Request body ```application/json```***
```json
{
  "token": "token-from-knowmax-license-system"
}
```

## Gedelegeerde authenticatie
Bij gedelegeerde authenticatie wordt server-to-server authenticatie gebruikt om een bearer token te verkrijgen voor een andere gebruiker. Een bearer token voor de client wordt in dit geval op de vertrouwde server aangevraagd namens de gebruiker. Deze bearer token kan vervolgens in de minder vertrouwde client gebruikt worden voor directe communicatie met de Knowmax Quest server.

> Gedelegeerde authenticatie is alleen beschikbaar voor Knowmax Magma API sleutels met het **AllowAuthenticate** recht.

***Endpoint***
```
POST /api/authentication/magma
```

***Request body ```application/json```***
```json
{
  "magmaName": "name-from-knowmax-magma",
  "secret": "secret-from-knowmax-magma",
  "user": {
    "id": "id-of-user",
    "name": "name-of-user",
    "email": "email-of-user",
    "organisationName": "name-of-organisation-of-user",
    "allowData": true,
    "allowIndex": true,
    "allowModify": true,
    "allowStatistics": true,
    "allowManagement": true    
  }
}
```
**email** en **organisationName** zijn optioneel. Met de **allowX** waarden kunnen de gewenste [rechten](/concepts/rights) voor de gebruiker worden ingesteld. Alleen rechten die ook beschikbaar zijn voor de gebruikte Knowmax Magma API sleutel kunnen worden ingesteld. Het **AllowAuthenticate** recht kan niet ingesteld worden voor een gedelegeerde gebruiker.