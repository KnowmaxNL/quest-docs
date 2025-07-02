---
title: Knowmax Quest Statistics database
permalink: /topics/statistics-database
category: Onderwerpen
order: 19
---
title: Knowmax Quest Statistics database
permalink: /concepts/statistics-database
---

Beschrijving van tabelstructuur in de database ten behoeve van door Knowmax Quest bijgehouden [statistieken](/concepts/statistics).

# Document, documentversie en documentnode
Om de statistieken te kunnen interpreteren is het belangrijk te weten wat een document, documentversie en documentnode is.

| Onderdeel | Omschrijving |
| --- | --- |
| Document | De eenheid waarbinnen 1 of meerdere documentversies zijn opgenomen. |
| Documentversie | Een specifieke versie van een document. |
| Documentnode | Het kleinste onderdeel behorende bij een documentversie waarvoor data is op te vragen. |

# Tabellen
Tabelen voor het bijhouden van statistieken.

## Application
Alle statistieken worden bijgehouden per applicatie. Een applicatie is een logische eenheid voor een bepaald gebruik van Knowmax Quest. Deze tabel bevat alle applicaties waarvoor het Knowmax Quest systeem statistieken bijhoudt.

| Veld | Omschrijving |
| --- | --- |
| Id | Unieke identificatie van application in database. |
| Name | Naam van applicatie |

## Identity
Er worden statistieken bijgehouden per unieke gebruiker. Iedere unieke gebruiker wordt beschreven door een identity die is opgenomen in deze tabel. Zoals bij alle statistieken worden ook deze identities per **application** bijgehouden. Tijdens de [authenticatie](authentication) van de gebruiker is de naam (veld **Name**) en unieke identificatie (veld **CustomId**) vastgesteld. Deze unieke identificatie wordt meestal bepaald door het systeem dat via delegatie de authenticatie van de gebruiker heeft uitgevoerd. Binnen Knowmax Quest heeft deze identificatie geen betekenis anders dan het herkennen van unieke gebruikers.

| Veld | Omschrijving |
| --- | --- |
| Id | Unieke identificatie van identity in database. |
| CustomId | Unieke identificatie van identity in extern systeem zoals bepaald tijdens [authenticatie](/concepts/authentication). |
| Name | Naam van identity in extern systeem zoals bepaald tijdens [authenticatie](/concepts/authentication). |
| Created | Tijdstip van eerste bevraging door gebruiker. |
| Modified | Tijdstip van laatste bevraging door gebruiker. |

## DocumentPureStatistics
Bevat per **document** het aantal keer dat data voor een documentnode binnen een document opgevraagd is door een willekeurige gebruiker. 

| Veld | Omschrijving |
| --- | --- |
| DocumentId | Unieke identificatie van het document |
| ViewCount | Aantal keer data opgevraagd |
| Created | Tijdstip van eerste keer data opgevraagd |
| Modified | Tijdstip van laatste keer data opgevraagd |

## DocumentStatistics
Bevat per **documentnode** het aantal keer dat data is opgevraagd door een willekeurige gebruiker.

| Veld | Omschrijving |
| --- | --- |
| DocumentId | Unieke identificatie van het document |
| DocumentVersionId | Unieke identificatie van de documentversion |
| DocumentNodeId | Unieke identificatie van de documentnode |
| ViewCount | Aantal keer data opgevraagd |
| Created | Tijdstip van eerste keer data opgevraagd |
| Modified | Tijdstip van laatste keer data opgevraagd |

## IdentityDocumentPureStatistics
Bevat per **document** het aantal keer dat data is opgevraagd door een specifieke gebruiker.

| Veld | Omschrijving |
| --- | --- |
| IdentityId | Unieke identificatie van de gebruiker |
| DocumentId | Unieke identificatie van het document |
| ViewCount | Aantal keer bekeken |
| Created | Tijdstip van eerste keer bekeken |
| Modified | Tijdstip van laatste keer bekeken |

## IdentityDocumentStatistics
Bevat per **documentnode** het aantal keer dat data is opgevraagd door een specifieke gebruiker.

| Veld | Omschrijving |
| --- | --- |
| IdentityId | Unieke identificatie van de gebruiker |
| DocumentId | Unieke identificatie van het document |
| DocumentVersionId | Unieke identificatie van de documentversion |
| DocumentNodeId | Unieke identificatie van de documentnode |
| ViewCount | Aantal keer data opgevraagd |
| Created | Tijdstip van eerste keer data opgevraagd |
| Modified | Tijdstip van laatste keer data opgevraagd |

## IdentityDocumentView
Bevat een record per keer dat data is opgevraagd voor een **documentnode** door een specifieke gebruiker.

| Veld | Omschrijving |
| --- | --- |
| IdentityId | Unieke identificatie van de gebruiker |
| DocumentId | Unieke identificatie van het document |
| DocumentVersionId | Unieke identificatie van de documentversion |
| DocumentNodeId | Unieke identificatie van de documentnode |
| Created | Tijdstip waarop data is opgevraagd |

## IdentityFavoriteDocument
Geeft aan of een bepaalde identiteit een bepaald document, documentversie of documentnode als favoriet heeft gemarkeerd. Alleen beschikbaar als de module Knowmax Quest Favorites is ingeschakeld.

# Overige tabellen
Vanuit de tabellen voor statistieken zijn er verwijzingen naar de tabellen **Document**, **DocumentVersion** en **DocumentNode**. Deze tabellen bevatten alle informatie over respectievelijk een document, een documentversie binnen een document en een node binnen een documentversie.

Deze tabellen kunnen gebruikt worden om een interpretatie te geven aan de opgevraagde onderdelen in de verschillende statistieken.

# "Pure" tabellen DocumentPureStatistics en IdentityDocumentPureStatistics
Binnen Knowmax Quest kan de laatste documentversie overschreven worden. Dat kan bijvoorbeeld voorkomen om een kleine fout op te lossen. Knowmax raadt het overschrijven van versies over het algemeen af. De aanbevolen manier is het toevoegen van een nieuwe versie. Wanneer er toch gekozen wordt om de laatste versie te overschrijven, zal er in de tabel **DocumentVersion** een nieuwe documentversie worden toegevoegd. De bijbehorende statistieken die verzwijzen naar de overschreven documentversion zullen verdwijnen uit de statistieken [^1]. De nieuwe versie is immers nog nooit door iemand bekeken.

De tabellen **DocumentPureStatistics** en **IdentityDocumentPureStatistics** houden de keren bij dat de data van een documentnode is opgevraagd, ongeacht de documentversie of documentnode.

[^1]: Het permanent verwijderen van data kan ongeveer 14 dagen duren.