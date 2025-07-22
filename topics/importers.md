---
title: 🚚 Importers
permalink: /topics/importers
category: Onderwerpen
order: 10
---

Tijdens het importeren van [documentversies](/topics/document-structure) gebruikt Knowmax Quest een importer geschikt voor een bepaald documentformaat om de documentversie in Knowmax Quest te importeren. De gebruikte importer stelt bijvoorbeeld vast of en in welke logische eenheden ([documentnodes](/topics/document-structure)) een document wordt [opgeknipt](/topics/composition) en welke [metadata](/topics/metadata) voor de documentversie wordt vastgelegd. Knowmax Quest kent verschillende ingebouwde importers voor bijvoorbeeld Adobe PDF bestanden en XML bestanden in diverse formaten.

Knowmax Quest kiest automatisch een geschikte importer voor een te importeren documentversie. Gebruikers kunnen geen invloed uitoefenen op deze keuze. Knowmax bepaalt tijdens installatie en configuratie van een Knowmax Quest systeem welke importers beschikbaar zijn en dus welke documentformaten geïmporteerd kunnen worden.

Knowmax Quest kent vijf methoden voor het importeren van een documentversie, te weten:

Importeermethode | Actie
---|---
NewVersion | De documentversie wordt achteraan toegevoegd
OverwriteLastVersion | De laatste documentversie wordt overschreven
OverwriteVersion | De documentversie met het overeenkomstige opgegeven nummer wordt overschreven
ResetVersion | Alle documentversies worden vervangen door deze documentversie en deze versie krijgt versienummer 1
Auto | Knowmax Quest bepaalt zelf aan de hand van de opgegeven versiedatum of een documentversie moet worden toegevoegd, tussengevoegd of overschreven