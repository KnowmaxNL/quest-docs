---
title: Quest transformaties
permalink: /concepts/quest-trans
---

> Dit onderdeel gaat over Knowmax Quest 4 en is nog niet bijgewerkt voor Knowmax Quest versie 5.

Knowmax Quest heeft de mogelijkheid om via de API opgevraagde documenten of documentonderdelen te transformeren volgens vooraf bepaalde transformatie-instellingen. In XML beschikbare documenten kunnen door Knowmax Quest worden omgezet naar HTML voor direct gebruik binnen op Knowmax Quest gebaseerde applicaties.

Naast transformatie van XML naar HTML is het ook mogelijk afbeeldingen verkregen via de ingang **Api/Document/Data** om te zetten met behulp van de Imageresizer plugin. Ook voor het omzetten van onderdelen naar PDF zijn tranformaties mogelijk. Dit onderdeel zal uitsluitend ingaan op transformaties van XML naar HTML door middel van XSL.

# Bronnen
Er zijn op dit moment vier bronnen binnen Knowmax Quest die XML transformaties ondersteunen, te weten:

1. **Api/Document/Data** voor het opvragen van de inhoud van een document-locatie;
2. **Api/Document/Compare** voor het opvragen van de inhoud van een document-locatie die vergeleken is met de inhoud van een andere versie van de document-locatie;
3. **Api/Document/InfoXml** voor het opvragen van informatie over een document;
4. **Api/Document/TocXml** voor het opvragen van de inhoudsopgave van een document.

Mogelijk worden in de toekomst andere bronnen die transformaties ondersteunen toegevoegd.

# Voorbeelden
Om de opgevraagde inhoud te transformeren kan één van de binnen het gebruikte Quest systeem beschikbare transformaties worden aangesproken. Hiervoor wordt aan de URL de parameter **transform** met als waarde het label van één van de beschikbare transformaties toegevoegd.

```
https://quest.knowmax.dev/Api/Document/Data/pub24-xml/1/1.2?transform=publicatie-xsl
```
```
https://quest.knowmax.dev/Api/Document/TocXml/pub24-xml?transform=inhoudsopgave-xsl 
```
```
https://quest.knowmax.dev/Api/Document/InfoXml/pub24-xml?transform=info-xsl
```

# Automatische keuze van transformatie
Voor de bron **Api/Document/Data** is het ook mogelijk om op basis van het gevraagde onderdeel automatisch een transformatie te kiezen. Deze keuze wordt gemaakt op basis van als JSON opgeslagen instellingen voor een bepaalde transformatie. Iedere transformatie kan dergelijke JSON keuzedata voor verschillende doeleinden bevatten. Om gebruik te kunnen maken van deze mogelijkheid moet de parameter **transform** een waarde tussen blokhaken bevatten. Deze waarde geeft aan welke JSON keuzedata getoetst moet worden.

Onderstaande JSON data geeft een voorbeeld van deze instelling voor een bepaalde transformatie. Door voor **transform** de waarde **[test]** te gebruiken, zal deze transformatie gekozen worden voor alle documenten die met de **QuestIni** importer geimporteerd zijn en voor het metawaarde veld **Custom.QuestImport** de waarde **TestXmlPublicatie** hebben.

```json
        {
          "test": {
            "ImporterId": "QuestIni",
            "Meta": [
              {
                "Label": "Custom.QuestImporter",
                "Value": "TestXmlPublicatie"
              }
            ],
            "QuestId": "library/manual/abc",
            "QuestVersion": 10
          }
        }    
```

De velden **ImporterId**, **Meta**, **QuestId** en **QuestVersion** zijn optioneel. In de array **Meta** kunnen meerdere metawaarden worden opgenomen waaraan het document moet voldoen. Het veld **test** is in het bovenstaande voorbeeld een object, maar mag ook een array van objecten bevatten. Om gekozen te worden zal het getoetste document aan alle condities moeten voldoen.

Gebruik in de array **Meta** het veld **Label** om de te toetsen metadatawaarde aan te duiden. Gebruik de notatiewijze familienaam gevolgd door het label van de metawaardedefinitie gescheiden door een . (punt). Gebruik het optionele veld **Negate** met waarde **true** om aan te geven dat het om een ontkennende conditie gaat. Het veld **Value** bevat de te toetsen waarde. **Value** is optioneel. Bij het niet opgeven van **Value** zal het bestaan van de beschreven metawaarde getoetst worden. Bij toetsing van de metadatawaarden wordt gekeken naar de waarden op root niveau en de waarden op het specifieke te transformeren niveau.

# Parameters binnen XSL
Afhankelijk van de gebruikte bron heeft men tijdens de transformatie de beschikking over parameters welke aan de XSL worden doorgegeven. Deze parameters kunnen in het XSL-bestand gebruikt worden door middel van **<xsl:param name="parameternaam"/>**. Daarna zijn de gedefinieerde parameters als XSL-variabelen te gebruiken. De parameternaam wordt in dat geval voorafgegaan door een **\$**-teken. Bijvoorbeeld: **<xsl:value-of select="\$parameternaam"/>**.

Momenteel zijn parameters alleen beschikbaar als een bron gebruikt wordt waarbij een Quest identificatie opgegeven moet worden.

Parameter | Omschrijving
--- | ---
Quest.UrlPattern | Met het URL-patroon is de volledige URL te reconstrueren om de inhoud van dit onderdeel op te vragen. Bijvoorbeeld: **https://quest.knowmax.dev/Api/Document/Data/{0}** . **{0}** beschrijft in dit patroon het onderdeel dat vervangen kan worden door een Quest identificatie.
Document.QuestId | Quest identificatie van het document zonder eventuele identificatie voor het documentonderdeel.
Document.Title | Titel van het hele document.
Version.Current |	Geeft aan of dit de huidige versie van het document betreft. Mogelijke waarden: **true** en **false**.
Version.Date | Versiedatum van dit document.
Version.Description | Versie-omschrijving indien deze bekend is..
Version.Title | Versie-titel indien deze bekend is.
Version.Number | Nummer van deze versie.
Node.FullQuestId| Volledige Quest identificatie van het opgevraagde document(onderdeel).
Node.QuestId | Bevat uitstuitend de Quest identificatie van het opgevraagde documentonderdeel, dus zonder document-id.
Node.Title | Titel van het documentonderdeel.
Node.Sequence| Volgordenummer van het opgevraagde documentonderdeel in de inhoudsopgave van het document.
Node.Level | Niveau van het opgvraagde documentonderdeel in inhoudsopgave van het document.
Node.RootPath | Bevat path naar root van document. Gebruik deze als voorloper voor het opvragen van resources uit het document. Resources worden altijd opgeslagen relatief aan de root van het document.

# Speciale onderdelen in de geïmporteerde XML
Het is mogelijk dat tijdens de import van de XML in Knowmax Quest enkele speciale elementen en attributen in de XML gegenereerd zijn waar rekening mee gehouden dient te worden. Dit geldt alleen voor XML afkomstig uit een bron die een document(onderdeel) geeft. Deze aanvullingen zijn allen binnen de namespace **https://schemas.knowmax.nl/2011/Quest** met prefix **quest** opgenomen.

Parameter | Omschrijving
--- | ---
DocumentNode-Placeholder (xml-element) | Deze placeholder worden automatisch bij het "opknippen" van de XML tijdens de import ingevoegd. Opgevraagde content dat met de parameter **compose** met waarde **true** wordt opgevraagd zal geen element **<Document-Placeholder id="xx" title="xx"/>** bevatten. De placeholder is immers vervangen door de werkelijke content door de parameter **compose** met waarde **true**.
ResourceName (xml-attribuut) | ResourceName is een attribuut dat wordt toegevoegd aan elementen die verwijzen naar een resource (afbeelding, pdf-bestand, enz). Het bevat de absolute verwijzing naar een resource vanuit de root van het document. De oorspronkelijke verwijzing kan mogelijk een relatieve verwijzing zijn vanuit het huidige documentonderdeel. In de meeste gevallen is het goed om ResourceName vooraf gegaan door de parameter **Node.RootPath** te gebruiken om naar een resource te verwijzen. <br /> Voorbeeld: In een documentonderdeel **hfd1/paragraaf1-1** van een document met identificatie **groep1/boek-abc** wordt als volgt naar een afbeelding verwezen: **images/1.jpg**. De waarde voor ResourceName zal dan zijn: **hfd1/paragraaf1-1/images/1.jpg**.
ResourceStatus (xml-attribuut) | Ondersteunde importers zullen elementen die verwijzen naar media zoals afbeeldingen voorzien van dit attribuut om aan te geven wat de status van de media is waarnaar verwezen wordt. Mogelijke waarden: **Valid**, **NotFound**, **Damaged**. Afhankelijk van de gebruikte importer kan het zo zijn dat dit attribuut alleen voorkomt bij verwijzingen naar media die niet de status **Valid** hebben.

# Speciale onderdelen in XML na compositie
Als bij het opvragen van een XML document(onderdeel) compositie wordt toegepast, kunnen er mogelijk enkele speciale XML attributen aan de XML toegevoegd worden. Dit geldt alleen voor XML afkomstig uit een bron die een document(onderdeel) geeft. Deze aanvullingen zijn allen binnen de namespace **https://schemas.knowmax.nl/2011/Quest** met prefix **quest** opgenomen.

Parameter | Omschrijving
--- | ---
QuestId (xml-attribuut) | Het attribuut QuestId bevat de volledige Quest-identificatie voor het betreffende document(onderdeel), inclusief het versienummer indien van toepassing.
QuestUrlPattern (xml-attribuut) | Het attribuut QuestURLPattern bevat het patroon hoe he betreffende documentonderdeel opgevraagd kan worden bij de Knowmax Quest API. Bijvoorbeeld: **https://quest.knowmax.dev/Api/Document/Data/{0}** . **{0}** beschrijft in dit patroon het onderdeel dat vervangen kan worden door een Quest identificatie.